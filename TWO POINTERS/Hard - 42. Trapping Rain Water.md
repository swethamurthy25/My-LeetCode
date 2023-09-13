Given n non-negative integers representing an elevation map where the width of each bar is 1, compute how much water it can trap after rain.

<img width="444" alt="image" src="https://github.com/swethamurthy25/My-LeetCode/assets/112581595/07eeeb61-6e88-45e3-a6c0-40169cbaa9c7">

____________________________________________________________________________________________________________________________________________________

### Understanding of the Question:

1. In the given image, the height array (input) represents the height of the bars.
2. Now we need to compute the amount of water it can trap/store after the rain. This is quite similar logic of the container with the most water.
3. But we need to find the minimum value here - means the minimum water it can store after the rain.

### Let's solve it manually first to have a better understanding:

height = [0,1,0,2,1,0,1,3,2,1,2,1]

MAX_LEFT_BAR

* We know min value is 0
* We need to calculate the max left bar - which means the max length of the left bar
* max_left = height[0] ie 0
* left_bar = [0,1,1,2,2,2,2,3,3,3,3,3]

MAX_RIGHT_BAR

* max_right = height[-1] ie 1 -- iterating from end
* right_bar = [3,3,3,3,3,3,3,3,2,2,2,1]

MIN_VALUE

* Now we have the length of max left and max right
* Lets calculate the min value now - min(left,right) - height[i]

Video Reference- https://www.youtube.com/watch?v=hI0A_UOgdD8

__________________________________________________________________________________________________________________________________________________________________________

### Brute Force Approach:

TC is O(n^2) as we are using nested for loops and iterating twice. Sc is also O(n) as we are initializing and using two new arrays.

1. `minValue = 0`: Initialize a variable `minValue` to store the total trapped water, initially set to 0.
2. `size = len(height)`: Determine the size of the input height list, which represents the number of bars.
3. Initialize two arrays, `left` and `right`, both filled with zeros. These arrays will be used to store the maximum bar heights to the left and right of each bar.
   The size of both arrays is equal to the number of bars in the input.
5. Calculate `left_max` to keep track of the maximum bar height to the left of the current bar. Initialize it with the height of the first bar (`height[0]`).
6. Iterate through the `height` list from left to right (index `i` ranging from 0 to `size-1`):
   - If the height of the current bar (`height[i]`) is greater than the current `left_max`, update `left_max` to the new maximum height, and store this maximum height
     in the `left` array at the same index `i`.
   - If the height of the current bar is not greater than `left_max`, store the current `left_max` in the `left` array at index `i`.
7. Calculate `right_max` to keep track of the maximum bar height to the right of the current bar. Initialize it with the height of the last bar (`height[-1]`).
8. Iterate through the `height` list from right to left (index `i` ranging from `size-1` to 0, counting down):
   - Similar to the left iteration, if the height of the current bar is greater than the current `right_max`, update `right_max` to the new maximum height, and
     store this maximum height in the `right` array at the same index `i`.
   - If the height of the current bar is not greater than `right_max`, store the current `right_max` in the `right` array at index `i`.
9. The `left` and `right` arrays now contain the maximum heights to the left and right of each bar, respectively. These arrays essentially represent the heights of
   the walls on both sides of each bar.
10. Initialize two pointers (index `i` ranging from 0 to `size-1`) and iterate through the `height` list:
   - Calculate the minimum of `left[i]` and `right[i]`, which represents the height of the shorter wall.
   - Subtract the height of the current bar (`height[i]`) from the calculated minimum wall height.
   - Add this result to the `minValue` variable, accumulating the trapped water.
11. Finally, return the `minValue`, which represents the total amount of trapped rainwater between the bars.

```python
class Solution:
    def trap(self, height: List[int]) -> int:
        #Brute Force
        minValue = 0
        size = len(height)
        #Define left and right array
        left = size*[0]
        right = size*[0]
        
        #left_max
        left_max = height[0]
        for i in range(0,size):
            if left_max < height[i]:
                left_max = height[i]
                left[i] = left_max
            else:
                left[i] = left_max

        #right_max - iterate from the end of the array
        right_max = height[-1]
        for i in range(size-1,-1,-1):
            if right_max < height[i]:
                right_max = height[i]
                right[i] = right_max
            else:
                right[i] = right_max
        print(left)
        print(right)

        for i in range(0,size):
            minValue += min(left[i],right[i]) - height[i]
        return minValue
```

<img width="482" alt="image" src="https://github.com/swethamurthy25/My-LeetCode/assets/112581595/9e8d69b1-5bbf-40ee-b97c-469daf90cc49">

_____________________________________________________________________________________________________________________________________
