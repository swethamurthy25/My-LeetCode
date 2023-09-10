You have a long flowerbed in which some of the plots are planted, and some are not. However, flowers cannot be planted in adjacent plots.

Given an integer array flowerbed containing 0's and 1's, where 0 means empty and 1 means not empty, and an integer n, return true if n new flowers can be planted in the 
flowerbed without violating the no-adjacent-flowers rule and false otherwise.

Input: flowerbed = [1,0,0,0,1], n = 1

Output: true 

Input: flowerbed = [1,0,0,0,1], n = 2

Output: false
_____________________________________________________________________________________________________________________________________________________

#### Approach 1:

1. We can traverse over all the elements of the flowerbed and find out those elements which are 0(implying an empty position).
2. For every such element, we check if both adjacent positions are also empty.
3. If so, we can plant a flower at the current position without violating the no-adjacent-flowers rule.
4. Edge case - For the first and last elements, we need not check the previous and the next adjacent positions respectively.
5. Decrement the n count as we do the planting and if n reaches 0 we are end of the process and return True
6. Else return False

TC is O(n) as we are iterating through all the elements

SC is O(1) as we are not using any extra space or memory.

```
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




 
