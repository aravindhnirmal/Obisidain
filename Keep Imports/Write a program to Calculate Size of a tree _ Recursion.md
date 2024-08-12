[[Keep/Colour/DEFAULT]] [[Keep/Archived]] 

class Node:
    def __init__(self, key):
        self.data = key
        self.left = None
        self.right = None

def sizeOfTree(root):
    if root is None:
        return 0
    else:
        # Recursively calculate the size of the left and right subtrees
        left_size = sizeOfTree(root.left)
        right_size = sizeOfTree(root.right)
        
        # The size of the tree is the sum of the sizes of its subtrees plus 1 (for the root node)
        return left_size + right_size + 1

# Driver program to test the function
if __name__ == '__main__':
    root = Node(1)
    root.left = Node(2)
    root.right = Node(3)
    root.left.left = Node(4)
    root.left.right = Node(5)

    tree_size = sizeOfTree(root)
    print("Size of the binary tree is:", tree_size)

