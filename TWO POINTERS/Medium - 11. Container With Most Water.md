You are given an integer array height of length n. There are n vertical lines drawn such that the two endpoints of the ith line are (i, 0) and (i, height[i]).

Find two lines that together with the x-axis form a container, such that the container contains the most water.

Return the maximum amount of water a container can store. Notice that you may not slant the container.

<img width="313" alt="image" src="https://github.com/swethamurthy25/My-LeetCode/assets/112581595/3874afbb-2726-49f6-8213-5b406b063cd0">

____________________________________________________________________________________________________________

### Understanding of the question:

1. We are given the input array height - which contains the height of each vertical line
2. We need to find the maximum area of the container that can be formed with these vertices which holds the maximum water.
3. Now how do we form a container? -- Basically, a container looks like a triangle which has the length and width
4. So the x-axis from 0 to len(heights) can be used to calculate width (i.e.) the width of any container will be the difference between the index of the two lines (i and j),
5. The y-axis values (height array) are used to calculate height (i.e.) the height will be whichever of the two sides is the lowest (min(H[i], H[j])).
6. The first thing we should realize is that the amount of water contained is always going to be a rectangle whose area is defined as length * width.

Youtube Reference: https://www.youtube.com/watch?v=UuiTKBwPgAo
___________________________________________________________________________________________________________________

### Brute Force Approach:

1. The brute force approach would be to compare every single pair of indexes in H or try every possible combination of width and height to get the area.
2. Find the max value among those areas.

TC is O(n^2) since we are trying all possible combinations and SC is O(1)

1. maxarea = 0: Initialize a variable maxarea to store the maximum area of the container. This is initially set to 0.
2. The code uses a nested loop to iterate through all possible pairs of bars to form containers. It uses two loops:
3. For left in range(len(height)): The outer loop iterates through each bar in the height list, considering it as the left bar of the container.
4. For right in range(left + 1, len(height)): The inner loop iterates through each bar to the right of the current left bar. This ensures that the right bar is always to 
   the right of the left bar.
5. Width = right - left: Calculate the width of the container by subtracting the index of the left bar from the index of the right bar.
6. hght = min(height[left], height[right]): Calculate the height of the container by taking the minimum of the heights of the left and right bars. The minimum height 
   determines how tall the container can be.
7. curr_area = width * hght: Calculate the current area of the container by multiplying the width and height.
8. maxarea = max(maxarea, curr_area): Update the maxarea with the maximum of its current value and the curr_area. This step ensures that max area always stores the maximum 
   area found so far.
9. After the nested loops have finished, the method returns the max area, which represents the maximum area of a container that can be formed by the given set of bars.

```python
class Solution:
    def maxArea(self, height: List[int]) -> int:
        #Brute force - trying all combinations to find the max area
        maxarea = 0
        for left in range(len(height)):
            for right in range(left + 1, len(height)):
                width = right - left
                hght = min(height[left], height[right])
                curr_area = width * hght
                maxarea = max(maxarea,curr_area)

        return maxarea
```
_____________________________________________________________________________________________________________________________________

### Optimized Solution using TWO POINTER Approach:

It's clear that we need to make a 2-pointer sliding window solution. We'll start from either end and at each step we'll check the container area, then we'll shift 
the lower-valued pointer inward. Once the two pointers meet, we know that we must have exhausted all possible containers and we should return our answer (maxArea).

TC is O(N) as we are iterating only once by using two pointers and SC is O(1)

1. `maxArea = 0`: Initialize a variable `maxArea` to store the maximum area of the container. This is initially set to 0.
2. `left, right = 0, len(height)-1`: Initialize two pointers, `left` and `right`, to the first and last bars in the `height` list. These pointers will be used to form     
    containers by considering bars between them.
3. `while left < right:`: Enter a `while` loop that continues as long as the `left` pointer is less than the `right` pointer. This loop will iterate through the bars from 
    both ends towards the center.
4. `width = (right-left)`: Calculate the width of the container by subtracting the index of the `left` bar from the index of the `right` bar. This width represents the 
    distance between the two pointers.
5. `hght = min(height[left], height[right])`: Calculate the height of the container by taking the minimum of the heights of the `left` and `right` bars. The minimum height 
    determines how tall the container can be.
6. `curr_area = width * hght`: Calculate the current area of the container by multiplying the width and height.
7. `maxArea = max(maxArea, curr_area)`: Update the `maxArea` with the maximum of its current value and the `curr_area`. This step ensures that `maxArea` always stores the 
    the maximum area found so far.

```python
lass Solution:
    def maxArea(self, height: List[int]) -> int:
        #Two Pointer approach
        maxArea = 0
        left, right = 0, len(height)-1
        while left < right:
            width = (right-left)
            hght = min(height[left], height[right])
            curr_area = width * hght
            maxArea = max(maxArea, curr_area)
            
            #Shifting the pointers
            if height[left] < height[right]:
                left += 1
            else:
                right -= 1
        return maxArea
```
______________________________________________________________________________________________________________________________________________

9. `if height[left] < height[right]:`: Check if the height of the `left` bar is less than the height of the `right` bar. If so, it means that moving the `left` pointer towards the right might result in a larger container because it would increase the width while maintaining the height. Therefore, increment the `left` pointer (`left += 1`).

10. `else:`: If the height of the `right` bar is less than or equal to the height of the `left` bar, it means that moving the `right` pointer towards the left might result in a larger container. Therefore, decrement the `right` pointer (`right -= 1`).

11. Repeat steps 4 to 9 in the `while` loop until the `left` pointer is no longer less than the `right` pointer.

12. After the `while` loop has finished, the method returns `maxArea`, which represents the maximum area of a container that can be formed by the given set of bars.

This code efficiently solves the problem of finding the maximum area of a container formed by the bars using a two-pointer approach with a time complexity of O(n), where n is the number of bars.


