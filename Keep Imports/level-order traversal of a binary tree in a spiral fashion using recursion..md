[[Keep/Colour/DEFAULT]] [[Keep/Archived]] 

class newNode:
    def __init__(self, key):
        self.data = key
        self.left = None
        self.right = None

def printSpiral(root):
    def height(node):
        if node is None:
            return 0
        else:
            lheight = height(node.left)
            rheight = height(node.right)
            return max(lheight, rheight) + 1

    def printGivenLevel(node, level, ltr):
        if node is None:
            return
        if level == 1:
            print(node.data, end=" ")
        elif level > 1:
            if ltr:
                printGivenLevel(node.left, level - 1, ltr)
                printGivenLevel(node.right, level - 1, ltr)
            else:
                printGivenLevel(node.right, level - 1, ltr)
                printGivenLevel(node.left, level - 1, ltr)

    h = height(root)
    ltr = False  # Initialize left to right as False
    for i in range(1, h + 1):
        printGivenLevel(root, i, ltr)
        ltr = not ltr  # Toggle left to right direction

# Driver Code
if __name__ == '__main__':
    root = newNode(1)
    root.left = newNode(2)
    root.right = newNode(3)
    root.left.left = newNode(7)
    root.left.right = newNode(6)
    root.right.left = newNode(5)
    root.right.right = newNode(4)
    
    print("Spiral Order traversal of binary tree is:")
    printSpiral(root)

