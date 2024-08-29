#tree #recursion 
Given the `root` of a binary tree, invert the tree, and return _its root_.

**Example 1:**

![](https://assets.leetcode.com/uploads/2021/03/14/invert1-tree.jpg)

**Input:** root = [4,2,7,1,3,6,9]
**Output:** [4,7,2,9,6,3,1]

**Example 2:**

![](https://assets.leetcode.com/uploads/2021/03/14/invert2-tree.jpg)

**Input:** root = [2,1,3]
**Output:** [2,3,1]

**Example 3:**

	**Input:** root = []
**Output:** []

### Solution
```java
class Solution{
	public TreeNode invertTree(TreeNode root) {  
	    if(root==null){  
	        return null;  
	    }  
	    TreeNode node=new TreeNode(root.val);  
	    TreeNode right=invertTree(root.left);  
	    TreeNode left=invertTree(root.right);  
	    root.right=right;  
	    root.left=left;  
	    return root;  
	}
}
```

**Explanation**
1. **Base Case (Line 3-5):**
    
    - The function first checks if `root` is `null`. If it is, it returns `null`. This is the base case for the recursion and handles the scenario when the tree is empty or when the recursion reaches a leaf node's child.
2. **Create a New Node (Line 6):**
    
    - A new `TreeNode` named `node` is created with the value of the `root`. However, this new node isn't used in the inversion process and thus is unnecessary for inverting the tree.
3. **Recursive Inversion (Line 7-8):**
    
    - The function calls itself recursively to invert the left subtree (`invertTree(root.left)`) and stores the result in the variable `right`.
    - Similarly, it inverts the right subtree (`invertTree(root.right)`) and stores the result in the variable `left`.
4. **Swapping Children (Line 9-10):**
    
    - After inverting the left and right subtrees, it swaps the left and right children of the `root`. This means the original left subtree becomes the right subtree, and the original right subtree becomes the left subtree.
5. **Return (Line 11):**
    
    - Finally, the function returns the `root`, which now has its left and right children swapped. This completes the inversion for the current subtree.
