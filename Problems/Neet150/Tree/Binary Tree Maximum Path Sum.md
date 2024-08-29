#tree #recursion 
### Question
A **path** in a binary tree is a sequence of nodes where each pair of adjacent nodes in the sequence has an edge connecting them. A node can only appear in the sequence **at most once**. Note that the path does not need to pass through the root.

The **path sum** of a path is the sum of the node's values in the path.

Given the `root` of a binary tree, return _the maximum **path sum** of any **non-empty** path_.

**Example 1:**

![](https://assets.leetcode.com/uploads/2020/10/13/exx1.jpg)

**Input:** root = [1,2,3]
**Output:** 6
**Explanation:** The optimal path is 2 -> 1 -> 3 with a path sum of 2 + 1 + 3 = 6.

**Example 2:**

![](https://assets.leetcode.com/uploads/2020/10/13/exx2.jpg)

**Input:** root = [-10,9,20,null,null,15,7]
**Output:** 42
**Explanation:** The optimal path is 15 -> 20 -> 7 with a path sum of 15 + 20 + 7 = 42.

### Solution
```java
class Solution{
	public int maxPathSum(TreeNode root) {  
	    int[] res=new int[1];  
	    res[0]=Integer.MIN_VALUE;  
	    maxSum(root,res);  
	    return res[0];  
	}  
	public int maxSum(TreeNode root,int[] res){  
	    if(root==null){  
	        return 0;  
	    }  
	    int left=Math.max(0,maxSum(root.left,res));  
	    int right=Math.max(0,maxSum(root.right,res));  
	    res[0]=Math.max(res[0],(root.val+left+right));  
	    return root.val+Math.max(left,right);  
	}
}
```

**Explanation**
1. **Instance Variables**:
    
    - `int[] res = new int[1];`: `res` is an array used to store the maximum path sum found during the traversal. Since arrays are mutable, this allows the value to be updated within recursive calls.
    - `res[0] = Integer.MIN_VALUE;`: This initializes the maximum path sum to the smallest possible value to ensure that any valid path sum will be larger.
2. **`maxPathSum(TreeNode root)`**:
    
    - This method is the entry point for calculating the maximum path sum. It initializes the `res` array and calls the `maxSum` method to perform the actual computation.
    - It returns the maximum path sum stored in `res[0]`.
3. **`maxSum(TreeNode root, int[] res)`**:
    
    - **Base Case**: If the current node (`root`) is `null`, the method returns `0`, indicating that there is no contribution to the path sum from a non-existent node.
    - **Recursive Case**:
        - It recursively calculates the maximum path sums for the left and right subtrees (`left` and `right`). The `Math.max(0, ...)` ensures that negative sums are ignored.
        - The overall maximum path sum is updated by considering the sum of the current node’s value and the maximum sums of both left and right subtrees.
        - Finally, the method returns the maximum sum of the current node's value and either the left or right subtree. This ensures that the returned value represents the maximum sum path that continues through the parent node.