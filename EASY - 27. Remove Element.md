
Given an integer array nums and an integer val, remove all occurrences of val in nums in place. The order of the elements may be changed. Then return the number of elements 
in nums which are not equal to val.

Consider the number of elements in nums that are not equal to val be k, to get accepted, you need to do the following things:
- Change the array nums such that the first k elements of nums contain elements that are not equal to val. 
- The remaining elements of nums are not important as well as the size of nums.
- Return k.

Input: nums = [3,2,2,3], val = 3

Output: 2, nums = [2,2,_,_]

Explanation: Your function should return k = 2, with the first two elements of nums being 2.
It does not matter what you leave beyond the returned k (hence they are underscores).

Input: nums = [0,1,2,2,3,0,4,2], val = 2

Output: 5, nums = [0,1,4,0,3,_,_,_]

Explanation: Your function should return k = 5, with the first five elements of nums containing 0, 0, 1, 3, and 4.
Note that the five elements can be returned in any order.
It does not matter what you leave beyond the returned k (hence they are underscores).

Constraints:
0 <= nums.length <= 100
0 <= nums[i] <= 50
0 <= val <= 100
____________________________________________________________________________________________________________________________________________

Understanding of the question:
- We need to remove the val from nums, but the operation should be in-place ie done directly on the nums array
- Return the len(nums) as output
- In place means if you encounter the val, just ignore it and continue iterating to the next element.
- Only swap places if the elements are diff / other than val
__________________________________________________________________

Brute Force:
The while loop iterates until val is found in nums and then removes it using the remove() method. In the worst case, if val occurs multiple times at different positions 
In the list, each removal operation takes O(n) time. 

```python
class Solution:
    def removeElement(self, nums: List[int], val: int) -> int:
        while val in nums:
            nums.remove(val)
        return len(nums)
```
        
 The time complexity of the given code is O(n^2), where n is the length of the input list nums and o(n) time for each removal operation.
 The space complexity of the code is O(1) because the removal is performed in-place, and no additional space is used that grows with the input size. 
 The nums list is modified directly without allocating extra memory.
 _____________________________________________________________________________________
 
 #### Optimized solution:
 - To optimize this code, we should avoid using remove() method as it takes o(n) times for each operation.
 - Instead, we can modify the array in place by swapping elements and by using the two pointer approach
 
 - We can use a two pointer approach that overwrites the first k elements of the array, where k is the number of elements that are not equal to val
 - The index variable i keeps track of the next spot to overwrite in the array, and we use x to check the value of each element and compare it to val.
 - If an element is equal to val, we just move on and don't do anything.
 - Basically, we keep searching until we find an element that is not equal to val. Once we do find an element not equal to val, we write it to the array at index I, 
   then increment i so that it's ready to write at the next spot.
 - At the end, we can just return i since it has been incremented exactly once for each element found that is not equal to val.

 ```python
 class Solution:
    def removeElement(self, nums: List[int], val: int) -> int:
        i = 0
        for x in range(len(nums)):
            if nums[x] != val:
                nums[i] = nums[x]
                i += 1
        return i
 ```

 The time complexity of the given code is O(n), where n is the length of the input list nums. The code iterates through the nums list once using the for loop. 
 Each iteration takes constant time, performing comparisons and assigning values. Therefore, the time complexity is linear with respect to the size of the input.
 
 The space complexity of the code is O(1) because the modifications are made in place within the nums list. The code only uses a constant amount of additional space, 
 regardless of the size of the input list.
 ___________________________________________________________________________
 
 #### Another solution using Two two-pointer

 ```python
class Solution:
    def removeElement(self, nums: List[int], val: int) -> int:
        i = 0
        for j in range(len(nums)):
            if nums[j] == val:
                j += 1
            else:
                nums[i] = nums[j]
                i += 1
                j += 1
        return i
 
____________________________________________________________________________________
 
