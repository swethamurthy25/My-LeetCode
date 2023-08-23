
Given an integer array nums sorted in non-decreasing order, remove the duplicates in-place such that each unique element appears only once. The relative order of the elements 
should be kept the same. Then return the number of unique elements in nums.

Consider the number of unique elements of nums to be k, to get accepted, you need to do the following things:
- Change the array nums such that the first k elements of nums contain the unique elements in the order they were present in nums initially. 
- The remaining elements of nums are not important as well as the size of nums.
- Return k.

Input: nums = [1,1,2]
Output: 2, nums = [1,2,_]
Explanation: Your function should return k = 2, with the first two elements of nums being 1 and 2 respectively.
It does not matter what you leave beyond the returned k (hence they are underscores).

Input: nums = [0,0,1,1,1,2,2,3,3,4]

Output: 5, nums = [0,1,2,3,4,_,_,_,_,_]

Explanation: Your function should return k = 5, with the first five elements of nums being 0, 1, 2, 3, and 4 respectively.
It does not matter what you leave beyond the returned k (hence they are underscores).

Constraints:
1 <= nums.length <= 3 * 104
-100 <= nums[i] <= 100
nums is sorted in non-decreasing order.
____________________________________________________________________________________________________

Understanding of the question:
1. We need to remove the duplicate elements from the nums array
2. The resultant nums array should contain only the unique elements, but removing the duplicate operation should be done in place without creating any additional arrays. [Essence of the que -- unique elements]
3. Return the length of nums as output
__________________________________________________________________________________________
Brute force:
- Using Python inbuild functions sort and set

```python
class Solution:
    def removeDuplicates(self, nums: List[int]) -> int:
        nums[:] = sorted(set(nums))
        return len(nums)
```

Here nums[:] = replaces the element in place.

Time Complexity: O(n) and 
Space Complexity: O(1)
_________________________________________________________________________________________________

Optimized solution using two-pointer approach:

1. left is initialized to 1, which represents the index where the next unique element should be placed in the modified array.
   This is because the first element is considered unique and will always be present.
2. A loop iterates through the array using the right index, starting from the second element (index 1) since we've already
   considered the first element.
3. Inside the loop, the code checks if the current element nums[right] is equal to the previous element nums[right-1].
   If they are equal, it indicates a duplicate.
4. If a duplicate is found, the right index is incremented to skip over all duplicates and point to the next unique element.
5. If the current element is not duplicated, the value at nums[right] is assigned to nums[left], effectively overwriting the
   value at the index left with the unique element.
6. After assigning the unique element, both left and right indices are incremented by 1 to move on to the next position for
   writing a unique element and checking the next element, respectively.
7. This process continues until the loop iterates through the entire array.
8. The function returns the value of left after the loop completes, which represents the length of the modified array without
   duplicates.

   
```python
class Solution:
    def removeDuplicates(self, nums: List[int]) -> int:
        left = 1
        for right in range(1,len(nums)):
            if nums[right] == nums[right-1]:
                right += 1
            else:
                nums[left] = nums[right]
                left += 1
                right += 1
        return left
 ```

 The time complexity of this code is O(n), where n is the length of the input list nums. 
 The code iterates through the list once using the two-pointer approach, comparing adjacent elements. Since the list is already sorted, the duplicates can be 
 detected by comparing adjacent elements. 

The space complexity is O(1) as the modifications are made in-place within the nums list and only a constant amount of additional space is used.
___________________________________________________________________________________________________________


















