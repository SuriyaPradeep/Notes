#tree #recursion 
### Question
Given a binary tree, determine if it is  **height-balanced**.

**Example 1:**

![](https://assets.leetcode.com/uploads/2020/10/06/balance_1.jpg)

**Input:** root = [3,9,20,null,null,15,7]
**Output:** true

**Example 2:**

![](https://assets.leetcode.com/uploads/2020/10/06/balance_2.jpg)

**Input:** root = [1,2,2,3,3,null,null,4,4]
**Output:** false

**Example 3:**

**Input:** root = []
**Output:** true

### Solution
```java
class Solution{
	public boolean isBalanced(TreeNode root) {  
	    if(root==null){  
	        return true;  
	    }  
	    return Height(root)!=-1;  
	}  
	public int Height(TreeNode root){  
	    if(root==null){  
	        return 0;  
	    }  
	    int left=Height(root.left);  
	    int right=Height(root.right);  
	    if(left==-1 || right==-1){  
	        return -1;  
	    }else if(Math.abs(right-left)>1){  
	        return -1;  
	    }  
	    return 1+Math.max(left,right);  
	}
}
```
**Explanation**
1. **isBalanced(TreeNode root)**:
    
    - This is the main function that checks whether the binary tree rooted at `root` is balanced.
    - If the tree is empty (`root == null`), it returns `true` because an empty tree is trivially balanced.
    - It calls the helper function `Height(root)`, which returns `-1` if the tree is not balanced. If `Height(root)` returns anything other than `-1`, the tree is balanced.
2. **Height(TreeNode root)**:
    
    - This helper function calculates the height of the tree while simultaneously checking if the tree is balanced.
    - If the subtree rooted at `root` is empty, it returns `0` (height of an empty subtree).
    - It recursively calculates the heights of the left and right subtrees.
    - If either the left or right subtree is unbalanced (`Height(root.left)` or `Height(root.right)` returns `-1`), it propagates the `-1` upward to indicate the tree is unbalanced.
    - If the difference in height between the left and right subtrees is more than `1`, it returns `-1` to indicate the tree is not balanced.
    - If the subtree is balanced, it returns the height of the subtree as `1 + Math.max(left, right)`.