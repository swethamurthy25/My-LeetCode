
Given an array of integer nums and an integer target, return indices of the two numbers such that they add up to the target. 
You may assume that each input would have exactly one solution, and you may not use the same element twice.
You can return the answer in any order.

Input : nums = [2,7,11,15]                   
Output: target = 9

#### Understanding of the question:

1. We are given with input array and the target value
2. We need to check which two elements of the array sum up equal to the target value.
3. Once those two elements are found, we need to return their "indices" as output, not the numbers.
4. The output should be returned in the form of a list/array.
5. We are not allowed to use the same element twice.

   
#### Approach1: Brute Force Method

1. Run two loops and check for every combination in the given array.
2. Fix the outer loop at a specific index and move the inner loop to get all the possible pairs.
3. If nums[i] + nums[j] == target, then return those indices [i,j] as the result.
4. Else continue iteration to check for the next pair.
5. Repeat the above steps until you find a combination matching the target.

```python
Class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        # Brute Force Method
        for i in range(len(nums)):
            for j in range(i+1 , len(nums)):
                if nums[i] + nums[j] == target:
                    return [i, j]
```

Time Complexity of first for loop – O(n) and Time Complexity of second for loop – O(n)

Total time – O(n^2)

Space Complexity – O(1)

***************************************************************************************************

DATA STRUCTURE USED: HASHTABLE

#### Approach 2: One-pass Hash Table: 

1. While iterating and inserting elements into the hash table, we also look back to check if the current element's complement already exists in the hash table. 
2. If it exists, we have found a solution and return the indices immediately.

 Time - O(n) and 
 Space - O(n)

```python
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        # Using One-pass Hash table & Enumerate function
        # Create a hashmap to store the result
        # for every number and its index in nums, if the target is present in the result
        # return its indices, else store the value to hashmap
        
        result = {}
        for i , num in enumerate(nums):
            if target-num in result:
                return([result[target-num], i])
            else:
                result[num] = i 
```

#### Approach 3: Two-pass Hash Table: 

TC is O(n) and SC is O(1)

It iterates through the array, storing encountered numbers in a hashmap along with their indices. If it finds a number such that the required complement 
to reach the target sum that is already in the hashmap, it returns the indices of the two numbers that add up to the target.

1. hashmap = {}: This line initializes an empty dictionary called hashmap.
2. This dictionary will be used to store the numbers from the array as keys and their corresponding indices as values.
3. The for loop iterates through the nums list using the indices of the elements.
4. Inside the for loop check for result = target - nums[i]: Calculate the difference between the target and the current number at index i.
5. This difference (result) represents the value that, if found in the hashmap, would complete the pair to reach the target sum.
6. Then the if-else code is used to check whether the result is already in the hashmap
7. If the result is not in the hashmap, it means that we haven't encountered a number earlier that could be combined with the current number to
   achieve the target sum.
8. So, the current number is added to the hashmap with its index as the value.
9. If the result is already in the hashmap, it means we have already seen a number earlier that, when combined with the current number, would result
    in the target sum.
10. In this case, the function returns a list containing the current index I and the index stored in the hashmap for the result, completing the pair
    that adds up to the 
    target.

```python
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        dict = {}
        for i in range(len(nums)):
            result = target - nums[i]
            if result not in dict:
                dict[nums[i]] = i
            else:
                return [i, dict[result]]
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
