Given an integer array nums, return all the triplets [nums[i], nums[j], nums[k]] such that i != j, i != k, and j != k, 
and nums[i] + nums[j] + nums[k] == 0. Notice that the solution set must not contain duplicate triplets.


Input: nums = [-1,0,1,2,-1,-4]
Output: [[-1,-1,2],[-1,0,1]]
Explanation: 
nums[0] + nums[1] + nums[2] = (-1) + 0 + 1 = 0.
nums[1] + nums[2] + nums[4] = 0 + 1 + (-1) = 0.
nums[0] + nums[3] + nums[4] = (-1) + 2 + (-1) = 0.
The distinct triplets are [-1,0,1] and [-1,-1,2].
Notice that the order of the output and the order of the triplets does not matter.

Input: nums = [0,1,1]
Output: []
Explanation: The only possible triplet does not sum up to 0.

Input: nums = [0,0,0]
Output: [[0,0,0]]
Explanation: The only possible triplet sums up to 0.

______________________________________________________________________________________

#### Understanding of the Question:
1. We are given with input array and we need to find a possible combination of 3 numbers summing up to 0
2. Return nums[i,j,k] as output, and the outputs should not contain duplicates.
3. Make sure that i != j, i != k, and j != k


#### Approach 1: Brute Force (Time Limit Exceeded)

1. Search for all possible combinations within nums. Use a nested for-loops for nums[i] , nums[j] and nums[k]
2. Before we search for all the combinations, we'll need to understand how to detect & avoid pushing duplicate combinations into the returning list (result)
3. Example: [-1, 0, 1] is a duplicate combination of [-1, 1, 0] because it contains the same elements (-1, 0, and 1)
4. To avoid duplicates - sort nums in ascending/descending order and this will cost O(n log n)
5. Usage of set() function to avoid the duplicates.

TC is O(n log n + n^3) which is asymptotically equal to O(n^3)
SC is O(n)

```python
class Solution:
    def threeSum(self, nums: List[int]) -> List[List[int]]:
        result = []
        nums = sorted(nums)
        setss = set()
        for i in range(len(nums)):
            for j in range(i+1,len(nums)):
                for k in range(j+1,len(nums)):
                    a , b, c = nums[i] , nums[j], nums[k]w
                    if a+b+c == 0 and (a,b,c) not in setss:
                        result.append([a,b,c])
                        setss.add((a,b,c))
        return result
 ```       
_____________________________________________________

#### Approach 2: Using sorting and two pointer 

1. Initialize the result array that we need to return as output
2. Sort the input array
3. For every index and value in the input array, we need to check whether the current value and its previous value are the same.
4. If i > 0 and a == nums[i-1]: continue: This condition checks if the current element a is a duplicate (same value as the previous element), and
   if the current index i is greater than 0. If these conditions are met, it means that we've already considered this value and its triplets in a previous
   iteration, so we skip this iteration.
5. Two pointers (left and right) are initialized to point to the elements right after the current element a (index+1) and at the end of the array, respectively
7. threeSum = a + nums[left] + nums[right]: The sum of the current element a and the elements pointed to by left and right pointers is calculated.

Depending on the value of threeSum, the pointers are adjusted:
8. If threeSum is greater than 0, it means the sum is too large. Thus, the right pointer is moved one step to the left: right -= 1.
9. If threeSum is less than 0, it means the sum is too small. Thus, the left pointer is moved one step to the right: left += 1.
10. If threeSum is equal to 0, it means a valid triplet has been found. The triplet [a, nums [left], nums[right]] is appended to the result list.
11. After appending, the left pointer is incremented and any duplicate elements are skipped using an inner while loop that checks nums[left] == nums[left-1]

12. After the inner while loop completes, the outer while loop continues searching for more valid triplets with the current element a.
13. The final result list contains all the unique triplets that sum up to zero.

TC is O(n log n) + (n^2) which is asymptotically equal to O(n^2) 
SC IS O(n)

```python
class Solution:
    def threeSum(self, nums: List[int]) -> List[List[int]]:
        #Optimized sol using Sorting + Two pointer approach
        #TC is O(n^2) and SC is O(1)
        nums.sort()
        result = []
        for index,a in enumerate(nums):
            if index>0 and a == nums[index-1]:
                continue

            left , right = index+1, len(nums)-1
            while left < right:
                threeSum = a + nums[left]+ nums[right]
                if threeSum > 0:
                    right -= 1
                elif threeSum < 0:
                    left += 1
                else:
                    result.append([a,nums[left],nums[right]])
                    left += 1
                    while nums[left] == nums[left-1] and left < right:
                        left += 1
        return result
```

_________________________________________________________________________________


