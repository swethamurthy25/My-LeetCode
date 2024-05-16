A phrase is a palindrome if, after converting all uppercase letters into lowercase letters and removing all non-alphanumeric characters, it reads the same forward and 
backward. Alphanumeric characters include letters and numbers.
Given a string s, return true if it is a palindrome, or false otherwise.

Input: s = "A man, a plan, a canal: Panama"
Output: true
Explanation: "amanaplanacanalpanama" is a palindrome.

Input: s = "race a car"
Output: false
Explanation: "raceacar" is not a palindrome.

Input: s = " "
Output: true
Explanation: s is an empty string "" after removing non-alphanumeric characters.
Since an empty string reads the same forward and backward, it is a palindrome.

Constraints:
1 <= s.length <= 2 * 105
s consists only of printable ASCII characters.
_____________________________________________________________________________________________________________________

Understanding of the question:
- We need to check whether the given string s is a palindrome or not.
- Before doing that, we need to convert the string s to lowercase and remove the special characters from it
- Return True if it is palindrome or else return False
_____________________________________________________________________________________________________________________

Brute Force method: By comparing with its reverse
 - Initialize the new string.
 - For every character in the string, check if it's an alphanumeric (isalnum())
 - If yes, convert it to lowercase and add it to the new string
 - Then reverse the string and check if it's the same.

```python
class Solution:
    def isPalindrome(self, s: str) -> bool:
        newStr = ""
        for ch in s:
            if ch.isalnum():
                newStr += ch.lower()
        return newStr == newStr[::-1]
```

* Time complexity is O(n), where n is the length of the input string.
* Space Complexity is O(n), where n is the length of the modified string after removing non-alphanumeric characters.
_________________________________________________________________________________________________________________

Optimized Solution: By using the TWO Pointer approach
- Use two pointers, left and right, starting from the beginning and end of the string respectively, and then move them towards each other until they meet in the middle.
  left = 0 
  right = len(s)-1
 
- At each step, we check if the character at the left index is alphanumeric. If it's not, we move the left one position to the right.
- Similarly, if the character at the right index is not alphanumeric, we move right one position to the left.
```python
  while left < right:
        if not s[left].isalnum():
               left += 1
        elif not s[right].isalnum():
               right -= 1
 ```
 - If both the characters at the left and right indices are alphanumeric, we check if they are equal or not.
 - If they are not equal, the string is not a palindrome and we return False.
 - Otherwise, we continue moving the pointers towards each other.
 - If the pointers meet in the middle of the string and no mismatches have been found, the string is a palindrome and we return True.
```python
   elif s[left].lower() != s[right].lower():
          return False
   else:
        left += 1
        right -= 1
   return True
```

```python
class Solution:
    def isPalindrome(self, s: str) -> bool:
        #Two pointer with SC O(1)
        if s is None:
            return True
        left = 0
        right = len(s)-1

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
```
            
* The time complexity of this code is O(n) because we need to traverse the string once. 
* The space complexity is O(1) because we are not using any extra data structures to store the string.
___________________________________________________________________________________________________________________________-


   
- 

















