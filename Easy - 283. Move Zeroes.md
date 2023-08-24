Given an integer array nums, move all 0s to the end of it while maintaining the relative order of the non-zero elements.

Note that you must do this in place without making a copy of the array.

Input: nums = [0,1,0,3,12]

Output: [1,3,12,0,0]

Input: nums = [0]

Output: [0]

Follow-up: Could you minimize the total number of operations done?
_________________________________________________________________________________________________

Understanding of the question:
1. We need to move all the zeros to the end of the list, these operations should be in place without
   using the additional array.
3. There is an edge case given as an example test case, if nums is 0, we need to return 0
4. If we encounter the non-zero elements just swap the numbers with its nearby element.
__________________________________________________________________________________________________________

#### Solution using Two pointer

1. i and j are two pointers that will be used to traverse the list.
2. The loop iterates through each index j in the range of the length of nums. This loop will examine each
   element in the list.
3. The if nums[j] != 0: condition checks if the current element at index j is not equal to 0.
4. If the element is not zero, it means we've found a non-zero element.
5. The code swaps the element at index i (which is guaranteed to be a zero) with the element at index j (which is a non-zero).
6. This swap essentially moves the non-zero element to the front of the array, preserving the order of non-zero elements.
7. After the swap i is incremented by 1

TC is O(n) and SC is O(1)

```python
class Solution:
    def moveZeroes(self, nums: List[int]) -> None:
        """
        Do not return anything, modify nums in-place instead.
        """
        if nums == 0: return 0
        i = 0
        for j in range(len(nums)):
            if nums[j] != 0:
                nums[i], nums[j] = nums[j], nums[i]
                i += 1
```



