#tree #bst  #sorting #topK 
### Question
Given the `root` of a binary search tree, and an integer `k`, return _the_ `kth` _smallest value (**1-indexed**) of all the values of the nodes in the tree_.

**Example 1:**

![](https://assets.leetcode.com/uploads/2021/01/28/kthtree1.jpg)

**Input:** root = [3,1,4,null,2], k = 1
**Output:** 1

**Example 2:**

![](https://assets.leetcode.com/uploads/2021/01/28/kthtree2.jpg)

**Input:** root = [5,3,6,2,4,null,null,1], k = 3
**Output:** 3

### Solution
```java
class Solution{
	public int kthSmallest(TreeNode root, int k) {  
	    List<Integer> res=new ArrayList<>();  
	    inorder(root,res);  
	    return res.get(k-1);  
	}  
	public void inorder(TreeNode root,List<Integer> res){  
	    if(root!=null){  
	        inorder(root.left,res);  
	        res.add(root.val);  
	        inorder(root.right,res);  
	    }  
	}
}
```
**Explanation**
- **In-order Traversal**:
    
    - The method `inorder` is a recursive function that traverses the tree in in-order (left -> root -> right).
    - It adds each node's value to the `res` list as it traverses the tree.
- **Finding the k-th Smallest Element**:
    
    - After the in-order traversal is complete, the list `res` contains all the elements of the tree in sorted order.
    - The `k`th smallest element in this list corresponds to the `(k-1)`th index, so the function returns `res.get(k-1)`.

