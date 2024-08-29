#linked-list #recursion 
### Question
Given the `head` of a linked list, reverse the nodes of the list `k` at a time, and return _the modified list_.

`k` is a positive integer and is less than or equal to the length of the linked list. If the number of nodes is not a multiple of `k` then left-out nodes, in the end, should remain as it is.

You may not alter the values in the list's nodes, only nodes themselves may be changed.

**Example 1:**

![](https://assets.leetcode.com/uploads/2020/10/03/reverse_ex1.jpg)

**Input:** head = [1,2,3,4,5], k = 2
**Output:** [2,1,4,3,5]

**Example 2:**

![](https://assets.leetcode.com/uploads/2020/10/03/reverse_ex2.jpg)

**Input:** head = [1,2,3,4,5], k = 3
**Output:** [3,2,1,4,5]

### Solution
```java
class Solution{
	public ListNode reverseKGroup(ListNode head, int k) {  
	    int count=0;  
	    ListNode curr=head;  
	    while(curr!=null && count!=k){  
	        curr=curr.next;  
	        count++;  
	    }  
	    if(count==k){  
	        curr=reverseKGroup(curr,k);  
	        while(count>0){  
	            ListNode next=head.next;  
	            head.next=curr;  
	            curr=head;  
	            head=next;  
	            count--;  
	        }  
	        head=curr;  
	    }  
	    return head;  
	}
}
```

**Explanation**
1. **Counting Nodes**:
    
    - The function starts by checking if there are at least `k` nodes left in the list.
    - It initializes a counter (`count`) and iterates through the list (`curr = curr.next`) up to `k` times or until the end of the list is reached.
    - If `count` equals `k`, it means there are `k` nodes available to reverse.
2. **Recursive Call**:
    
    - If there are exactly `k` nodes, it makes a recursive call `reverseKGroup(curr, k)` to reverse the next segment of `k` nodes.
    - The result of this recursive call (`curr`) will be the new head of the remaining list after reversing.
3. **Reversing k Nodes**:
    
    - After the recursive call, the function proceeds to reverse the current `k` nodes.
    - It uses a while loop (`while (count > 0)`) to reverse the nodes by adjusting their `next` pointers.
    - In each iteration:
        - It saves the next node (`ListNode next = head.next`).
        - It changes the `next` pointer of the current node (`head`) to point to the result of the recursive call (`head.next = curr`).
        - It moves the `curr` pointer to the current node (`curr = head`).
        - It advances the `head` pointer to the saved next node (`head = next`).
        - It decrements the `count`.
4. **Adjusting Head**:
    
    - After the loop, the `head` pointer is adjusted to point to the new head of the reversed sublist (`head = curr`).
5. **Returning the New Head**:
    
    - Finally, the function returns the new head of the list, which is the result of reversing the first `k` nodes and connecting them to the result of the recursive call for the rest of the list.