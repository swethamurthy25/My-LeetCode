Given a string s, check if it can be constructed by taking a substring of it and appending multiple copies of the substring together.

Example 1:
Input: s = "abab"
Output: true
Explanation: It is the substring "ab" twice.

Example 2:
Input: s = "aba"
Output: false

Example 3:
Input: s = "abcabcabcabc"
Output: true
Explanation: It is the substring "abc" four times or the substring "abcabc" twice.

Constraints:
1 <= s.length <= 104
s consists of lowercase English letters.
___________________________________________________________________________________________

Understanding:
-- First check the len of the string , the string can have min of 2 repetitions (substring) 
-- So n//2 is used to identify or limit the repetations.

Solution:
-- rep = '': Initializes an empty string rep that will be used to construct the potential substring.
-- n = len(s): Computes the length of the input string s and stores it in the variable n.
-- for i in range(n // 2):: Iterates through the range of indices from 0 to n // 2 - 1.
-- rep += s[i]: Appends the character at index i of the input string s to the rep string, gradually building a potential substring.
-- if n % len(rep) == 0:: Checks if the length of the substring candidate rep evenly divides the length of the input string s.
-- if rep * (n // len(rep)) == s:: If the condition in step 5 holds, this checks if the repetition of the substring candidate 
   rep n // len(rep) times is equal to the original input string s.

-- return True: If both conditions in steps 5 and 6 are satisfied, it means that the input string s can be formed by repeating 
   the substring candidate rep. In this case, the method returns True.
-- return False: If no valid substring pattern is found in the loop, the method returns False, indicating that the input string 
   cannot be formed by repeating a substring.

Time Complexity (TC): The loop iterates up to n // 2 times, where n is the length of the input string. 
                      Therefore, the time complexity is O(n) due to the loop.

Space Complexity (SC): The space complexity is also O(n) because of the rep string used to build the potential substring.
                       The method constructs a candidate substring and checks if it can be repeated to form the original input string. 
                       It's a form of pattern matching where the code attempts to find a valid repeating pattern within the string.


```python      
class Solution:
    def repeatedSubstringPattern(self, s: str) -> bool:
        # TC is O(n) and SC is O(n)
        rep = ''
        n = len(s)
        for i in range(n // 2):
            rep += s[i]
            if n % len(rep) == 0:
                if rep * (n // len(rep)) == s:
                    return True
        return False















 
