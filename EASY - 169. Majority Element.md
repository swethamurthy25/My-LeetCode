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
- To count the number of occurrences of each number using a hashmap
- Return the number whose count exceeds n//2

Solution 1:
```python
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
```
     
 Solution 2:
 ```python
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
 ```

The time complexity of the provided code is O(n), where n is the length of the input list numbers.

The space complexity of the code is O(n) as well.
In the worst case, when all elements in nums are distinct, the count dictionary will store n key-value pairs, where n is the length of the nums list. 

Therefore, the space required is proportional to the size of the input list.
______________________________________________________________________________________________________

### But in the follow-up - we need to solve this using linear time o(n) and o(1) space:

So to achieve this we need to eliminate the hashmap data structure and use Boyer-Moore's algorithm.

The Boyer-Moore algorithm is primarily known for its application in efficient string searching, but it can also be adapted and used in various other data structure-related problems.  The Boyer-Moore algorithm can be used to find the majority element in an array. By adapting the algorithm to maintain a candidate element and a count, it is possible to efficiently identify the majority element in linear time.

The Boyer-Moore algorithm can be extended to perform pattern matching in trees and graphs efficiently.

1. The result and count are initialized to 0. The result will store the potential majority element, and the count will keep track of 
   its count.
2. The code iterates through the elements in the nums list using a for loop.
3. During the first iteration, the count will be 0. If the count is indeed 0, the result is updated to the current element i.
4. This element is considered a potential majority element at this point.
5. From the second iteration,  If i is equal to the result, the count is incremented by 1; otherwise, the count is decremented by 1.
6. We will do this process until we reach count == 0 again. In this case, we cannot decrease to -1 further.
7. So we need to update/change the result (majority) element.
8. Finally, after processing all elements in the list, the code returns the result, which should contain the majority of elements.

The Boyer-Moore Majority Vote Algorithm works because if there is a majority element in the list (an element that occurs more than n/2 times), it will survive the cancellation process and end up as the final result in the result variable. 

```python
class Solution:
    def majorityElement(self, nums: List[int]) -> int:
        #Using Boyer Moore Algorithm
        result,count = 0,0
        for i in nums:
            if count == 0:
                result = i
            count += (1 if i == result else -1)
        return result
```

TC is o(n)
SC is O(1)
______________________________________________________________________________________________________________________________











