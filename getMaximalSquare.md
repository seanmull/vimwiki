Given an m x n binary matrix filled with 0's and 1's, find the largest square containing only 1's and return its area.

Input: matrix = [["1","0","1","0","0"],["1","0","1","1","1"],["1","1","1","1","1"],["1","0","0","1","0"]]
Output: 4

This problem can be solved via dynammic programming method.  Look at a simple example:

1 0 1
1 1 1
1 1 1 

First we check if the top row and column have a "1" so the length is 1 in this example
Then we start at row = 1 and column = 1

We loop through the bottom four squares following the given pattern

Look up look left and look up-left and pick the minimum of the three and then add the number
of the index

1 1 1            1 1 1
1 1 1      =>    1 2 2
1 1 1            1 2 3

We check all 4 corners of the square this way.

While all of this is going on update the max length and return max * max

Find if there is a "1" in the top row
Find if there is a "1" in the left column
Update max to 1 or 0
Loop for row (start at 1)
  Loop for column (start at 1)
    store left, up and diagonal
    if we are at "1"
      update the current square to 1 + the min of those three
      update max
return max * max
