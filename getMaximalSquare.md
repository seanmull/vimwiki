Given an m x n binary matrix filled with 0's and 1's, find the largest square containing only 1's and return its area.

Input: matrix = [["1","0","1","0","0"],["1","0","1","1","1"],["1","1","1","1","1"],["1","0","0","1","0"]]
Output: 4

This problem can be solved via dynammic programming method.  Look at a simple example:

1 0 1
1 1 1
1 1 1 

First we check if the top row and column have a "1" so the length is 1 in this example
Then we start at row = 1 and column = 1





```
/**
 * @param {character[][]} matrix
 * @return {number}
 */
var maximalSquare = function(matrix) {
    let maxRow = matrix[0].indexOf("1")
    let maxCol = matrix.map((x) => (x[0])).indexOf("1")
    let max = (maxRow !== -1 || maxCol !== -1) ? 1 : 0
    for(let r = 1; r < matrix.length; r++){
        for(let c = 1; c < matrix[0].length; c++){
            let left = parseInt(matrix[r][c - 1]),
                top = parseInt(matrix[r - 1][c]),
                dia = parseInt(matrix[r - 1][c -1]) 
            if(matrix[r][c] === "1"){
                matrix[r][c] = Math.min(left, top, dia) + 1          
                max = Math.max(max, parseInt(matrix[r][c]))
            }
        }
    }
    return max * max
};
```
