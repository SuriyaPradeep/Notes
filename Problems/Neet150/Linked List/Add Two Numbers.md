#linked-list 
### Question
You are given two **non-empty** linked lists representing two non-negative integers. The digits are stored in **reverse order**, and each of their nodes contains a single digit. Add the two numbers and return the sum as a linked list.

You may assume the two numbers do not contain any leading zero, except the number 0 itself.

**Example 1:**

![](https://assets.leetcode.com/uploads/2020/10/02/addtwonumber1.jpg)

**Input:** l1 = [2,4,3], l2 = [5,6,4]
**Output:** [7,0,8]
**Explanation:** 342 + 465 = 807.

**Example 2:**

**Input:** l1 = [0], l2 = [0]
**Output:** [0]

**Example 3:**

**Input:** l1 = [9,9,9,9,9,9,9], l2 = [9,9,9,9]
**Output:** [8,9,9,9,0,0,0,1]

### Solution
```java
class Solution{
	public ListNode addTwoNumbers(ListNode l1, ListNode l2) {  
	    ListNode dummy=new ListNode(0),curr=dummy;  
	    int carryOn=0;  
	    while(l1!=null || l2!=null || carryOn!=0){  
	        int val1=l1==null?0:l1.val;  
	        int val2=l2==null?0:l2.val;  
	        int sum=val1+val2+carryOn;  
	        int digit=(sum%10);  
	        carryOn=sum/10;  
	        curr.next=new ListNode(digit);  
	        curr=curr.next;  
	        l1=l1==null?null:l1.next;  
	        l2=l2==null?null:l2.next;  
	    }  
	    return dummy.next;  
	}
}
```

**Explanation**
1. **Initialization**:
    
    - `dummy` is a dummy node to simplify the code for returning the result.
    - `curr` is a pointer to traverse and build the new list.
    - `carryOn` is used to handle the carry for summation.
2. **While Loop**:
    
    - The loop continues as long as there are nodes in either `l1` or `l2`, or there is a carry to process.
    - `val1` and `val2` get the values of the current nodes of `l1` and `l2` or 0 if the respective node is `null`.
    - `sum` is the sum of `val1`, `val2`, and `carryOn`.
    - `digit` is the single digit to be stored in the new node.
    - `carryOn` is updated to the carry for the next iteration.
    - A new node with the value of `digit` is created and linked to `curr.next`.
    - `curr` is moved to the next node.
    - `l1` and `l2` are moved to their next nodes if they are not `null`.
3. **Return**:
    
    - The result is `dummy.next` since `dummy` was a placeholder node.