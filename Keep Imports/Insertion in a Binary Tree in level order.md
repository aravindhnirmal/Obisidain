[[Keep/Colour/DEFAULT]] [[Keep/Archived]] 

class TreeNode:
    def __init__(self, data):
        self.key = data
        self.left = None
        self.right = None

def inorder(temp):
    if not temp:
        return
    inorder(temp.left)
    print(temp.key, end=" ")
    inorder(temp.right)

def insert(temp, key):
    if not temp:
        return TreeNode(key)

    q = [temp]

    while q:
        temp = q.pop(0)

        if not temp.left:
            temp.left = TreeNode(key)
            break
        else:
            q.append(temp.left)

        if not temp.right:
            temp.right = TreeNode(key)
            break
        else:
            q.append(temp.right)

if __name__ == '__main__':
    root = TreeNode(10)
    root.left = TreeNode(11)
    root.left.left = TreeNode(7)
    root.right = TreeNode(9)
    root.right.left = TreeNode(15)
    root.right.right = TreeNode(8)

    print("Inorder traversal before insertion:", end=" ")
    inorder(root)

    key = 12
    root = insert(root, key)

    print()
    print("Inorder traversal after insertion:", end=" ")
    inorder(root)






































\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\










class TreeNode:
    def __init__(self, key):
        self.left = None
        self.right = None
        self.val = key

def insert_level_order(root, key):
    if not root:
        return TreeNode(key)  # If the tree is empty, create the root node.

    queue = [root]

    while queue:
        node = queue.pop(0)

        if not node.left:
            node.left = TreeNode(key)
            return root  # Inserted successfully

        if not node.right:
            node.right = TreeNode(key)
            return root  # Inserted successfully

        queue.append(node.left)
        queue.append(node.right)

# Function to perform an inorder traversal for testing
def inorder_traversal(root):
    if root:
        inorder_traversal(root.left)
        print(root.val, end=" ")
        inorder_traversal(root.right)

# Example usage:
if __name__ == "__main__":
    root = TreeNode(1)  # Create the root node with value 1
    insert_level_order(root, 2)
    insert_level_order(root, 3)
    insert_level_order(root, 4)
    insert_level_order(root, 5)

    print("Inorder Traversal after Insertion:")
    inorder_traversal(root)

