#linked-list #sorting #priority-queue 
### Question
You are given an array of `k` linked-lists `lists`, each linked-list is sorted in ascending order.

_Merge all the linked-lists into one sorted linked-list and return it._

**Example 1:**

**Input:** lists = [[1,4,5],[1,3,4],[2,6]]
**Output:** [1,1,2,3,4,4,5,6]
**Explanation:** The linked-lists are:
[
  1->4->5,
  1->3->4,
  2->6
]
merging them into one sorted list:
1->1->2->3->4->4->5->6

**Example 2:**

**Input:** lists = []
**Output:** []

**Example 3:**

**Input:** lists = [[]]
**Output:** []

### Solution
```java
class Solution{
	public ListNode mergeKLists(ListNode[] lists) {  
	    PriorityQueue<ListNode> pq=new PriorityQueue<>((a,b)->a.val-b.val);  
	    for(ListNode node:lists){  
	        if(node!=null){  
	            pq.add(node);  
	        }  
	    }  
	    ListNode dummy=new ListNode(0),curr=dummy;  
	    while(!pq.isEmpty()){  
	        ListNode node=pq.poll();  
	        curr.next=node;  
	        curr=curr.next;  
	        if(node.next!=null){  
	            pq.add(node.next);  
	        }  
	    }  
	    return dummy.next;  
	}
}
```

**Explanation**
1. **Priority Queue Initialization**:
    
    - You initialize a priority queue (min-heap) that orders the `ListNode` objects based on their values.
2. **Adding Initial Nodes to the Priority Queue**:
    
    - You iterate through the input array of `ListNode` objects (`lists`). If a list head is not null, you add it to the priority queue.
3. **Merging Process**:
    
    - You create a dummy node to serve as the starting point of the merged list.
    - While the priority queue is not empty, you extract the node with the smallest value from the queue.
    - Attach this node to the current end of the merged list (`curr.next = node`).
    - Move the `curr` pointer to this node.
    - If the extracted node has a next node, add that next node to the priority queue.
4. **Return the Merged List**:
    
    - After processing all nodes, the dummy node's next pointer points to the head of the merged list, which you return.
