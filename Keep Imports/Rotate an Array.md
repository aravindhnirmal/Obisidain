[[Keep/Colour/DEFAULT]] [[Keep/Archived]] 

class Solution:
    def rotate(self, nums, k):
        n = len(nums)
        
        # Calculate effective number of rotations
        k = k % n
        
        # Reverse the entire array
        nums.reverse()
        
        # Reverse the first k elements
        nums[:k] = reversed(nums[:k])
        
        # Reverse the remaining elements
        nums[k:] = reversed(nums[k:])

