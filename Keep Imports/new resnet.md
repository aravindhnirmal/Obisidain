[[Keep/Colour/DEFAULT]] 

import os
import torch
import torch.nn as nn
import torchvision.transforms as transforms
from torch.utils.data import DataLoader, Dataset
from torchvision.models import resnet18
from PIL import Image
from flask import Flask, request, jsonify, render_template

# Define ResNet18 model class
class CustomResNet18(nn.Module):
    def __init__(self, num_classes):
        super(CustomResNet18, self).__init__()
        self.resnet = resnet18(pretrained=True)
        num_ftrs = self.resnet.fc.in_features
        self.resnet.fc = nn.Linear(num_ftrs, num_classes)

    def forward(self, x):
        return self.resnet(x)

# Define CustomDataset class
class CustomDataset(Dataset):
    def __init__(self, root_dir, transform=None):
        self.root_dir = root_dir
        self.transform = transform
        self.image_dir = os.path.join(root_dir, 'images')
        self.label_dir = os.path.join(root_dir, 'labels')
        self.image_files = sorted([f for f in os.listdir(self.image_dir) if f.endswith('.jpg')])
        self.label_files = sorted([f for f in os.listdir(self.label_dir) if f.endswith('.txt')])

    def __len__(self):
        return len(self.image_files)

    def __getitem__(self, idx):
        img_name = os.path.join(self.image_dir, self.image_files[idx])
        label_name = os.path.join(self.label_dir, self.label_files[idx])

        image = Image.open(img_name).convert('RGB')

        with open(label_name, 'r') as file:
            label = float(file.readline().strip().split()[0])

        if self.transform:
            image = self.transform(image)

        return image, label

# Define transformations
transform = transforms.Compose([
    transforms.Resize((224, 224)),
    transforms.ToTensor(),
    transforms.Normalize(mean=[0.485, 0.456, 0.406], std=[0.229, 0.224, 0.225])
])

# Load dataset and create DataLoader
root_dir = '/home/kali/Downloads/fracture/train/'
  # Replace 'path/to/dataset' with the actual path to your dataset
dataset = CustomDataset(root_dir, transform=transform)
train_loader = DataLoader(dataset, batch_size=32, shuffle=True)

# Initialize ResNet-18 model
num_classes = 1  # Assuming binary classification
model = CustomResNet18(num_classes)

# Check if GPU is available
device = torch.device("cuda" if torch.cuda.is_available() else "cpu")
model.to(device)

# Define loss function and optimizer
criterion = nn.BCEWithLogitsLoss()
optimizer = torch.optim.Adam(model.parameters(), lr=0.001)

# Training loop
num_epochs = 1
for epoch in range(num_epochs):
    model.train()
    for images, labels in train_loader:
        images, labels = images.to(device), labels.to(device)

        optimizer.zero_grad()
        outputs = model(images)
        loss = criterion(outputs.squeeze(), labels.float())  # Squeeze the output to remove extra dimension
        loss.backward()
        optimizer.step()

    print(f'Epoch [{epoch+1}/{num_epochs}], Loss: {loss.item():.4f}')

print("Training finished.")
# Save the trained model
torch.save(model.state_dict(), 'trained_resnet18.pth')

# Initialize Flask app
app = Flask(__name__, template_folder='templates2')

# Define a route for the home page
@app.route('/')
def home():
    return render_template('index.html')

# Define a route for the result page
# Define a route for the result page
@app.route('/result', methods=['POST'])
def result():
    if 'image' not in request.files:
        return jsonify({'error': 'No image provided'})
    
    image_file = request.files['image']
    
    try:
        image = Image.open(image_file).convert('RGB')
        image_tensor = transform(image).unsqueeze(0)
        with torch.no_grad():
            output = model(image_tensor)
            prediction = torch.sigmoid(output).item()
            result = "Fractured" if prediction >= 0.5 else "Not Fractured"
        return render_template('result.html', prediction=result)
    except Exception as e:
        return jsonify({'error': str(e)})

# Run the Flask app
if __name__ == '__main__':
    app.run(debug=True)







import numpy as np
import matplotlib.pyplot as plt
from sklearn.metrics import confusion_matrix, precision_recall_curve, roc_curve, f1_score, auc
def evaluate_classification(y_true, y_pred):
    # Compute confusion matrix
    cm = confusion_matrix(y_true, y_pred)

    # Compute normalized confusion matrix
    cm_normalized = cm.astype('float') / cm.sum(axis=1)[:, np.newaxis]

    # Compute F1 score
    f1 = f1_score(y_true, y_pred)

    # Compute precision-recall curve
    precision, recall, _ = precision_recall_curve(y_true, y_pred)

    # Compute area under the precision-recall curve
    pr_auc = auc(recall, precision)

    # Compute ROC curve
    fpr, tpr, _ = roc_curve(y_true, y_pred)

    # Compute area under the ROC curve
    roc_auc = auc(fpr, tpr)

    # Plot confusion matrix
    plt.figure()
    plt.imshow(cm_normalized, interpolation='nearest', cmap=plt.cm.Blues)
    plt.title('Normalized Confusion Matrix')
    plt.colorbar()
    plt.xlabel('Predicted label')
    plt.ylabel('True label')
    plt.xticks([0, 1])
    plt.yticks([0, 1])
    plt.show()

    # Plot precision-recall curve
    plt.figure()
    plt.plot(recall, precision, marker='.')
    plt.xlabel('Recall')
    plt.ylabel('Precision')
    plt.title('Precision-Recall Curve (AUC = %0.2f)' % pr_auc)
    plt.show()

    # Plot ROC curve
    plt.figure()
    plt.plot(fpr, tpr, marker='.')
    plt.xlabel('False Positive Rate')
    plt.ylabel('True Positive Rate')
    plt.title('ROC Curve (AUC = %0.2f)' % roc_auc)
    plt.show()

    return f1, pr_auc, roc_auc

