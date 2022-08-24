You are given an m x n grid where each cell can have one of three values:

0 representing an empty cell,
1 representing a fresh orange, or
2 representing a rotten orange.
Every minute, any fresh orange that is 4-directionally adjacent to a rotten orange becomes rotten.

Return the minimum number of minutes that must elapse until no cell has a fresh orange. If this is impossible, return -1.

Example 1:

Input: grid = [[2,1,1],[1,1,0],[0,1,1]]
Output: 4

X 0 0   X X 0  X X X  X X X  X X X
0 0     X 0    X X    X X    X X
  0 0     0 0    0 0    X 0    X X
  0       1      2      3      4
  
  
We need to use a BFS approach for this since we are expanding the rotten oranges and needing to count every day that has passed.  We also need to track when we have no more fresh oranges.

Steps
1. Count all the fresh oranges
2. Get all the [row, column] positions of the rotten oranges
3. We loop through all rotten locations
4. Take the top location from the queue
5. We look up, down, left, right from this location
6.  if we see a fresh orange we turn in rotten
7.  we add this location to the rotten oranges
8.  and we decrement the fresh oranges
9.  we add the minutes if we have any rotten oranges left
10.return if there is any fresh left

Pseudocode
init fresh = 0
init rotten as a queue
loop through grid
  if loc is rotten store it in rotten
  if loc is fresh increment fresh
init m 
while there is no rotten oranges left 
  init length to the queue size (important!!!!)
  loop through the current queue
    take loc from top of queue
    look up, left, right, down (guard for out of bounds)
      if it is fresh
        turn it rotten
        add it to the rotten queue
        decrement fresh
  if we have any rotten left increment minutes
return minutes


Common issues:
- storing the length after each bfs
