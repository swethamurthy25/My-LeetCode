This covers two similar questions from leetcode:

118. Given an integer numRows, return the first numRows of Pascal's triangle.
     In Pascal's triangle, each number is the sum of the two numbers directly above it.
     Return the entire result array.

119. Given an integer rowIndex, return the rowIndexth (0-indexed) row of Pascal's triangle.
     In Pascal's triangle, each number is the sum of the two numbers directly above it.
     Return the rowIndexth (0th index) as output.

Example of 118:

Input: numRows = 5

Output: [[1],[1,1],[1,2,1],[1,3,3,1],[1,4,6,4,1]]

Example of 119:

Input: rowIndex = 3

Output: [1,3,3,1] - Here the value of the 3rd row only is returned as output

<img width="254" alt="image" src="https://github.com/swethamurthy25/My-LeetCode/assets/112581595/086ae3de-7caf-4881-84c0-b47c12f7bb60">

_______________________________________________________________________________________________________

### Solution for 118 & 119:

1. First let's handle the edge cases: If numRows is 0, an empty list is returned because there are no rows to generate.
2. If numRows is 1, the function returns [[1]], representing the first row of Pascal's triangle.

3. The result list is initialized with [[1]], representing the first row.
4. The for loop iterates from 0 to numRows - 2 to construct the remaining numRows - 1 rows of Pascal's triangle.
5. temp is created by adding 0 to the beginning and end of the previous row, effectively creating a row with two additional
   0s on each side.
6. An empty list row is initialized to store the elements of the current row.
7. Another nested loop iterates over the elements in temp, and each element in the current row is calculated as the sum of two 
   adjacent elements in temp.
8. The current row is appended to the result list.

### Result/output of 118:

After the loop completes, the function returns the result, which contains the first numRows rows of Pascal's triangle.

### Result/output of 119:

After the loop completes, the function returns result[rowIndex], which contains the rowIndex-th row of Pascal's triangle.

So the whole execution of the code is the same for both questions, it only differs at the final stage of returning the output.

### Source code of 118:

```python
class Solution:
    def generate(self, numRows: int) -> List[List[int]]:
        #Edge cases
        if numRows == 0: return []
        if numRows == 1: return [[1]]

        result = [[1]]
        for i in range(numRows-1):
            temp = [0] + result[-1] + [0]
            row = []
            for j in range(len(result[-1])+1):
                row.append(temp[j]+temp[j+1])
            result.append(row)
        return result
```

### Source code of 119:

```python
class Solution:
    def getRow(self, rowIndex: int) -> List[int]:
        #Edge case
        if rowIndex == 0: return [1]

        result = [[1]]
        for i in range(rowIndex):
            temp = [0] + result[-1] + [0]
            row = []
            for j in range(len(result[-1])+1):
                row.append(temp[j]+temp[j+1])
            result.append(row)
        return result[rowIndex]
```








     
