[[Keep/Colour/DEFAULT]] 

import os
import torch
import torch.nn as nn
import torchvision.transforms as transforms
from torch.utils.data import DataLoader, Dataset
from PIL import Image


class FCRNN(nn.Module):
    def __init__(self):
        super(FCRNN, self).__init__()
        [[first]] convolutional layer with 3 input channels, 16 output channels, and a kernel size of 3x3.
        self.conv1 = nn.Conv2d(3, 16, 3, 1)
        self.pool = nn.MaxPool2d(2, 2)
        # max-pooling layer with a kernel size of 2x2 and a stride of 2.
        self.conv2 = nn.Conv2d(16, 32, 3, 1)
        #  second convolutional layer with 16 input channels, 32 output channels, and a kernel size of 3x3.
        self.gru = nn.GRU(32 * 54 * 54, 128, batch_first=True)
        [[type]] of recurrent neural network (RNN) architecture
        [[Gated]] Recurrent Unit (GRU) layer. It takes an input size of 32 * 54 * 54 (computed from the shape of the output of the second convolutional layer) and produces an output of size 128. batch_first=True means the input and output tensors are provided as (batch_size, seq_length, feature_dim).
        self.fc = nn.Linear(128, 1)  # Assuming binary classification

    def forward(self, x):
        x = self.pool(nn.functional.relu(self.conv1(x)))
        # forward pass of the neural network.
        x = self.pool(nn.functional.relu(self.conv2(x)))
        # output from the first convolutional layer is passed through the second convolutional layer (conv2), followed by ReLU activation, and then max-pooling.
        x = x.view(-1, 32 * 54 * 54)
        x = x.unsqueeze(1)  # Add a time dimension
        x, _ = self.gru(x)
        [[GRU]] layer processes the data and produces outputs at each step, but only the last output is retained (x[:, -1, :]) and passed to the fully connected layer (fc).
        x = x[:, -1, :]  # Get the last output of the GRU
        x = self.fc(x)
        return x


class CustomDataset(Dataset):
    def __init__(self, root_dir, transform=None):
        self.root_dir = root_dir
        self.transform = transform
        [[optional]] transformation to be applied to the images.
        self.image_dir = os.path.join(root_dir, 'images')
        self.label_dir = os.path.join(root_dir, 'labels')
        self.image_files = sorted([f for f in os.listdir(self.image_dir) if f.endswith('.jpg')])
        self.label_files = sorted([f for f in os.listdir(self.label_dir) if f.endswith('.txt')])

    def __len__(self):
      [[it]] returns the total number of samples in the dataset, which is equal to the number of image files present.
        return len(self.image_files)

    def __getitem__(self, idx):
        img_name = os.path.join(self.image_dir, self.image_files[idx])
        label_name = os.path.join(self.label_dir, self.label_files[idx])

        image = Image.open(img_name).convert('RGB')

        with open(label_name, 'r') as file:
            label = file.readline().strip()  # Read the first line of the label file
            parts = label.split()  # Split the label into individual parts
            class_label = int(parts[0])  # Extract the class label

        if self.transform:
            image = self.transform(image)

        return image, class_label



# Define transformations
transform = transforms.Compose([
    transforms.Resize((224, 224)),
    [[Resizes]] the input image to a square shape of size 224x224 pixels.
    transforms.ToTensor(),
    # converts the image data from a PIL Image object (or numpy array) to a tensor, which is the primary data type used in PyTorch for training neural networks
    transforms.Normalize((0.5, 0.5, 0.5), (0.5, 0.5, 0.5))
    [[imilar]] scale, which can help improve training stability and convergence
])

# Load dataset and create DataLoader
from google.colab import drive
drive.mount('/content/drive')

root_dir = '/content/drive/My Drive/fracture/train'
dataset = CustomDataset(root_dir, transform=transform)
train_loader = DataLoader(dataset, batch_size=32, shuffle=True)

# Initialize model
model = FCRNN()

# Check if GPU is available
device = torch.device("cuda" if torch.cuda.is_available() else "cpu")
[[Checks]] if a GPU is available. If available, it assigns the GPU device; otherwise, it uses the CPU.
model.to(device)

# Define loss function and optimizer
criterion = nn.BCEWithLogitsLoss()
# Binary Cross Entropy with Logits Loss, which is commonly used for binary classification tasks.
optimizer = torch.optim.Adam(model.parameters(), lr=0.001)
# Adam optimizer is used here, and it optimizes the parameters of the model with a learning rate of 0.001.
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
    # Precision-Recall curve is created by plotting precision on the y-axis and recall on the x-axis for different threshold values
    #
    plt.show()

    # Plot ROC curve
    plt.figure()
    plt.plot(fpr, tpr, marker='.')
    plt.xlabel('False Positive Rate')
    plt.ylabel('True Positive Rate')
    plt.title('ROC Curve (AUC = %0.2f)' % roc_auc)

# ROC AUC (Receiver Operating Characteristic Area Under the Curve) is the area under the receiver operating characteristic curve.
# The ROC curve plots the true positive rate (sensitivity) against the false positive rate (1-specificity) for different threshold values.
    plt.show()

    return f1, pr_auc, roc_auc

# Example usage
y_true = np.array([0, 1, 1, 0, 1])
y_pred = np.array([0, 1, 1, 0, 0])
f1, pr_auc, roc_auc = evaluate_classification(y_true, y_pred)
print(f'F1 score: {f1}')
# Precision measures the proportion of true positive predictions among all positive predictions,
# while recall measures the proportion of true positive predictions among all actual positives in the dataset


#  F1 score ranges from 0 to 1, where higher values indicate better performance
#  F1 score of 1 indicates perfect precision and recall, while a score of 0 indicates poor performance.
print(f'Precision-Recall AUC: {pr_auc}')
print(f'ROC AUC: {roc_auc}')


import numpy as np
import matplotlib.pyplot as plt
from sklearn.metrics import precision_recall_curve, auc

def f1_confidence_curve(y_true, y_score):
    thresholds = np.linspace(0, 1, 100)
    f1_scores = []
    for threshold in thresholds:
        y_pred = (y_score >= threshold).astype(int)
        f1_scores.append(f1_score(y_true, y_pred))
    return thresholds, f1_scores

def precision_recall_confidence_curve(y_true, y_score):
    precision, recall, thresholds = precision_recall_curve(y_true, y_score)
    pr_auc = auc(recall, precision)
    return recall, precision, thresholds, pr_auc

# Example usage
y_true = np.array([0, 1, 1, 0, 1])
y_score = np.array([0.1, 0.8, 0.6, 0.3, 0.7])  # Example predicted probabilities

# Compute F1 confidence curve
thresholds_f1, f1_scores = f1_confidence_curve(y_true, y_score)

# Plot F1 confidence curve
plt.plot(thresholds_f1, f1_scores)
plt.xlabel('Threshold')
plt.ylabel('F1 Score')
plt.title('F1 Confidence Curve')
plt.grid(True)
plt.show()

# Compute precision-recall confidence curve
recall, precision, thresholds_pr, pr_auc = precision_recall_confidence_curve(y_true, y_score)

# Plot precision-recall curve
plt.plot(recall, precision)
plt.xlabel('Recall')
plt.ylabel('Precision')
plt.title(f'Precision-Recall Curve (AUC = {pr_auc:.3f})')
plt.grid(True)
plt.show()
# Save the trained model
torch.save(model.state_dict(), '/content/drive/My Drive/fracture/trained_fcrnn.pth')


