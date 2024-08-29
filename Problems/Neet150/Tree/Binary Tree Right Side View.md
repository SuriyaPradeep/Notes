#tree #queues 
Given the `root` of a binary tree, imagine yourself standing on the **right side** of it, return _the values of the nodes you can see ordered from top to bottom_.

**Example 1:**

![](https://assets.leetcode.com/uploads/2021/02/14/tree.jpg)

**Input:** root = [1,2,3,null,5,null,4]
**Output:** [1,3,4]

**Example 2:**

**Input:** root = [1,null,3]
**Output:** [1,3]

**Example 3:**

**Input:** root = []
**Output:** []

### Solution
```java
class Solution{
	public List<Integer> rightSideView(TreeNode root) {  
	    Queue<TreeNode> queue=new LinkedList<>();  
	    List<Integer> ans=new ArrayList<>();  
	    if(root!=null){  
	        queue.add(root);  
	    }  
	    while(!queue.isEmpty()){  
	        int size=queue.size();  
	        for(int i=0;i<size;i++){  
	            TreeNode curr=queue.poll();  
	            if(i==size-1){  
	                ans.add(curr.val);  
	            }  
	            if(curr.left!=null){  
	                queue.add(curr.left);  
	            }  
	            if(curr.right!=null){  
	                queue.add(curr.right);  
	            }  
	        }  
	    }  
	    return ans;  
	}
}
```

**Explanation**
- **Queue Initialization**:
    
    - A `Queue` is used to perform a level-order traversal (BFS) of the tree.
    - A `List<Integer>` named `ans` is initialized to store the nodes visible from the right side.
- **Root Check**:
    
    - If the `root` is not null, it is added to the queue. This is the first step in starting the traversal.
- **Level-Order Traversal**:
    
    - The outer `while` loop runs as long as there are nodes in the queue, meaning the tree still has levels to process.
    - `int size=queue.size();` stores the number of nodes at the current level.
- **Processing Each Level**:
    
    - The inner `for` loop iterates over each node at the current level.
    - `TreeNode curr=queue.poll();` retrieves and removes the node at the front of the queue.
    - If `i == size - 1`, it means the current node is the last node of the current level, and its value is added to the `ans` list.
- **Enqueue Children**:
    
    - The left child of the current node is added to the queue if it exists.
    - The right child of the current node is added to the queue if it exists.
- **Return the Right Side View**:
    
    - After processing all levels of the tree, the `ans` list is returned, containing the values of the nodes visible from the right side.