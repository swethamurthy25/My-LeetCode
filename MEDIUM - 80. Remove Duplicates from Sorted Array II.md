
Given an integer array nums sorted in non-decreasing order, remove some duplicates in place such that each unique element appears at 
most twice. The relative order of the elements should be kept the same.

Since it is impossible to change the length of the array in some languages, you must instead have the result placed in the first part 
of the array nums. More formally, if there are k elements after removing the duplicates, then the first k elements of nums should hold
the final result. It does not matter what you leave beyond the first k elements.

Return k after placing the final result in the first k slots of nums.
Do not allocate extra space for another array. You must do this by modifying the input array in place with O(1) extra memory.

Example 1:

Input: nums = [1,1,1,2,2,3]

Output: 5, nums = [1,1,2,2,3,_]

Explanation: Your function should return k = 5, with the first five elements of nums being 1, 1, 2, 2, and 3 respectively.
It does not matter what you leave beyond the returned k (hence they are underscores).

Example 2:
Input: nums = [0,0,1,1,1,1,2,3,3]

Output: 7, nums = [0,0,1,1,2,3,3,_,_]

Explanation: Your function should return k = 7, with the first seven elements of nums being 0, 0, 1, 1, 2, 3, and 3 respectively.
It does not matter what you leave beyond the returned k (hence they are underscores).

Constraints:
1 <= nums.length <= 3 * 104
-104 <= nums[i] <= 104
nums is sorted in non-decreasing order.
_____________________________________________________________________________________________________________________________________________________________

Understanding of Question:
- We will be given an input array in a sorted manner, we need to remove the duplicates from it.
- We are allowed to have two duplicates, any number more than that has to be removed.
- Only the duplicate is removed in between the array, the remaining rest of the numbers have to be moved forward and the last
  spaces should be left empty.
- We are not allowed to create any additional array or list, we need all these operations in place.

For example:
nums = [1,1,1,2,2,3] - 

Here the nums[i] = 1 has to be removed because it is coming thrice , so when we remove the third 1, 

The array will become like this: [1,1,_,2,2,3]

Now we should move the remaining numbers forward : [1,1,2,2,3,_]
________________________________________________________________________________________________________________________________________________

### Solution

1. The variable i is initialized to 1. This variable will be used as an index to traverse the list.
2. The while loop runs as long as i is less than the length of the nums list minus 1. This is to ensure that there are at least
   three elements left to compare in the consecutive sequence.
3. Inside the loop, an if statement checks whether the current element at index i is the same as both the previous element at index
   i-1 and the next element at index i+1.
4. If this condition is true, it means that three consecutive elements are the same, and the del statement removes the current
   element at index i.
5. If the condition in the if statement is not met, it means that the current element is not part of a sequence of three consecutive
   duplicates. In this case, the index i is incremented to move to the next element.
6. After the loop finishes, the return statement returns the length of the modified nums list, which now has consecutive duplicates
   removed.

#### TC: 
The time complexity of this code can be a bit tricky to analyze due to the deletion operation inside the loop. In the worst case, 
each element might need to be deleted from the list, and for each deletion, the elements after that need to be shifted by one position. 
This involves copying a portion of the list, resulting in an O(n) time complexity for each deletion.

So, TC is O(n^2)

#### SC:
The space complexity of the provided code is O(1) because it doesn't use any extra data structures that grow with the input size.

```python
class Solution:
    def removeDuplicates(self, nums: List[int]) -> int:
        i = 1
        while i < len(nums)-1:
            if nums[i] == nums[i-1] and nums[i] == nums[i+1]:
                del nums[i]
            else:
                i += 1
        return len(nums)
```



