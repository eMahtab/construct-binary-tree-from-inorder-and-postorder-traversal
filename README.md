# Construct Binary Tree from Inorder and Postorder Traversal
### https://leetcode.com/problems/construct-binary-tree-from-inorder-and-postorder-traversal

Given inorder and postorder traversal of a tree, construct the binary tree.

**Note: You may assume that duplicates do not exist in the tree.**
```
For example, given

inorder = [9,3,15,20,7]
postorder = [9,15,7,20,3]
Return the following binary tree:

    3
   / \
  9  20
    /  \
   15   7
```

### Implementation :

```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
class Solution {
    public static TreeNode buildTree(int[] inorder, int[] postorder) {
	   int inOrderStart = 0;
	   int inOrderEnd = inorder.length - 1;
	   int postOrderStart = 0;
	   int postOrderEnd = postorder.length - 1;
	      
	   Map<Integer, Integer> map = new HashMap<>();
	   for(int i = 0; i < inorder.length; i++) {
	    	  map.put(inorder[i], i);
	   }
	      
	   return construct(inorder, inOrderStart, inOrderEnd, postorder, postOrderStart, postOrderEnd, map);
    }
	
    private static TreeNode construct(int[] inorder, int inStart, int inEnd, 
	   int[] postorder, int postStart, int postEnd, Map<Integer, Integer> map) {
	   if(inStart > inEnd || postStart > postEnd)
		return null;
		
	   TreeNode node = new TreeNode(postorder[postEnd]);
	   int rootIndex = map.get(postorder[postEnd]);
	   int sizeOfLeftSubtree = rootIndex - inStart;
	   node.left = construct(inorder, inStart, rootIndex - 1, 
                                 postorder, postStart, postStart + sizeOfLeftSubtree - 1, map);
	   node.right = construct(inorder, rootIndex + 1, inEnd, 
                                  postorder, postStart + sizeOfLeftSubtree, postEnd - 1, map);
		
	   return node;
   }
}
```
**👉 In above implementation key thing is to specify the start and end indices for the Postorder array correctly**
