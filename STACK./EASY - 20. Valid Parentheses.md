Given a string s containing just the characters '(', ')', '{', '}', '[' and ']', determine if the input string is valid.

An input string is valid if:

Open brackets must be closed by the same type of brackets.
Open brackets must be closed in the correct order.
Every close bracket has a corresponding open bracket of the same type.

Example 1:
Input: s = "()"
Output: true

Example 2:
Input: s = "()[]{}"
Output: true

Example 3:
Input: s = "(]"
Output: false

__________________________________________________________________________________

Approach 1: Using Stack and hashmap/dictionary

* First We have to check if the given string is valid or not based on parenthesis.
* And the condition for the same is given in the question.
* Stack - because we have to see if they are in the correct order or not. 
* Hashmap - to see if the closing has an opening parenthesis we will use a hashmap.

Logic how it works:

1. Start iterating from the beginning of the string 
2. When we encounter an opening bracket i.e. "(" or "[" or "{" it may or may not be an invalid expression because there can be a matching ending bracket somewhere in the remaining part of the expression.
3. Here, we simply increment the counter keeping track of left parenthesis till now. (left += 1)
4. If we encounter a closing bracket, this has two meanings:
    - One, there was no matching opening bracket for this closing bracket and in that case, we have an invalid expression. This is the case when left == 0 i.e. when there are no unmatched left brackets available.
    - We had some unmatched opening brackets available to match this closing bracket. This is the case when left > 0 i.e. we have unmatched left brackets available.
5. Continue processing the string until all parenthesis have been processed.
6. If in the end we still have unmatched left parenthesis available, this implies an invalid expression.

************************************

Approach:

1. Initialize an empty stack
2. Initialize a hashmap where each closing has an opening parenthesis.
3. Now we will use a for loop for iterating through the string.
4. If the first element is opening parenthesis, push it into the stack.
5. Else If there is a closing parenthesis, check if the last element in the stack (stack[-1]) is the opening parenthesis or not. The stack should not be empty because the first element would never be a closing parenthesis.
6. So if the given condition is true, pop it from the stack. So we no longer have to check or deal with that parenthesis
7. Else return false because it is not valid
8. Once we have done it for all the elements if the stack is empty at last we would know that it is valid (because we are popping all the parenthesis) or else false.

TC is O(n) because we are using one for loop and stack
SC is O(n) because we are using a dictionary and stack
```python
class Solution:
    def isValid(self, s: str) -> bool:
        
        stack = []
        dict = {")":"(",
                 "]":"[",
                 "}":"{"
                }
        
        for ch in s:
            if ch in dict:
                if stack and stack[-1] == dict[ch]:
                    stack.pop()
                else:
                    return False
            else:
                stack.append(ch)
        
        return True if not stack else False
```
_________________________________________________________________________________________

Approach 2:
```python
class Solution:
    def isValid(self, s: str) -> bool:
        stack = []
        dict = {')':'(', 
                ']':'[', 
                '}':'{'}
        opening_brackets =  ["(","[","{"]

        for i in s:
            if i in opening_brackets:
                stack.append(i)
            elif stack and stack[-1] == dict[i]:
                stack.pop()
            else:
                return False

        if stack == []: return True
        else: return False
```
______________________________________________________________________________________
