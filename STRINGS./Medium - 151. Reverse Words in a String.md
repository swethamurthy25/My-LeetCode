Given an input string s, reverse the order of the words.

A word is defined as a sequence of non-space characters. The words in s will be separated by at least one space. Return a string of the words in reverse order concatenated 
by a single space.

Note that s may contain leading or trailing spaces or multiple spaces between two words. The returned string should only have a single space separating the words. 
Do not include any extra spaces.

#### Example 1:

Input: s = "the sky is blue"

Output: "blue is sky the"

#### Example 2:

Input: s = "  hello world  "

Output: "world hello"

Explanation: Your reversed string should not contain leading or trailing spaces.

#### Example 3:

Input: s = "a good   example"

Output: "example good a"

Explanation: You need to reduce multiple spaces between two words to a single space in the reversed string.

#### Follow-up: If the string data type is mutable in your language, can you solve it in place with O(1) extra space?
______________________________________________________________________________________________________________________________________

### Understanding of the Question

* We are given an input string s and s contains the words
* We need to reverse the order of the words. For example: input: the sky is blue, output should be blue is sky the.
* Do not reverse the characters, but reverse only the words.
* s may contain leading or trailing spaces or multiple spaces between two words.
* The output string should only have a single space separating the words. Do not include any extra spaces.
_______________________________________________________________________________________________________________________________________

### Brute Force approach using built-in functions:

1. First split the words, so that they will be stored in a list. 
2. Then reverse the list.
3. Now we need to return the output as a string so use the join() method to concatenate the string again.

TC is O(n) and SC is O(n) since we are splitting and storing it in a list.

```python
class Solution:
    def reverseWords(self, s: str) -> str:
        #Using build-in functions
        s = s.split()
        s = reversed(s)        
        return " ".join(s)
```
