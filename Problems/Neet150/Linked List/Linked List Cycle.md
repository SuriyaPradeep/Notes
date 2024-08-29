#linked-list 
### Question
Given `head`, the head of a linked list, determine if the linked list has a cycle in it.

There is a cycle in a linked list if there is some node in the list that can be reached again by continuously following the `next` pointer. Internally, `pos` is used to denote the index of the node that tail's `next` pointer is connected to. **Note that `pos` is not passed as a parameter**.

Return `true` _if there is a cycle in the linked list_. Otherwise, return `false`.

**Example 1:**

![](https://assets.leetcode.com/uploads/2018/12/07/circularlinkedlist.png)

**Input:** head = [3,2,0,-4], pos = 1
**Output:** true
**Explanation:** There is a cycle in the linked list, where the tail connects to the 1st node (0-indexed).

**Example 2:**

![](https://assets.leetcode.com/uploads/2018/12/07/circularlinkedlist_test2.png)

**Input:** head = [1,2], pos = 0
**Output:** true
**Explanation:** There is a cycle in the linked list, where the tail connects to the 0th node.

**Example 3:**

![](https://assets.leetcode.com/uploads/2018/12/07/circularlinkedlist_test3.png)

**Input:** head = [1], pos = -1
**Output:** false
**Explanation:** There is no cycle in the linked list.

### Solution
```java
class Solution{
	public boolean hasCycle(ListNode head) {  
	    ListNode slow,fast;  
	    slow=fast=head;  
	    while(fast!=null && fast.next!=null){  
	        slow=slow.next;  
	        fast=fast.next.next;  
	        if(slow==fast){  
	            return true;  
	        }  
	    }  
	    return false;  
	}
}
```

**Explanation**
1. **Initialize Pointers**:
    
    - Two pointers, `slow` and `fast`, are both initialized to the head of the list. The `slow` pointer will move one step at a time, while the `fast` pointer will move two steps at a time.
2. **Traverse the List**:
    
    - You traverse the list with a `while` loop that continues as long as `fast` and `fast.next` are not null.
    - In each iteration, move `slow` one step forward and `fast` two steps forward.
    - If at any point `slow` and `fast` meet, it means there is a cycle in the list, and you return `true`.
3. **No Cycle Detected**:
    
    - If the loop exits, it means `fast` or `fast.next` reached null, indicating the end of the list and no cycle. You return `false`.
