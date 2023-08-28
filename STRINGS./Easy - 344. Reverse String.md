
Write a function that reverses a string. The input string is given as an array of characters s.
You must do this by modifying the input array in place with O(1) extra memory.

Input: s = ["h","e","l","l", "o"]
Output: ["o","l","l","e","h"]

Input: s = ["H","a","n","n","a","h"]
Output: ["h","a","n","n","a","H"]

________________________________________________________________________________________

Approach 1: Brute force using python inbuild functions

1. Input is given in the form of a list array with each character separated by a comma
2. So we can use list.reverse() function to get the output

TC is O(n) and SC is O(1)

```python
class Solution:
    def reverseString(self, s: List[str]) -> None:
        return s.reverse()
```
____________________________________________________________________________________________

Approach 2: Without using inbuild functions, using a two-pointer approach

1. Initialize two pointers - left ptr at the beginning of the array and right ptr at the end of the array
2. While left < right, if both left and right exist, swap both the left and right elements
3. For every swap, increment the left pointer by 1 and decrement the right pointer by 1

TC is O(n) and SC is O(1)

```python
class Solution:
    def reverseString(self, s: List[str]) -> None:
        left, right = 0, len(s)-1
        
        while left < right:
            if s[left] and s[right]:
                s[left],s[right] = s[right],s[left]
                left += 1
                right -= 1
        return s
```

________________________________________________________________________________________
