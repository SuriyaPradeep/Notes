#tree #queues 
### Question
Given the `root` of a binary tree, return _the level order traversal of its nodes' values_. (i.e., from left to right, level by level).

**Example 1:**

![](https://assets.leetcode.com/uploads/2021/02/19/tree1.jpg)

**Input:** root = [3,9,20,null,null,15,7]
**Output:** [[3],[9,20],[15,7]]

**Example 2:**

**Input:** root = [1]
**Output:** [[1]]

**Example 3:**

**Input:** root = []
**Output:** []

### Solution
```java
class Solution{
	public List<List<Integer>> levelOrder(TreeNode root) {  
	    List<List<Integer>> ans=new ArrayList<>();  
	    Queue<TreeNode> queue=new LinkedList<>();  
	    if(root!=null) {  
	        queue.add(root);  
	    }  
	    while(!queue.isEmpty()){  
	        int size=queue.size();  
	        List<Integer>list=new ArrayList<>();  
	        for(int i=0;i<size;i++){  
	            TreeNode node=queue.poll();  
	            list.add(node.val);  
	            if(node.left!=null){  
	                queue.add(node.left);  
	            }  
	            if(node.right!=null){  
	                queue.add(node.right);  
	            }  
	        }  
	        ans.add(list);  
	    }  
	    return ans;  
	}
}
```

**Explanation**
1. **Initialization**:
    
    - **`ans`**: A list of lists to store the final result. Each inner list corresponds to a level in the tree.
    - **`queue`**: A queue used for the breadth-first search (BFS). It stores nodes to be processed at each level.
2. **Handling the Root**:
    
    - If `root` is not `null`, it is added to the queue. This is the starting point of the BFS.
3. **Breadth-First Search**:
    
    - The while loop runs as long as there are nodes in the queue (i.e., as long as there are levels left to process).
    - **`size = queue.size()`**: The size of the queue is determined at the beginning of each level, representing the number of nodes in the current level.
    - **`list`**: A temporary list to store the values of the nodes at the current level.
    - A for loop iterates over the nodes in the current level:
        - **`queue.poll()`**: The node is dequeued from the front of the queue.
        - The value of the node (`node.val`) is added to `list`.
        - If the node has a left child (`node.left`), it is enqueued for processing in the next level.
        - If the node has a right child (`node.right`), it is also enqueued.
    - After processing all nodes at the current level, the `list` is added to `ans`.
4. **Return the Result**:
    
    - Once all levels have been processed, the `ans` list is returned, which contains the values of the tree's nodes level by level.