[[Keep/Colour/DEFAULT]] [[Keep/Archived]] 

class Node:
    def __init__(self, data):
        self.data = data
        self.next = None

class LinkedList:
    def __init__(self):
        self.head = None

    def append(self, data):
        new_node = Node(data)
        if not self.head:
            self.head = new_node
            return
        current = self.head
        while current.next:
            current = current.next
        current.next = new_node

    def delete_N_after_M(self, M, N):
        current = self.head

        # Traverse M nodes
        for _ in range(M - 1):
            if current is None:
                return
            current = current.next

        if current is None:
            return

        # Delete N nodes
        temp = current.next
        for _ in range(N):
            if temp is None:
                break
            temp = temp.next

        # Update the next pointer
        current.next = temp

    def display(self):
        current = self.head
        while current:
            print(current.data, end=" -> ")
            current = current.next
        print("None")

# Example usage:
ll = LinkedList()
for data in [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]:
    ll.append(data)

M = 2  # Skip 2 nodes
N = 3  # Delete 3 nodes after each 2 nodes

ll.delete_N_after_M(M, N)
ll.display()

