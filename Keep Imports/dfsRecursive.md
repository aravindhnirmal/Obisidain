[[Keep/Colour/DEFAULT]] [[Keep/Archived]] 

class Node:
    def __init__(self, key):
        self.data = key
        self.left = None
        self.right = None

def dfsRecursive(root):
    if root:
        print(root.data, end=" ")  # Visit the current node
        dfsRecursive(root.left)    # Recur on the left subtree
        dfsRecursive(root.right)   # Recur on the right subtree

# Driver program to test the function
if __name__ == '__main__':
    root = Node(1)
    root.left = Node(2)
    root.right = Node(3)
    root.left.left = Node(4)
    root.left.right = Node(5)

    print("DFS Recursive traversal of binary tree:")
    dfsRecursive(root)

