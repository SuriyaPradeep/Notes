#tree #recursion 
Given two integer arrays `preorder` and `inorder` where `preorder` is the preorder traversal of a binary tree and `inorder` is the inorder traversal of the same tree, construct and return _the binary tree_.

**Example 1:**

![](https://assets.leetcode.com/uploads/2021/02/19/tree.jpg)

**Input:** preorder = [3,9,20,15,7], inorder = [9,3,15,20,7]
**Output:** [3,9,20,null,null,15,7]

**Example 2:**

**Input:** preorder = [-1], inorder = [-1]
**Output:** [-1]

### Solution
```java
class Solution{
	public TreeNode buildTree(int[] preorder, int[] inorder) {  
	    if(preorder.length==0 || inorder.length==0){  
	        return null;  
	    }  
	    TreeNode root=new TreeNode(preorder[0]);  
	    int mid=0;  
	    for(int i=0;i<inorder.length;i++){  
	        if(preorder[0]==inorder[i]){  
	            mid=i;  
	            break;  
	        }  
	    }  root.left=buildTree(Arrays.copyOfRange(preorder,1,mid+1),Arrays.copyOfRange(inorder,0,mid));  
	    root.right=buildTree(Arrays.copyOfRange(preorder,mid+1,preorder.length),Arrays.copyOfRange(inorder,mid+1,inorder.length));  
	    return root;  
	}
}
```

**Explanation**
1. **Base Case**:
    
    - If either `preorder` or `inorder` is empty (`preorder.length == 0 || inorder.length == 0`), the tree is empty, so the method returns `null`.
2. **Identify the Root**:
    
    - The first element of the `preorder` array (`preorder[0]`) is always the root of the tree or subtree. So, you create a new `TreeNode` with this value: `TreeNode root = new TreeNode(preorder[0]);`.
3. **Find the Root in Inorder Array**:
    
    - You search for the root's value in the `inorder` array. The index where this value is found (`mid`) helps you determine the boundaries of the left and right subtrees in the `inorder` array.
    - The left part of the `inorder` array (from the start up to `mid`) corresponds to the left subtree, and the right part (from `mid + 1` to the end) corresponds to the right subtree.
4. **Recursive Construction**:
    
    - **Left Subtree**:
        - You call `buildTree` recursively for the left subtree using the elements after the root in the `preorder` array (from index 1 to `mid + 1`) and the left part of the `inorder` array (from index 0 to `mid`).
    - **Right Subtree**:
        - You call `buildTree` recursively for the right subtree using the remaining elements in the `preorder` array (from index `mid + 1` to the end) and the right part of the `inorder` array (from index `mid + 1` to the end).
    - The recursive calls build the left and right subtrees of the root, and these are then linked to the root node as `root.left` and `root.right`.
5. **Return the Root**:
    
    - Finally, the root node with its subtrees attached is returned as the result.
