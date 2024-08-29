#tree #recursion 
### Question
Given a binary tree `root`, a node _X_ in the tree is named **good** if in the path from root to _X_ there are no nodes with a value _greater than_ X.

Return the number of **good** nodes in the binary tree.

**Example 1:**

**![](https://assets.leetcode.com/uploads/2020/04/02/test_sample_1.png)**

**Input:** root = [3,1,4,3,null,1,5]
**Output:** 4
**Explanation:** Nodes in blue are **good**.
Root Node (3) is always a good node.
Node 4 -> (3,4) is the maximum value in the path starting from the root.
Node 5 -> (3,4,5) is the maximum value in the path
Node 3 -> (3,1,3) is the maximum value in the path.

**Example 2:**

**![](https://assets.leetcode.com/uploads/2020/04/02/test_sample_2.png)**

**Input:** root = [3,3,null,4,2]
**Output:** 3
**Explanation:** Node 2 -> (3, 3, 2) is not good, because "3" is higher than it.

**Example 3:**

**Input:** root = [1]
**Output:** 1
**Explanation:** Root is considered as **good**.

### Solution
```java
class Solution{
	public int goodNodes(TreeNode root) {  
	    return dfs(root,Integer.MIN_VALUE);  
	}  
	public int dfs(TreeNode root,int max){  
	    if(root==null){  
	        return 0;  
	    }  
	    int res=root.val>max?1:0;  
	    res+=dfs(root.left,Math.max(root.val,max));  
	    res+=dfs(root.right,Math.max(root.val,max));  
	    return res;  
	}
}
```