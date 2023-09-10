You have a long flowerbed in which some of the plots are planted, and some are not. However, flowers cannot be planted in adjacent plots.

Given an integer array flowerbed containing 0's and 1's, where 0 means empty and 1 means not empty, and an integer n, return true if n new flowers can be planted in the 
flowerbed without violating the no-adjacent-flowers rule and false otherwise.

Input: flowerbed = [1,0,0,0,1], n = 1

Output: true 

Input: flowerbed = [1,0,0,0,1], n = 2

Output: false
_______________________________________________________________________________________________________________________________________

#### Approach 1:

1. We can traverse over all the elements of the flowerbed and find out those elements which are 0(implying an empty position).
2. For every such element, we check if both adjacent positions are also empty.
3. If so, we can plant a flower at its current position without violating the no-adjacent-flowers rule.
4. Edge case - For the first and last elements, we need not check the previous and the next adjacent positions respectively.
5. Decrement the n count as we do the planting and if n reaches 0 we are end of the process and return True
6. Else return False

##### Left Plot:
* The current plot is the first plot in the flowerbed (i.e., i == 0), indicating that there is no plot to the left.
* The plot to the left of the current plot is empty (i.e., flowerbed[i-1] == 0).

##### Right Plot:
* The current plot is the last plot in the flowerbed (i.e., i == len(flowerbed) - 1), indicating that there is no plot to the right.
* The plot to the right of the current plot is empty (i.e., flowerbed[i+1] == 0).
  
TC is O(n) as we are iterating through all the elements

SC is O(1) as we are not using any extra space or memory.

```python
class Solution:
    def canPlaceFlowers(self, flowerbed: List[int], n: int) -> bool:
        #Approach 1 - TC is O(n) and SC is O(1)
        if n == 0: return True
        for i in range(len(flowerbed)):
            if flowerbed[i] == 0:
                left_plot = (i==0) or flowerbed[i-1] == 0
                right_plot = (i == len(flowerbed)-1) or (flowerbed[i+1]==0)
                if left_plot and right_plot:
                    flowerbed[i] = 1
                    n -= 1
                    if n == 0: return True
        return False
```
________________________________________________________________________________________________________________

#### Approach 2:

1. It starts by creating a new list f. This list is constructed by adding a 0 at the beginning and end of the flowerbed list.
2. This is done to simplify the boundary conditions when checking adjacent plots. So, f contains the original flowerbed with additional 0s at both ends.
3. The loop then iterates through the f list from index 1 to the length of the original flowerbed plus 1.
4. This loop allows us to consider each plot in the flowerbed, including the additional 0s at the boundaries.
5. Inside the loop, it checks if the current plot and its adjacent plots (previous and next) are all empty.
6. In other words, it checks if f[i-1], f[i], and f[i+1] are all equal to 0.
7. If all three conditions are met, it means that the current plot can be used to plant a new flower without violating the adjacent plot constraints.
8. So, it sets f[i] to 1 (indicating a planted flower) and decrements n by 1 (since one flower has been planted).
9. After planting a flower, it checks if n has become less than or equal to 0.
10. If n is less than or equal to 0, it returns True because it means that all required flowers have been planted.
11. If the loop completes without planting all the required flowers (i.e., n is still greater than 0), the method returns False because it's not possible to plant all n flowers without violating the adjacent plot constraints.

```python
class Solution:
    def canPlaceFlowers(self, flowerbed: List[int], n: int) -> bool:
        #Approach 2 
        f = [0] + flowerbed + [0]
        #Skipping the first & last element of the array since we added it
        for i in range(1,len(flowerbed)+1):
            if f[i-1] == 0 and f[i] == 0 and f[i+1]==0:
                f[i] = 1
                n -= 1
            if n <= 0: return True
        return False
```

_____________________________________________________________________________________________________________________________________________








 
