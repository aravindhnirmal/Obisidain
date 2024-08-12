[[Keep/Colour/DEFAULT]] [[Keep/Archived]] 

class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        num_index_map = {}
        
        for index, num in enumerate(nums):
            remaining = target - num
            
            if remaining in num_index_map:
                return [num_index_map[remaining], index]
            
            num_index_map[num] = index
        
        return []

