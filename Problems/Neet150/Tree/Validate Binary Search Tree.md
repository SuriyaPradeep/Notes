#tree #recursion #bst 
Given the `root` of a binary tree, _determine if it is a valid binary search tree (BST)_.

A **valid BST** is defined as follows:

- The left 
    
    subtree
    
     of a node contains only nodes with keys **less than** the node's key.
- The right subtree of a node contains only nodes with keys **greater than** the node's key.
- Both the left and right subtrees must also be binary search trees.

**Example 1:**

![](https://assets.leetcode.com/uploads/2020/12/01/tree1.jpg)

**Input:** root = [2,1,3]
**Output:** true

**Example 2:**

![](https://assets.leetcode.com/uploads/2020/12/01/tree2.jpg)

**Input:** root = [5,1,4,null,null,3,6]
**Output:** false
**Explanation:** The root node's value is 5 but its right child's value is 4.

### Solution
```java
class Solution{
	public boolean isValidBST(TreeNode root) {  
	    return dfs(root,null,null);  
	}  
	public boolean dfs(TreeNode root,Integer min,Integer max){  
	    if(root==null){  
	        return true;  
	    }  
	    if(min!=null && root.val<=min || max!=null && root.val>=max){  
	        return false;  
	    }  
	    return dfs(root.left,min,root.val) && dfs(root.right,root.val,max);  
	}
}
```

**Explanation**
1. 1. **Initial Call**:
    
    - The `isValidBST` function is called with the root node and initially no constraints on the value (`min` and `max` are `null`).
2. **Base Case**:
    
    - If the `root` is `null`, the function returns `true`, indicating that an empty subtree is valid.
3. **Value Check**:
    
    - The function checks if the current node's value violates the BST property:
        - If `min` is not `null` and `root.val <= min`, it returns `false` because the current node's value must be greater than `min`.
        - If `max` is not `null` and `root.val >= max`, it returns `false` because the current node's value must be less than `max`.
4. **Recursive DFS**:
    
    - The function then recursively checks the left and right subtrees:
        - For the left subtree, it calls `dfs` with the `min` unchanged and the current node's value (`root.val`) as the new `max`. This ensures that all nodes in the left subtree are less than the current node's value.
        - For the right subtree, it calls `dfs` with the `max` unchanged and the current node's value (`root.val`) as the new `min`. This ensures that all nodes in the right subtree are greater than the current node's value.
5. **Return**:
    
    - The function returns `true` only if both the left and right subtrees are valid BSTs.