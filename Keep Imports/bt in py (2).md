[[Keep/Colour/DEFAULT]] 

https://chat.openai.com/c/92cc95f9-2c74-4abb-a0a4-d07f685ceb5a

class TreeNode:
    def __init__(self, data):
        self.data = data
        self.left = None
        self.right = None

class BinaryTree:
    def __init__(self):
        self.root = None

    def insert(self, data):
        if self.root is None:
            self.root = TreeNode(data)
        else:
            self._insert_recursively(self.root, data)

    def _insert_recursively(self, node, data):
        if data < node.data:
            if node.left is None:
                node.left = TreeNode(data)
            else:
                self._insert_recursively(node.left, data)
        elif data > node.data:
            if node.right is None:
                node.right = TreeNode(data)
            else:
                self._insert_recursively(node.right, data)

# Example usage:
tree = BinaryTree()
tree.insert(5)
tree.insert(3)
tree.insert(8)
tree.insert(1)
tree.insert(4)
tree.insert(7)
tree.insert(9)

