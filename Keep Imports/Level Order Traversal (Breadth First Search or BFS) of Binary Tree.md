[[Keep/Colour/DEFAULT]] [[Keep/Archived]] 

# A node structure
class Node:
    def __init__(self, key):
        self.data = key
        self.left = None
        self.right = None

# Function to print level order traversal of tree
def printLevelOrder(root):
    if root is None:
        return
    
    # Create an empty queue for level-order traversal
    queue = []
    
    # Enqueue the root node
    queue.append(root)

    while queue:
        # Dequeue the front node
        node = queue.pop(0)
        print(node.data, end=" ")  # Print the data of the dequeued node

        # Enqueue the left child
        if node.left:
            queue.append(node.left)

        # Enqueue the right child
        if node.right:
            queue.append(node.right)

# Driver program to test above function
if __name__ == '__main__':
    root = Node(1)
    root.left = Node(2)
    root.right = Node(3)
    root.left.left = Node(4)
    root.left.right = Node(5)

    print("Level order traversal of binary tree is -")
    printLevelOrder(root)

