#linked-list 
### Question
Given the `head` of a linked list, remove the `nth` node from the end of the list and return its head.

**Example 1:**

![](https://assets.leetcode.com/uploads/2020/10/03/remove_ex1.jpg)

**Input:** head = [1,2,3,4,5], n = 2
**Output:** [1,2,3,5]

**Example 2:**

**Input:** head = [1], n = 1
**Output:** []

**Example 3:**

**Input:** head = [1,2], n = 1
**Output:** [1]


### Solution
```java
class Solution{
	public ListNode removeNthFromEnd(ListNode head, int n) {  
	    ListNode dummy=new ListNode(0);  
	    dummy.next=head;  
	    ListNode cur1=dummy;  
	    for(int i=0;i<n;i++){  
	        cur1=cur1.next;  
	    }  
	    ListNode cur2=dummy;  
	    while(cur1.next!=null){  
	        cur1=cur1.next;  
	        cur2=cur2.next;  
	    }  
	    cur2.next=cur2.next.next;  
	    return dummy.next;  
	}
}
```

**Explanation**
1. **Initialization**:
    
    - `dummy` is a dummy node to handle edge cases where the head might be removed. It points to the original `head`.
    - `cur1` and `cur2` are pointers initialized to `dummy`.
2. **Advance `cur1` by `n` Steps**:
    
    - Move `cur1` `n` steps ahead in the list. This creates a gap of `n` nodes between `cur1` and `cur2`.
3. **Move Both Pointers Until `cur1` Reaches the End**:
    
    - Move `cur1` and `cur2` simultaneously until `cur1` reaches the end of the list. At this point, `cur2` will be pointing to the node just before the node that needs to be removed.
4. **Remove the N-th Node from the End**:
    
    - Adjust the `next` pointer of `cur2` to skip the N-th node from the end, effectively removing it from the list.
5. **Return the Modified List**:
    
    - Return `dummy.next`, which points to the new head of the list.