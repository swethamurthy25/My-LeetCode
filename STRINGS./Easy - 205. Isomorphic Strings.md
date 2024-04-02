Given two strings s and t, determine if they are isomorphic.
Two strings s and t are isomorphic if the characters in s can be replaced to get t.
All occurrences of a character must be replaced with another character while preserving the order of characters. No two characters may map to the same character, 
but a character may map to itself.

Input: s = "egg", t = "add"
Output: true

Input: s = "foo", t = "bar"
Output: false

Input: s = "paper", t = "title"
Output: true

Constraints:
1 <= s.length <= 5 * 104
t.length == s.length
s and t consist of any valid ASCII character.
_____________________________________________________________________________________________

What did we understand from the question?

1. We are given two strings s and t, which are the same length [Edge case]
2. We need to map and compare each character of s to t. One character of t should map with only one character of s.
3. The order of mapping should not be changed.

For example:

s = foo and t = bar

f --> b

o --> a

o --> r (here o is already mapped to a, it cannot be remapped to r again)

So return False.
_________________________________________________________________________________________

Using Hashmap/Dictionary:

1. Edge case: if len(s) != len(t):: 
2. This condition checks if strings s and t lengths are unequal. If they have different lengths, they cannot be isomorphic, so the method immediately returns False

3. s_map, t_map = {}, {}: Two dictionaries (s_map and t_map) are used to map characters from one string to the other.

4. for i in range(len(s)):
This loop iterates through each index i from 0 to len(s) - 1.

5. s_ch = s[i] and t_ch = t[i] assign the characters at index I of strings s and t to variables s_ch and t_ch, respectively.

6. The following three conditions are used to check if the mapping between characters is consistent:

7. if s_ch is not in s_map:: If the character from string s is not in the s_map dictionary, it's added as a key with a value of the corresponding character from string t.
 
8. if t_ch is not in t_map:: If the character from string t is not in the t_map dictionary, it's added as a key with a value of the corresponding character from string s.
 
9. if t_map[t_ch] != s_ch or s_map[s_ch] != t_ch:: This condition checks if the mapping between characters is consistent in both directions. If there's any inconsistency, the method returns False.

10. If all characters are successfully mapped consistently, the method returns True, indicating that the strings are isomorphic.

```python
class Solution(object):
    def isIsomorphic(self, s, t):
        
        #Edge Cases - Given s.length = t.length
        if len(s) != len(t):
            return False

        #We require two hashmaps to store and compare the characters
        s_map = {}
        t_map = {}

        #Iterate through every character and their index
        for i in range(0,len(s)):
            s_ch = s[i]
            t_ch = t[i]

        #If the char is not in dict, add it to the dict 
        #If the char already exists, check whether the mapping holds true
            if s_ch not in s_map:
                s_map[s_ch] = t_ch
            if t_ch not in t_map:
                t_map[t_ch] = s_ch
            if t_map[t_ch] != s_ch or s_map[s_ch] != t_ch:
                return False
        return True
```
_______________________________________________________________________________

Complexity
Time complexity: O(n)
where n is the length of the input strings s and t. 
This is because we iterate through all the characters in the input strings once and for each character, we perform a constant amount of work, which includes 
checking if the current character already exists as a key in a dictionary and adding the current character and its corresponding character in the other string as a
key-value pair to the appropriate dictionary.

Space complexity: O(n)
We use two dictionaries, s_map, and t_map, to store the mappings of the characters in s and t. 
Each dictionary can store at most n key-value pairs, where n is the length of the input strings. 
Since we are using two dictionaries, the space complexity is O(2n) = O(n)

____________________________________________________________________________________________________________
