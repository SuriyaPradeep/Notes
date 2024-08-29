#linked-list 
### Question
Given the `head` of a singly linked list, reverse the list, and return _the reversed list_.

**Example 1:**

![](https://assets.leetcode.com/uploads/2021/02/19/rev1ex1.jpg)

**Input:** head = [1,2,3,4,5]
**Output:** [5,4,3,2,1]

**Example 2:**

![](https://assets.leetcode.com/uploads/2021/02/19/rev1ex2.jpg)

**Input:** head = [1,2]
**Output:** [2,1]

**Example 3:**

**Input:** head = []
**Output:** []

### Solution
```java
class Solution{
	public ListNode reverseList(ListNode head) {  
	    ListNode prev=null;  
	    while(head!=null){  
	        ListNode next=head.next;  
	        head.next=prev;  
	        prev=head;  
	        head=next;  
	    }  
	    head=prev;  
	    return head;  
	}
}
```

**Explanation**
1. **Initialization**:
    
    - `prev` is initialized to `null`. This will eventually become the new head of the reversed list.
    - `head` is the current node being processed.
2. **Iterative Reversal**:
    
    - The loop runs until `head` becomes `null`, indicating the end of the list.
    - Inside the loop:
        - `next` stores the next node in the original list (`head.next`).
        - `head.next` is set to `prev` to reverse the link.
        - Move `prev` to the current node (`head`).
        - Move `head` to the next node (`next`).
3. **Update and Return New Head**:
    
    - After the loop, `prev` points to the new head of the reversed list.
    - Update `head` to point to `prev` (the new head).
    - Return the new head.

