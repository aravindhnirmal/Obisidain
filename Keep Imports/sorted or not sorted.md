[[Keep/Colour/DEFAULT]] [[Keep/Archived]] 

class Node:
    def __init__(self, data):
        self.data = data
        self.next = None

class LinkedList:
    def __init__(self):
        self.head = None

    def insert_at_end(self, data):
        new_node = Node(data)
        if self.head is None:
            self.head = new_node
        else:
            temp = self.head
            while temp.next:
                temp = temp.next
            temp.next = new_node

    def display(self):
        temp = self.head
        while temp:
            print(temp.data, end=" -> ")
            temp = temp.next
        print("None")

    def is_sorted_iterative(self):
        temp = self.head
        while temp and temp.next:
            if temp.data > temp.next.data:
                return False
            temp = temp.next
        return True

    def is_sorted_recursive(self, current=None):
        if current is None:
            current = self.head
        if current is None or current.next is None:
            return True
        if current.data > current.next.data:
            return False
        return self.is_sorted_recursive(current.next)

# Create a linked list (sorted)
ll_sorted = LinkedList()
ll_sorted.insert_at_end(10)
ll_sorted.insert_at_end(20)
ll_sorted.insert_at_end(30)
ll_sorted.insert_at_end(40)

# Create a linked list (not sorted)
ll_not_sorted = LinkedList()
ll_not_sorted.insert_at_end(10)
ll_not_sorted.insert_at_end(40)
ll_not_sorted.insert_at_end(20)
ll_not_sorted.insert_at_end(30)

# Check if the linked lists are sorted
print("Is ll_sorted sorted:", ll_sorted.is_sorted_iterative())  # or ll_sorted.is_sorted_recursive()
print("Is ll_not_sorted sorted:", ll_not_sorted.is_sorted_iterative())  # or ll_not_sorted.is_sorted_recursive()

