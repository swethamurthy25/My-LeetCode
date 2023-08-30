Given a non-empty array of non-negative integers nums, the degree of this array is defined as the maximum frequency of any one of its elements.

Your task is to find the smallest possible length of a (contiguous) subarray of nums, that has the same degree as nums.

Input: nums = [1,2,2,3,1] and Output: 2

Explanation: 

The input array has a degree of 2 because both elements 1 and 2 appear twice. Of the subarrays that have the same degree: [1, 2, 2, 3, 1], [1, 2, 2, 3], 
[2, 2, 3, 1], [1, 2, 2], [2, 2, 3], [2, 2]. The shortest length is 2. So return 2.
__________________________________________________________________________

#### Understanding of the Question:

1. We are given with input nums array and we need to calculate the degree and find the min length of the sub-array
2. Now how do we calculate the degree of an array ??-- The degree of an array refers to the maximum frequency of any element present in the array.
3. This reminds us of the hashtable/dict to keep track of the freq of each element.
4. After getting the max frequency, we need to find the subarray - A subarray is a contiguous subset of elements within an array.
5. Return the minimum length of the sub-array as the output
______________________________________________________________________________________________________

#### Approach 1:

1. count = {}: This initializes an empty dictionary count which will be used to store the frequency (count) of each element in the nums list.
2. Iterate through nums and count the freq of each element
3. maxi_degree = max(count.values()): This calculates the maximum degree (maximum frequency) among all the elements.
4. It retrieves the values (frequencies) from the count dictionary and finds the maximum among them.

5. Start and end dictionaries are used to store the starting and ending indices of each element in the nums list.
6. The second loop iterates through the nums list using both the element and its index (i and num)
7. For each element num, it checks whether num is already a key in the start dictionary.
8. If not, it adds a new key num to the start dictionary with the value of the current index i
9. In any case, it updates the end dictionary with the current index i as the value for the key num.

10. The third loop iterates through the count dictionary to find elements with a frequency equal to maxi_degree.
11. For each such element, it calculates the length of the subarray containing only that element.
12. The length is calculated as the difference between the ending index and the starting index, plus 1.
13. The minimum of these subarray lengths is stored in min_length.
14. Finally, the method returns the calculated min_length, which represents the shortest subarray length with the maximum degree.

```python
class Solution:
    def findShortestSubArray(self, nums: List[int]) -> int:
        count = {}
        for i in nums:
            if i not in count:
                count[i] = 1
            else:
                count[i] += 1
        print(count)

        #Find the max count(degree)
        maxi_degree = max(count.values())
        print(maxi_degree)

        start,end = {},{}
        for i,num in enumerate(nums):
            if num not in start:
                start[num] = i
            end[num] = i
        print(start)
        print(end)

        min_length = float('inf')
        print(min_length)
        for num,freq in count.items():
            if freq == maxi_degree:
                subarray_length = end[num] - start[num]+1
                print(subarray_length)
                min_length = min(min_length,subarray_length)
        return min_length
```

