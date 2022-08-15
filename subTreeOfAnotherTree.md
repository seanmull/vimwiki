Given the roots of two binary trees root and subRoot, return true if there is a subtree of root with the same structure and node values of subRoot and false otherwise.

A subtree of a binary tree tree is a tree that consists of a node in tree and all of this node's descendants. The tree tree could also be considered as a subtree of itself.
Input: root = [3,4,5,1,2], subRoot = [4,1,2]
Output: true

Steps:
1. Create a helper function that checks to see if trees are the same.
2. Run isSubtree recursively to see if we see at least one instance of a match
3.  Return true if at least we get one true
4.  Otherwise return false

Helper function
isSameTree
 //base cases
 if t1 and t2 is null return true
 if t1 or t2 is null return false
 // recursive cases
 left = isSametree(t1.left, t2.left)
 right = isSametree(t1.right, t2.right)
 return t1.val === t2.val and left and right
 
isSubtree
  //base cases
  if root or subroot is null return false
  set cur to false
  if(rootval = subval)
    cur = isSameTree(root, sub)
  // recursively cases
  return cur ||
         isSubtree(root.left, sub) ||
         isSubtree(root.right, sub) 
