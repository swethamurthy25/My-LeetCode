
Given a string s and an integer k, reverse the first k characters for every 2k characters counting from the start of the string.If there are fewer than k characters 
left, reverse all of them. If there are less than 2k but greater than or equal to k characters, then reverse the first k characters and leave the other as original.

Input: s = "abcdefg", k = 2
Output: "bacdfeg"

Input: s = "abcd", k = 2
Output: "bacd"
_______________________________________________________________________________________________________________________________

#### What did we understand from the question?

1. In string s, take the first k characters and reverse them 
2. Skip K characters
3. Then reverse the next k characters. In the end, if less than k characters remaining, reverse all of them

#### Example: 

S = abcdefg and k = 2

Now first k characters (2 characters) are "ab" , reverse them
s = bacdefg

Now skip k characters (2 characters), just copy the same
s = bacdefg 

Now skip the next k characters ie "ef" 
s = bacdfeg

Now only g is left which is less than k, so leave it as it is.
s = bacdfeg
______________________________________________________________________

Approach 1: Brute Force using built-in functions

TC is O(n) and - n is the size of string s
SC is O(n) - n is the size of the list array

1. If the k value is greater than or equal to len(S), we are going to reverse the entire string s. [Edgecase]
2. Iterating through every character of string and skipping 2*k characters - for (0,len(s),2*k)
3. Reverse k characters and join them with the original string

```python
class Solution:
    def reverseStr(self, s: str, k: int) -> str:
        if k >= len(s):
            s[::-1]
        s = list(s)
        for i in range(0,len(s),2*k):
            s[i:i+k] = reversed(s[i:i+k])
        return "".join(s)
```

________________________________________________________________________________________________________________________________






