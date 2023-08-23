
Given an array of integer nums and an integer target, return indices of the two numbers such that they add up to the target. 
You may assume that each input would have exactly one solution, and you may not use the same element twice.
You can return the answer in any order.

Input : nums = [2,7,11,15]                   
Output: target = 9

Approach1: Brute Force Method
1. Run two loops and check for every combination in the given array.
2. Fix the outer loop at a specific index and move the inner loop to get all the possible pairs.
3. If nums[outerLoopIndex] + nums[innerLoopIndex] is equal to target, return {outerLoopIndex, innerLoopIndex}  as result. Else continue iteration to check for the next pair.
4. Repeat the above steps until you find a combination that adds up to the given target.

```python
Class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        # Brute Force Method
        for i in range(len(nums)):
            for j in range(i+1 , len(nums)):
                if nums[j] == target – nums[i]:
                    return [i, j]
```

Time Complexity of first for loop – O(n) and Time Complexity of second for loop – O(n)

Total time – O(n^2)

Space Complexity – O(1)

***************************************************************************************************

DATA STRUCTURE USED: HASHTABLE

Approach 2: One-pass Hash Table: 

1. While we are iterating and inserting elements into the hash table, we also look back to check if the current element's complement already exists in the hash table. 
2. If it exists, we have found a solution and return the indices immediately.

 Time - O(n) and 
 Space - O(n)

```python
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        # Using One-pass Hash table & Enumerate function
        # Create a hashmap to store the result
        # for every number and its index in nums, if target-nums is present in the result
        # return its indices, else store the value to hashmap
        
        result = {}
        for i , num in enumerate(nums):
            if target-num in result:
                return([result[target-num], i])
            else:
                result[num] = i 
```

Another Approach:

```python
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        # Using dictionary/hash table
        # i, x = index and its number
        
        dict = {}
        for i in range(len(nums)):
            print(nums[i])
            result = target - nums[i]
            if result in dict:
                return [i, dict[result]]
            else:
                dict[nums[i]] = i
```
            
***************************************************************************
 
 Another Approach using Pointers: 
 
 But this will not work for all the integer pairs and we need to sort the array. Sorting will lead to O(n log n) complexity.

 ```python
  #Using Two Pointers - O(n) and O(1)
        n = len(nums)
        i = 0
        j = n-1
        
        while i < j:
            if nums[i]+nums[j] == target:
                return [i,j]
            elif nums[i]+nums[j] < target:
                i += 1
            else:
                j -= 1
                
        return []
 ```    
 ************************************END********************************************