
Question:
Given two strings s and t, return true if t is an anagram of s, and false otherwise. An Anagram is a word or phrase formed by rearranging the letters 
of a different word or phrase, typically using all the original letters exactly once.

Example 1:
Input: s = "anagram", t = "nagaram"
Output: true

Example 2:
Input: s = "rat", t = "car"
Output: false

***********************************************************************
Understanding:
- we have to make sure the s and t has the same set of character and the same number of char count
- If we find a new character or if the char count is not matching return False, else return True
- We can try solving the questions either by using Python build-in function or without using it

**********************************************************************************
Approach 1: Using in-built sorted function

Time Complexity: O(nlogn) -- Due to sorting approach

Space Complexity: O(1) -- Constant space because we have only 26 characters

```python
class Solution:
    def isAnagram(self, s: str, t: str) -> bool:
        #Sorting approach - O(n log n)
        if len(s) != len(t):
            return False
        s = sorted(list(s)) 
        t = sorted(list(t)) 
        return s == t
```
        
***********************************************************************
Approach 2: Using in-built Counter function

Time Complexity: O(n)

Space Complexity: O(1) -- Constant space because we have only 26 characters

```python
class Solution:
    def isAnagram(self, s: str, t: str) -> bool:
        return Counter(s) == Counter(s)
```

****************************************************************************************
Approach 3 - Without using any of the in-built functions, Using Hashmap/Dictionary

How do we implement this?

Solution 1:
- Here hashmap will keep track of each character and its respective count. So build two hashmaps to keep track of s and t separately
For example: 
s = "anagram" --> our hashmap will look like this {a:3, n:1, g:1, r:1, m:1}
t = "nagaram: --> our hashmap will look like this {a:3, n:1, g:1, r:1, m:1}

- Every time we see a char, we need to increment the count by 1 in both hash maps
- Use the get function to add characters to the hashmap. If the key is not found in the hashmap, the get function will return
  the default value 0.
- After building the hashmap, we need to compare the keys (characters) and their values (count) from each of the hashmap
- Return false if the keys or the count is not matching, else return True
- Cover the edge case also --> means if the len(s) and len(t) are not same , directly we can return False

```python
class Solution:
    def isAnagram(self, s: str, t: str) -> bool:
        if len(s) != len(t):
            return False

        countS , countT = {}, {}
        for char in range(len(s)):
            countS[s[char]] = 1 + countS.get(s[char],0)
            countT[t[char]] = 1 + countT.get(t[char],0)
        for c in countS:
            if countS[c] != countT.get(c,0):
                return False
        return True
```

Time Complexity will be O(n) -- basically O(s+t) because we are iterating through both s and t strings.

Space complexity will be O(n) -- basically O(s+t) because building a hashmap takes some space.

__________________________________________________________________________________________________________________

Solution 2:
1. Initialize the result hashmap
2. For every char in s, if it is not present in hashmap, add that to hashmap 
3. If it is present in hashmap, increment the count by 1
4. For every char in t, if it is not present in hashmap, return False
5. Or else, decrement the hashmap value by 1 
6. For every letter in result. values, if it is not equal to 0, return False 
7. Else return True

Time Complexity: O(n)

Space Complexity: O(1) -- Constant space because we have only 26 characters

```python
class Solution:
    def isAnagram(self, s: str, t: str) -> bool:
        if len(s) != len(t):
            return False

        result = {}

        #First add the s characters to the result map
        for ch in s:
            if ch not in result:
                result[ch] = 1
            else:
                result[ch] += 1

        #Now iterate through t and check any ch of t present in the result
        #if t is present in the result, dec the count or else return False
        for ch in t:
            if ch not in result:
                return False
            else:
                result[ch] -= 1

        for letter in result.values():
            if letter != 0:
                return False
        return True
```
*********************** END ***************************************
