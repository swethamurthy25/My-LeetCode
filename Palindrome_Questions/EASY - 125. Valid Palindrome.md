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

 * if s is None: return False. This checks if the input string s is None. If it is, the function returns False.
 * This is a safety check to handle the case where s is not provided or is None.
 * The main logic of the function is to create a cleaned string newStr. 
 * For each character, it checks if it is alphanumeric using char.isalnum(). If it is alphanumeric, it converts it to lowercase using char.lower(). 
 * This filters out non-alphanumeric characters and converts the remaining alphanumeric characters to lowercase.
 * The cleaned string newStr is then compared to its reverse (newStr[::-1]). This is done to check if the string is a palindrome.
 * If the cleaned string is equal to its reverse, the function returns True, indicating that the original string is a palindrome. Otherwise, it returns False.

 * The time complexity (TC) is O(n) where n is the length of the input string, and the space complexity (SC) is O(n) due to the additional space
   needed for the cleaned string.

```python
class Solution:
    def isPalindrome(self, s: str) -> bool:
        #Brute Force - TC is O(n) & SC is o(n)
        if s is None: return False

        newStr = ''.join(char.lower() for char in s if char.isalnum())
        return newStr == newStr[::-1]
```


OPTIMIZED SOLUTION:

1. Two pointers left and right are initialized at the beginning and end of the string, respectively. These pointers will move towards each other during the comparison process.
2. The main loop continues until the left pointer crosses or meets the right pointer.
3. If the character at the left pointer is not alphanumeric, increment the left pointer. If the character at the right pointer is not alphanumeric, decrement the
   right pointer. This step skips non-alphanumeric characters.
4. If both characters at the left and right pointers are alphanumeric and not equal (ignoring case), return False because the string is not a palindrome.
5. If the characters are equal, move the left pointer to the right and the right pointer to the left.
6. If the loop completes without returning False, the string is a palindrome, and the method returns True.
7. It has a time complexity of O(n) and a space complexity of O(1).

```python
class Solution:
    def isPalindrome(self, s: str) -> bool:
        #Optimized Solution using two pointer
        if s is None: return False
        left, right = 0, len(s)-1

        while left < right:
            if not s[left].isalnum():
                left += 1
            elif not s[right].isalnum():
                right -= 1
            elif s[left].lower() != s[right].lower():
                return False
            else:
                left += 1
                right -= 1
        return True
'''




