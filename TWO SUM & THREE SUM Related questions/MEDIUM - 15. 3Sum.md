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
3. For every index and value in the input array, we need to check whether the current value and its previous value are the same. If it's the same, it is
   a duplicate value, so we can just simply continue with the steps (we do not want to reuse the same element)
5. Now initialize two pointers - left should point to index +1 and right to len(nums)-1 and follow the two-pointer approach
6. If the summation of three numbers is equal to 0 , append the same to the results array and return the result array

TC is O(n log n) + (n^2) which is asymptotically equal to O(n^2) 
SC IS O(n)

  # Sorting and two pointer approach
        result = []
        nums.sort()
        
        for i,a in enumerate(nums):
            if i > 0 and a == nums[i-1]:
                continue
                
            left , right = i+1 , len(nums)-1
            while left < right:
                threeSum = a + nums[left] + nums[right]
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
_________________________________________________________________________________


