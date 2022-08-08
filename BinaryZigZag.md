Given the root of a binary tree, return the zigzag level order traversal of its nodes' values. (i.e., from left to right, then right to left for the next level and alternate between).};

        3
     9    20
        15  7

Input: root = [3,9,20,null,null,15,7]

Output: [[3],[20,9],[15,7]]

We can use breath first search.  We take a queue and push the parent.
After each loop we will have a level of the tree.  Before we push the 
array onto the result we reverse every other level.

L1   3          
L2  9  20     ----->   20 9
L3    15  7

     3
<-----------

   9  20
<-----------

     15 7
<----------


Init q = [3]
while q is not empty
  Init l = [] // we will store each level of elements here
  init lengthOfQueue //this will tell us how many elements we loop through
  loop from 0 to lengthofqueue
  get front of queue
  push it onto level
  if we have a left push it
  if we have a right push it
  if its odd push l onto results
  if its even push l.reverse onto results
return results
