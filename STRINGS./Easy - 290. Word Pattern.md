Given a pattern and a string s, find if s follows the same pattern.

Here follow means a full match, such that there is a bijection between a letter in pattern and a non-empty word in s.

Input: pattern = "abba", s = "dog cat cat dog" and Output: true

Input: pattern = "abba", s = "dog cat cat fish" and Output: false

Input: pattern = "aaaa", s = "dog cat cat dog" and Output: false
_______________________________________________________________________________________

Understanding of the Problem:

* This question is similar to 205. isomorphic string.
* We are given patterns - with alphabets and string - string which contains words that are separated by a single white space
  
* The most naive way to start thinking about this problem is to have a single hash map, tracking which character (in the pattern) maps to what word (in s).
  
* Every word in string s should map with the alphabet in the patterns.
* As soon we see this, we should think about the data structure hashmap which can be used for mapping the words.

* But make sure the length of the pattern should match the number of words (edge case) if there is a mismatch return False
* The split function can be used to split the words in a string.

* For example: pattern = "abba" s = "dog cat cat dog"
* Here a --> dog , b --> cat , b --> cat , a --> dog ----> so return True

* For example: pattern = "abba" s = "dog cat cat fish"
* Here a --> dog, b --> cat, b --> cat, a --> fish ----> so return False [a is already mapped to the dog, it cannot be remapped to fish again, so return false]
_________________________________________________________________________________________________________

Solution:

* Initially we need to split the string s into a list so that it's easy to compare with the pattern.
* words = s.split(' '): The input string s is split into words using the space as a delimiter, and the resulting words are stored in the words list.

* if len(pattern) != len(words):: This condition checks if the length of the pattern and the number of words in the words list are not equal. If they have different lengths, the method immediately returns False, as the pattern and words cannot match.

* Two dictionaries, char_map, and word_map, are used to maintain mappings between characters in the pattern and words in the string, respectively.

*  The for loop iterates through the characters in the pattern (c) and the words in the words list (w) using the zip function, which pairs elements from two sequences together.

 * Inside the loop, the code checks if the mapping between characters and words is consistent in both directions:

 * if c in char_map and char_map[c] != w:: If the character c is already in the char_map dictionary and its corresponding word is not w, it means the pattern and
   words are inconsistent, and the method returns False.

 * if w in word_map and word_map[w] != c:: If the word w is already in the word_map dictionary and its corresponding character is not c, it means the pattern and
   word is inconsistent, and the method returns a False

* If no inconsistencies are found, the code updates the mappings in both char_map and word_map dictionaries:
* char_map[c] = w: Maps character c to word w in the char_map dictionary.
* word_map[w] = c: Maps word w to character c in the word_map dictionary.
* Finally, if all checks pass, the method returns True, indicating that the pattern and words match consistently.

Time complexity: O(N+M) where N represents the length of s and M represents the length of the pattern. 
All operations in the algorithm are linear with the length of the inputs.

Space complexity: O(W) where WWW is the number of unique characters in pattern and words in s, for the same reasons as the previous approach.

```python
class Solution:
    def wordPattern(self, pattern: str, s: str) -> bool:
        words = s.split(' ')
        
        #Edge case
        if len(pattern) != len(words):
            return False

        char_map = {}
        word_map = {}

        #Iterate through both words and patterns at the same time using ZIP 
        for c, w in zip(pattern,words):
            if c in char_map and char_map[c] != w:
                return False
            if w in word_map and word_map[w] != c:
                return False
            char_map[c] = w
            word_map[w] = c
        return True
```
__________________________________________________________________________________________

   
