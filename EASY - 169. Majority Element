Given an array nums of size n, return the majority element.
The majority element is the element that appears more than ⌊n / 2⌋ times. You may assume that the majority element always exists in the array.

Example:
Input: nums = [3,2,3]
Output: 3

Input: nums = [2,2,1,1,1,2,2]
Output: 2

Constraints:
n == nums.length
1 <= n <= 5 * 104
-109 <= nums[i] <= 109
 
Follow-up: Could you solve the problem in linear time and in O(1) space?
________________________________________________________________________________________

Straight forward solution:
- To count the number of occurances of each number using hashmap
- Return the number whose count exceeds n//2

Solution 1:
class Solution:
    def majorityElement(self, nums: List[int]) -> int:
        
        count={}
        for i in nums:
            if i not in count:
                count[i] = 1
            else:
                count[i] += 1
        max_count = max(count,key=count.get)
        return max_count      
        
 Solution 2:
 class Solution:
    def majorityElement(self, nums: List[int]) -> int:
        
        count={}
        for i in nums:
            if i not in count:
                count[i] = 1
            else:
                count[i] += 1
        if count[i] > len(nums)//2:
              return i
              
The time complexity of the provided code is O(n), where n is the length of the input list nums.
The space complexity of the code is O(n) as well.
In the worst case, when all elements in nums are distinct, the count dictionary will store n key-value pairs, where n is the length of the nums list. 
Therefore, the space required is proportional to the size of the input list.
______________________________________________________________________________________________________

But in the follow up - we need to solve this using linear time o(n) and o(1) space:

So to achieve this we need to eleminate hashmap datastructure and need to use Boyer-Moore's algorithm

The Boyer-Moore algorithm is primarily known for its application in efficient string searching, but it can also be adapted and used in various other data structure-related 
problems.  the Boyer-Moore algorithm can be used to find the majority element in an array. By adapting the algorithm to maintain a candidate element and a count, 
it is possible to efficiently identify the majority element in linear time.

The Boyer-Moore algorithm can be extended to perform pattern matching in trees and graphs efficiently.

class Solution:
    def majorityElement(self, nums: List[int]) -> int:
        result , count = 0,0
        for i in nums:
            if count == 0:
                result = i
            count += (1 if i == result else -1)
        return result

TC is o(n)
SC is O(1)
______________________________________________________________________________________________________________________________











