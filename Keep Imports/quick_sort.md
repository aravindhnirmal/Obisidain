[[Keep/Colour/DEFAULT]] [[Keep/Archived]] 

def quick_sort(arr):
    if len(arr) <= 1:
        return arr  # Base case: If the array has 0 or 1 element, it's already sorted.

    pivot = arr[len(arr) // 2]  # Choose a pivot element (e.g., middle element)
    left = [x for x in arr if x < pivot]  # Elements less than the pivot
    middle = [x for x in arr if x == pivot]  # Elements equal to the pivot
    right = [x for x in arr if x > pivot]  # Elements greater than the pivot

    # Recursively sort left and right subarrays and combine them
    return quick_sort(left) + middle + quick_sort(right)

# Example usage:
arr = [38, 27, 43, 3, 9, 82, 10]
sorted_arr = quick_sort(arr)
print("Sorted array:", sorted_arr)

