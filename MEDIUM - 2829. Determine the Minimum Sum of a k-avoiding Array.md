You are given two integers, n, and k.
An array of distinct positive integers is called a k-avoiding array if there does not exist any pair of distinct elements that sum to k.
Return the minimum possible sum of a k-avoiding array of length n.

Input: n = 5, k = 4 

Output: 18

Explanation: Consider the k-avoiding array [1,2,4,5,6], which has a sum of 18. It can be proven that there is no k-avoiding array 
with a sum less than 18.

Input: n = 2, k = 6

Output: 3

Explanation: We can construct the array [1,2], which has a sum of 3.
It can be proven that there is no k-avoiding array with a sum less than 3.
________________________________________________________________________________________________

#### Understanding of the Question:

1. We will be given two values n and k. n is the number of elements in the array and k is some value
2. Now we need to form or generate an 'n' list of elements and return its sum as output.
3. But here is the trickier part, if you take any two numbers from the list and add them together, you should not
   get the number "k".
4. So, the array should be designed in such a way that no pair of numbers within it can be combined to give you a sum of the value k.

_________________________________________________________________________________________________________

#### Optimized Solution:

1. A set s is initialized.
2. A variable i is initialized to 1. This will be used to generate numbers that will be added to the set.
3. Then the while loop is used to generate numbers and add them to the set s until the set's length becomes equal to n,
   which is the desired length of the k-avoiding array.

Inside the loop:

4. It checks if k - i is not already in the set s. This is to ensure that the sum of i and k - i does not equal k, 
   which is the condition for a k-avoiding array.
5. If the condition is met, i is added to the set s.
6. After either adding an element to the set or skipping it, i is incremented by 1 to move to the next number.
7. Once the set s has reached the desired length n, the loop exits.

The code returns the sum of all elements in the set s using the sum() function.

TC is O(n) and SC is O(n) since we are using a set function for storing the array elements.

```python
class Solution:
    def minimumSum(self, n: int, k: int) -> int:
        #Initialize a set
        s = set()
        i = 1
        while len(s) < n:
            if k - i not in s:
                s.add(i)
            i += 1
        return sum(s)
```




