#tree #recursion 
### Question\
Given the roots of two binary trees `p` and `q`, write a function to check if they are the same or not.

Two binary trees are considered the same if they are structurally identical, and the nodes have the same value.

**Example 1:**

![](https://assets.leetcode.com/uploads/2020/12/20/ex1.jpg)

**Input:** p = [1,2,3], q = [1,2,3]
**Output:** true

**Example 2:**

![](https://assets.leetcode.com/uploads/2020/12/20/ex2.jpg)

**Input:** p = [1,2], q = [1,null,2]
**Output:** false

**Example 3:**

![](https://assets.leetcode.com/uploads/2020/12/20/ex3.jpg)

**Input:** p = [1,2,1], q = [1,1,2]
**Output:** false

### Solution
```java
class Solution{
	public boolean isSameTree(TreeNode p, TreeNode q) {  
	    if(p==null && q==null){  
	        return true;  
	    }else if(p==null || q==null){  
	        return false;  
	    }else if (p.val!=q.val){  
	        return false;  
	    }  
	    return isSameTree(p.right,q.right)&&isSameTree(p.left,q.left);  
	}
}
```

**Explanation**
1. **Base Cases**:
    
    - **Both `p` and `q` are `null`**: If both nodes are `null`, the trees are the same up to this point, so return `true`.
    - **One of `p` or `q` is `null`**: If one of the nodes is `null` and the other is not, the trees differ, so return `false`.
    - **Node values differ**: If the values of the current nodes `p` and `q` are different, return `false`.
2. **Recursive Check**:
    
    - If the current nodes are not `null` and their values are equal, recursively check the left subtrees (`p.left` vs `q.left`) and the right subtrees (`p.right` vs `q.right`).
    - Both recursive checks must return `true` for the trees to be considered the same.