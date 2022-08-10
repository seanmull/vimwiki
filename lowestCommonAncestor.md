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
       
The lca of 1 and 2 would be 4
The lca of 4 and 4 would be 4





S2 3, 1, 2
S1 6, 1, 2

function lowestCommonAncestor(root, p, q){
    if(p.val < root.val && q.val < root.val)
        return lowestCommonAncestor(root.left, p, q);

    if(p.val > root.val && q.val > root.val)
        return lowestCommonAncestor(root.right, p, q);

    return root.val;
}



function inOrderTraversal(node){
    if(node === null) return;
    inOrderTraversal(node.left);
    console.log(node.val);
    inOrderTraversal(node.right);

