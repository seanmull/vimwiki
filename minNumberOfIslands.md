Given an m x n 2D binary grid grid which represents a map of '1's (land) and '0's (water), return the number of islands.

An island is surrounded by water and is formed by connecting adjacent lands horizontally or vertically. You may assume all four edges of the grid are all surrounded by water.


Example 1:

Input: grid = [
  ["1","1","1","1","0"],
  ["1","1","0","1","0"],
  ["1","1","0","0","0"],
  ["0","0","0","0","0"]
]

Output: 1

The problem asks to provide a number of all contiguous 1's in the array. For instance
the example above is only one island since there is no 0's seperating the one's.

One approach to the problem is to loop through all elements and perform a depth first
search on all. We would need to convert the 1 to 0 for all elements visited.

Psedocode

Make a helper dfs function

// base cases
if out of bounds return
if element == "0" return

set element to "0"
// recursive cases
dfs(up)
dfs(down)
dfs(left)
dfs(right)

main function
loop through grid
if element = 0 continue
count++
dfs(element)
