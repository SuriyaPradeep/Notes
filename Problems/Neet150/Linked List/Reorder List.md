#linked-list 
### Question
You are given the head of a singly linked-list. The list can be represented as:

L0 → L1 → … → Ln - 1 → Ln

_Reorder the list to be on the following form:_

L0 → Ln → L1 → Ln - 1 → L2 → Ln - 2 → …

You may not modify the values in the list's nodes. Only nodes themselves may be changed.

**Example 1:**

![](https://assets.leetcode.com/uploads/2021/03/04/reorder1linked-list.jpg)

**Input:** head = [1,2,3,4]
**Output:** [1,4,2,3]

**Example 2:**

![](https://assets.leetcode.com/uploads/2021/03/09/reorder2-linked-list.jpg)

**Input:** head = [1,2,3,4,5]
**Output:** [1,5,2,4,3]

### Solution
```java
class Solution{
	public void reorderList(ListNode head) {  
	    ListNode slow=head,fast=head;  
	    while(fast!=null && fast.next!=null){  
	        slow=slow.next;  
	        fast=fast.next.next;  
	    }  
	    ListNode head2=slow.next;  
	    slow.next=null;  
	    ListNode prev=null;  
	    while(head2!=null){  
	        ListNode next=head2.next;  
	        head2.next=prev;  
	        prev=head2;  
	        head2=next;  
	    }  
	    head2=prev;  
	    ListNode cur1=head,cur2=head2;  
	    while(cur1!=null && cur2!=null){  
	        ListNode next1=cur1.next;  
	        ListNode next2=cur2.next;  
	        cur1.next=cur2;  
	        cur2.next=next1;  
	        cur1=next1;  
	        cur2=next2;  
	    }  
	}
}
```

**Explanation**
1. **Finding the Middle of the List**:
    
    - You use two pointers, `slow` and `fast`, to find the middle of the list. The `fast` pointer moves twice as fast as the `slow` pointer. When `fast` reaches the end of the list, `slow` will be at the middle.
2. **Splitting the List**:
    
    - After finding the middle, you split the list into two halves. `head2` points to the start of the second half, and you break the link between the two halves by setting `slow.next` to `null`.
3. **Reversing the Second Half**:
    
    - You reverse the second half of the list. `prev` is used to build the reversed list.
4. **Merging the Two Halves**:
    
    - You merge the two halves by alternating nodes from each half.