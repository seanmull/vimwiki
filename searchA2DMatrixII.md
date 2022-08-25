Write an efficient algorithm that searches for a value target in an m x n integer matrix matrix.
This matrix has the following properties:

Integers in each row are sorted in ascending from left to right.
Integers in each column are sorted in ascending from top to bottom.

Example 1:

Input: matrix = [[1,4,7,11,15],[2,5,8,12,19],[3,6,9,16,22],[10,13,14,17,24],[18,21,23,26,30]], target = 5
Output: true


[[1,4,7,11,15],
 [2,5,8,12,19],
 [3,6,9,16,22],
 [10,13,14,17,24],
 [18,21,23,26,30]], 
 
 target = 5
 
Steps
1. Start on the upper right
2. Move left until the number is less
3. Then go down until number is more
4. If we don't find it return false


init r and c to 0 and end
init m to end of row

while we are not out of bounds
  if we are the target return true
  if we are less then target move left
  if we are more move down
