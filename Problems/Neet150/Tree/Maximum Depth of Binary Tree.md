#tree #recursion 
### Question
Given the `root` of a binary tree, return _its maximum depth_.

A binary tree's **maximum depth** is the number of nodes along the longest path from the root node down to the farthest leaf node.

**Example 1:**

![](https://assets.leetcode.com/uploads/2020/11/26/tmp-tree.jpg)

**Input:** root = [3,9,20,null,null,15,7]
**Output:** 3

**Example 2:**

**Input:** root = [1,null,2]
**Output:** 2

### Solution
```java
class Solution{
	public int maxDepth(TreeNode root) {  
	    if(root==null){  
	        return 0;  
	    }  
	    return 1+Math.max(maxDepth(root.left),maxDepth(root.right));  
	}
}
```

**Explanation**
1. **Base Case (Line 3-5):**
    
    - The method first checks if `root` is `null`. If it is, it returns `0`. This represents the depth of an empty tree or when the recursion reaches a leaf node's child.
2. **Recursive Case (Line 6):**
    
    - The method calls itself recursively to calculate the maximum depth of the left subtree (`maxDepth(root.left)`) and the maximum depth of the right subtree (`maxDepth(root.right)`).
3. **Calculate Depth (Line 6):**
    
    - The method returns `1` plus the maximum depth of the left and right subtrees. The `1` represents the current node (root), and `Math.max(maxDepth(root.left), maxDepth(root.right))` determines the greater depth between the left and right subtrees.