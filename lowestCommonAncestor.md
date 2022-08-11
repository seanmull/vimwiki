Given a binary tree, find the lowest common ancestor (LCA) of two given nodes in the tree.
According to the definition of LCA on Wikipedia: “The lowest common ancestor is defined between two nodes p and q as the lowest node in T that has both p and q as descendants (where we allow a node to be a descendant of itself).

Input: root = [3,5,1,6,2,0,8,null,null,7,4], p = 5, q = 1
Output: 3
Explanation: The LCA of nodes 5 and 1 is 3

Let's look at simple example
       6
    /    \
  3       4
        /  \
       2    1
       
The lca of 1 and 2 would be 4  // this is the normal case
The lca of 4 and 2 would be 4  // this is the special case

The way to solve this is to bubble the answer.  We have a left and right node.
If one is null and the other is p or q return p or q
If both are null return null
Use dfs to access the left and right nodes for every sub tree
The trick part is how to deal with special case that p or q is the lca
for that situation you need.
Have it return null or root given we have return both nulls or p and q
After that all we have left is the case that one side is not null then we just return that
node

Base cases
if root is null return null
if root is equal to p or q

Recursion cases
store left = lca(left)
store right = lca(right)
if left and right are null return null
if left and right are not null return root
else return left or right if the other one is null
