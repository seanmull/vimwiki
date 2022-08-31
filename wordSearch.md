Given an m x n grid of characters board and a string word, return true if word exists in the grid.

The word can be constructed from letters of sequentially adjacent cells, where adjacent cells are horizontally or vertically neighboring. The same letter cell may not be used more than once.

Example 1:

Input: board = [["A","B","C","E"],["S","F","C","S"],["A","D","E","E"]], word = "ABCCED"
Output: true

This problem should involve a backtracking method, since we are looking for all combinations of the graph. For instance:

A B
C D

Let's say we look for A->C->D->B

If we start at A and look in the B direction then the C direction
From C we look in the D direction (we cannot go back to A)
From D we look in the B direction (we cannot go back to D)

One way to not allow us to go back to the previous letter is to temporarily mark
the letter we don't want to go back to and replace it when we are done looking through that path

Steps:
1. Create a helper outOfBounds function that passes the grid and row, column 
2. Create the main function that loops through the grid calling the checkNeighbors function.
3. Create the checkNeighbors function
4.   Check base cases
5.    if we are at the end of the word return true
6.    if we are outOfBounds return false
7.  save the current character on the board 
8.  save the word as the substring minus the first letter 
9.  recursively look in all four direction and store result in each stack
10. restore the letter in the position
11. return results
