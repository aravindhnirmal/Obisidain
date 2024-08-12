[[Keep/Colour/DEFAULT]] [[Keep/Archived]] 

class Stack:
    def __init__(self):
        self.items = []

    def push(self, item):
        self.items.append(item)

    def pop(self):
        if not self.is_empty():
            return self.items.pop()
        else:
            raise IndexError("Stack is empty")

    def peek(self):
        if not self.is_empty():
            return self.items[-1]
        else:
            raise IndexError("Stack is empty")

    def is_empty(self):
        return len(self.items) == 0

    def size(self):
        return len(self.items)

# Example usage
stack = Stack()
stack.push(5)
stack.push(10)
stack.push(15)

print(stack.pop())  # Output: 15
print(stack.peek())  # Output: 10
print(stack.size())  # Output: 2
print(stack.is_empty())  # Output: False

