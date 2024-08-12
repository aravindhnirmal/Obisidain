[[Keep/Colour/DEFAULT]] [[Keep/Archived]] 

class Node:
    def __init__(self, data):
        self.data = data
        self.next = None

class LinkedList:
    def __init__(self):
        self.head = None

    def traverse(self):
        if self.head is None:
            print("List is empty")
        else:
            current = self.head
            while current is not None:
                print(current.data, end=" ")
                current = current.next
            print()

    def insert_at_position(self, position, data):
        new_node = Node(data)

        if position == 0:
            new_node.next = self.head
            self.head = new_node
        else:
            current = self.head
            count = 0
            while current is not None and count < position - 1:
                current = current.next
                count += 1

            if current is None:
                print("Invalid position")
            else:
                new_node.next = current.next
                current.next = new_node

    def delete_at_position(self, position):
        if self.head is None:
            print("List is empty")
        elif position == 0:
            self.head = self.head.next
        else:
            current = self.head
            count = 0
            while current is not None and count < position - 1:
                current = current.next
                count += 1

            if current is None or current.next is None:
                print("Invalid position")
            else:
                current.next = current.next.next

# Usage example
my_list = LinkedList()

my_list.insert_at_position(0, 10)
my_list.insert_at_position(1, 20)
my_list.insert_at_position(2, 30)

my_list.traverse()  # Output: 10 20 30

my_list.delete_at_position(1)

my_list.traverse()  # Output: 10 30

