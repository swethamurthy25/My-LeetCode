Given an m x n 2D binary grid which represents a map of '1's (land) and '0's (water), return the number of islands.

An island is surrounded by water and is formed by connecting adjacent lands horizontally or vertically. You may assume all four edges
of the grid is all surrounded by water.

<img width="233" alt="image" src="https://github.com/swethamurthy25/My-LeetCode/assets/112581595/96aa8db6-4907-46fd-a981-95d0bd620c28">

________________________________________________________________________________________________________________

#### Understanding of the Question:

1. LeetCode 200 is about counting the number of “islands” in a grid of 0s and 1s.
2. In this case, islands are any group of 1s with 0s on each side. Diagonals don’t count though.
3. As we generally know, islands are 1's that are surrounded by 0's on four sides but this strategy won't work here.
4. Since We can only connect the lands or 1’s horizontally and vertically, but not diagonally.
5. Both Depth-First Search (DFS) and Breadth-First Search (BFS) can be used to solve the island counting question.
6. But we prefer to use DFS here because it's a natural fit for exploring connected components like islands.
7. It starts from a cell and explores as far as possible along one branch before backtracking
8. This behavior aligns well with the concept of exploring a single island until there are no more connected land cells to explore.

___________________________________________________________________________________________________________________________

#### Solution using DFS:

We can split the solution into two parts - DFS and actual computation of island count

#### Computation of Island Count

1. The numIslands method takes a 2D list grid as input and calculates the number of islands in the grid.
2. Edge case - If not grid: return 0: If the grid is empty, the function returns 0 immediately.
3. Initialize a variable island to keep track of the number of islands found.
4. The nested for loops iterate through each cell in the grid.
5. If the cell value is '1', indicating an unvisited island cell, the dfs method is called to explore the entire island connected to this cell
6. After the dfs call, the island count is incremented.
7. Finally, the method returns the total count of islands found.

````python
def numIslands(self, grid: List[List[str]]) -> int:
        if not grid: return 0
        island = 0
        for r in range(len(grid)):
            for c in range(len(grid[r])):
                if grid[r][c] == '1':
                    self.dfs(grid,r,c)
                    island += 1
        return island
````

#### DFS

1. The dfs method is a depth-first search (DFS) function that explores connected cells in the grid.
2. It takes three parameters: self, representing the instance of the class, grid which is the input grid, and the indices r and c
   which represent the row and column indices of the current cell being explored.
3. grid[r][c] = '0': This line marks the current cell as visited by changing its value to '0', indicating that it's no longer part of an island.
4. lstt = [(r-1,c),(r+1,c),(r,c-1),(r,c+1)]: This creates a list of tuples representing the neighboring cells of the current cell (above, below, left, and right).
5. The for loop iterates through the neighboring cells, checking if they are within the bounds of the grid and if they contain a '1'.
6. If both conditions are met, the dfs function is recursively called on the neighboring cell.

```python
class Solution:
    def dfs(self,grid,r,c):
        grid[r][c] = '0'
        lstt = [(r-1,c),(r+1,c),(r,c-1),(r,c+1)]
        for row,col in lstt:
            if row >=0 and col >=0 and row < len(grid) and col <len(grid[row]) and grid[row][col] == '1':
                self.dfs(grid,row,col)
````
#### Complete Code:

```python
class Solution:
    def dfs(self,grid,r,c):
        grid[r][c] = '0'
        lstt = [(r-1,c),(r+1,c),(r,c-1),(r,c+1)]
        for row,col in lstt:
            if row >=0 and col >=0 and row < len(grid) and col <len(grid[row]) and grid[row][col] == '1':
                self.dfs(grid,row,col)

    def numIslands(self, grid: List[List[str]]) -> int:
        if not grid: return 0
        island = 0
        for r in range(len(grid)):
            for c in range(len(grid[r])):
                if grid[r][c] == '1':
                    self.dfs(grid,r,c)
                    island += 1
        return island
````

Time complexity: O(M×N) where M is the number of rows and N is the number of columns.

Space complexity: worst case O(M×N) in case the grid map is filled with lands where DFS goes by M×N deep.

