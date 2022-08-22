Given an array nums of distinct integers, return all the possible permutations. You can return the answer in any order.

Example 1:

Input: nums = [1,2,3]

Output: [[1,2,3],[1,3,2],[2,1,3],[2,3,1],[3,1,2],[3,2,1]]

One way to approach this problem is through backtracking.  

        [1           2            3]             
      
    2      3     1      3     1       2
    
    3      2     3      1     2       1
        
      
Create a backtracking function that push one element from arr into perm
and slices the same element from arr
Call the backtrack function
Replace both elements at the end of the loop

init results
function backtrack                 
  //base case if arr is []  
    push perm into result          
  // recursion case
  loop from 0 to arr length
    push arr[i] to perm       perm [1] arr [2]    
    slice out arr[i] from arr    
    call backtrack                
    get arr and perm to original state  
 call backtrack (arr, []) [1, 2] , []
 return results
 
stack 
[1, 2] , []  ------------------->  
[2] , [1]    popped         [1], [2] popped
[], , [1,2]  popped         [0], [2,1] popped

 
Note with each recursion call arr gets smaller but after the recursive call
arr and perm are back to there original state.  This undos those previous pushes
and pops.  We need this to look at the next i value.
