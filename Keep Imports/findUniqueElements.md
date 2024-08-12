[[Keep/Colour/DEFAULT]] [[Keep/Archived]] 

def findUniqueElements(matrix):
    frequency = {}  # Dictionary to store the frequency of each element

    # Count the frequency of each element in the matrix
    for row in matrix:
        for element in row:
            if element in frequency:
                frequency[element] += 1
            else:
                frequency[element] = 1

    unique_elements = []

    # Find unique elements with frequency 1
    for row in matrix:
        for element in row:
            if frequency[element] == 1:
                unique_elements.append(element)

    return unique_elements

# Example usage:
matrix1 = [
    [20, 15, 30, 2],
    [2, 3, 5, 30],
    [6, 7, 6, 8]
]

matrix2 = [
    [1, 2, 3],
    [5, 6, 2],
    [1, 3, 5],
    [6, 2, 2]
]

unique_elements1 = findUniqueElements(matrix1)
if unique_elements1:
    print("Unique elements in matrix1:", unique_elements1)
else:
    print("No unique element in matrix1")

unique_elements2 = findUniqueElements(matrix2)
if unique_elements2:
    print("Unique elements in matrix2:", unique_elements2)
else:
    print("No unique element in matrix2")

