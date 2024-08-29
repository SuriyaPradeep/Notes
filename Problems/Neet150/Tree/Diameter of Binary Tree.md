#tree #recursion 
### Question
Given the `root` of a binary tree, return _the length of the **diameter** of the tree_.

The **diameter** of a binary tree is the **length** of the longest path between any two nodes in a tree. This path may or may not pass through the `root`.

The **length** of a path between two nodes is represented by the number of edges between them.

**Example 1:**

![](https://assets.leetcode.com/uploads/2021/03/06/diamtree.jpg)

**Input:** root = [1,2,3,4,5]
**Output:** 3
**Explanation:** 3 is the length of the path [4,2,1,3] or [5,2,1,3].

**Example 2:**

**Input:** root = [1,2]
**Output:** 1

### Solution
```java
class Solution{
	int result=-1;  
	public int diameterOfBinaryTree(TreeNode root) {  
	    dfs(root);  
	    return result;  
	}  
	public int dfs(TreeNode root){  
	    if(root==null){  
	        return -1;  
	    }  
	    int left=1+dfs(root.left);  
	    int right=1+dfs(root.right);  
	    result=Math.max(result,(left+right));  
	    return Math.max(left,right);  
	}
}
```

**Explanation**
1. `int result=-1;`: Initializes the result variable to store the maximum diameter found.
2. `public int diameterOfBinaryTree(TreeNode root)`: The main function that starts the DFS traversal.
3. `dfs(root);`: Calls the depth-first search helper function.
4. `return result;`: Returns the final result after the traversal.
5. `public int dfs(TreeNode root)`: The DFS helper function that calculates the height of the tree and updates the diameter.

The helper function `dfs`:
- Returns `-1` for `null` nodes, indicating a height of `0` for non-existent nodes.
- Computes the height of the left and right subtrees.
- Updates the `result` with the maximum diameter found so far.
- Returns the height of the current node.