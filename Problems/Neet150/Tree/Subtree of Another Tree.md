#tree #recursion 
### Question
Given the roots of two binary trees `root` and `subRoot`, return `true` if there is a subtree of `root` with the same structure and node values of `subRoot` and `false` otherwise.

A subtree of a binary tree `tree` is a tree that consists of a node in `tree` and all of this node's descendants. The tree `tree` could also be considered as a subtree of itself.

**Example 1:**

![](https://assets.leetcode.com/uploads/2021/04/28/subtree1-tree.jpg)

**Input:** root = [3,4,5,1,2], subRoot = [4,1,2]
**Output:** true

**Example 2:**

![](https://assets.leetcode.com/uploads/2021/04/28/subtree2-tree.jpg)

**Input:** root = [3,4,5,1,2,null,null,null,null,0], subRoot = [4,1,2]
**Output:** false

### Solution
```java
class Solution{
	public boolean isSubtree(TreeNode root, TreeNode subRoot) {  
	    if(subRoot==null || isSameTree(root,subRoot)){  
	        return true;  
	    }else if(root==null){  
	        return false;  
	    }  
	    return isSubtree(root.left,subRoot) ||  isSubtree(root.right,subRoot);  
	}  
	public boolean isSameTree(TreeNode p,TreeNode q){  
	    if(p==null && q==null) {  
	        return true;  
	    }else if(p==null || q==null){  
	        return false;  
	    }else if(p.val!=q.val){  
	        return false;  
	    }  
	    return isSameTree(p.left,q.left) && isSameTree(p.right,q.right);  
	}
}
```

**Explanation**
1. **isSubtree Function**:
    
    - **Base Cases**:
        - **`subRoot == null`**: If `subRoot` is `null`, it is considered a subtree of `root`, so return `true`.
        - **`isSameTree(root, subRoot)`**: If the `root` tree and `subRoot` tree are the same (as determined by the `isSameTree` function), return `true`.
        - **`root == null`**: If `root` is `null` but `subRoot` is not `null`, `subRoot` can't be a subtree of `root`, so return `false`.
    - **Recursive Calls**:
        - If neither of the base cases is met, recursively check whether `subRoot` is a subtree of `root.left` or `root.right`. If either returns `true`, then `subRoot` is a subtree of `root`.
2. **isSameTree Function**:
    
    - This function checks if two trees (`p` and `q`) are identical, using the same logic as previously described.
    - **Base Cases**:
        - **Both `p` and `q` are `null`**: Return `true`.
        - **One of `p` or `q` is `null`**: Return `false`.
        - **`p.val != q.val`**: If the values of the current nodes differ, return `false`.
    - **Recursive Calls**:
	        - Recursively check the left and right children of both trees. The trees are the same if both the left and right subtrees match.