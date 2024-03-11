A phrase is a palindrome if, after converting all uppercase letters into lowercase letters and removing all non-alphanumeric characters, it reads the same forward 
and backward. Alphanumeric characters include letters and numbers.

Given a string s, return true if it is a palindrome, or false otherwise.

Example 1:

Input: s = "A man, a plan, a canal: Panama"

Output: true

Explanation: "amanaplanacanalpanama" is a palindrome.

Example 2:

Input: s = "race a car"

Output: false

Explanation: "raceacar" is not a palindrome.

_________________________________________________________________________________________________________________________________

BRUTE FORCE METHOD:

 * Consider a string “s” and first remove all the alphanumeric characters like spaces and commas.
 * The isalnum() method in Python is used to check if all characters in a given string are alphanumeric. 
 * Then change all the letters to lowercase.
 * And then reverse the string and compare it with the original “s”. If it is the same return True else return False

 * TC - O(N) & SC is O(N) - Here, we used extra memory because we are building a new string, and also using the in-build functions which will increase
    the time complexity.

```python
class Solution:
    def isPalindrome(self, s: str) -> bool:
        #Brute Force - TC is O(n) & SC is o(n)
        if s is None: return False

        newstr = ""
        for i in s:
            if i.isalnum():
                newstr += i.lower()
        return newstr == newstr[::-1]
```






