#tree #bst #recursion 
### Question
Given a binary search tree (BST), find the lowest common ancestor (LCA) node of two given nodes in the BST.

According to the [definition of LCA on Wikipedia](https://en.wikipedia.org/wiki/Lowest_common_ancestor): “The lowest common ancestor is defined between two nodes `p` and `q` as the lowest node in `T` that has both `p` and `q` as descendants (where we allow **a node to be a descendant of itself**).”

**Example 1:**

![](https://assets.leetcode.com/uploads/2018/12/14/binarysearchtree_improved.png)

**Input:** root = [6,2,8,0,4,7,9,null,null,3,5], p = 2, q = 8
**Output:** 6
**Explanation:** The LCA of nodes 2 and 8 is 6.

**Example 2:**

![](https://assets.leetcode.com/uploads/2018/12/14/binarysearchtree_improved.png)

**Input:** root = [6,2,8,0,4,7,9,null,null,3,5], p = 2, q = 4
**Output:** 2
**Explanation:** The LCA of nodes 2 and 4 is 2, since a node can be a descendant of itself according to the LCA definition.

**Example 3:**

**Input:** root = [2,1], p = 2, q = 1
**Output:** 2

### Solution
```java
class Solution{
	public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {  
	    if(p.val<root.val && q.val<root.val){  
	        return lowestCommonAncestor(root.left,p,q);  
	    }else if(p.val>root.val && q.val>root.val){  
	        return lowestCommonAncestor(root.right,p,q);  
	    }  
	    return root;  
	}
}
```

**Explanation**
1. **Understanding the BST Property**:
    
    - In a BST, for any node `root`, all nodes in the left subtree of `root` have values less than `root.val`, and all nodes in the right subtree have values greater than `root.val`.
2. **Base Cases**:
    
    - **Both `p` and `q` are smaller than `root`**:
        - If both `p.val` and `q.val` are less than `root.val`, then the LCA must be in the left subtree. Therefore, the function recursively calls itself with `root.left`.
    - **Both `p` and `q` are larger than `root`**:
        - If both `p.val` and `q.val` are greater than `root.val`, then the LCA must be in the right subtree. So, the function recursively calls itself with `root.right`.
    - **Nodes are on different sides**:
        - If `p` and `q` lie on different sides of `root` (i.e., one is smaller and one is larger), then `root` is the LCA. This is because one node lies in the left subtree and the other in the right subtree, meaning `root` is the common ancestor at the lowest level.
3. **Returning the LCA**:
    
    - When the code finds that `p` and `q` are on different sides of `root`, or if one of them is equal to `root`, it returns `root` as the LCA.