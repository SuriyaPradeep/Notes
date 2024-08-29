#linked-list 
### Question
You are given the heads of two sorted linked lists `list1` and `list2`.

Merge the two lists into one **sorted** list. The list should be made by splicing together the nodes of the first two lists.

Return _the head of the merged linked list_.

**Example 1:**

![](https://assets.leetcode.com/uploads/2020/10/03/merge_ex1.jpg)

**Input:** list1 = [1,2,4], list2 = [1,3,4]
**Output:** [1,1,2,3,4,4]

**Example 2:**

**Input:** list1 = [], list2 = []
**Output:** []

**Example 3:**

**Input:** list1 = [], list2 = [0]
**Output:** [0]

### Solution
```java
class Solution{
	public ListNode mergeTwoLists(ListNode list1, ListNode list2) {  
	    ListNode dummy=new ListNode(0),curr=dummy;  
	    while(list1!=null && list2!=null){  
	        ListNode node=null;  
	        if(list1.val<=list2.val){  
	            node=list1;  
	            list1=list1.next;  
	        }else{  
	            node=list2;  
	            list2=list2.next;  
	        }  
	        curr.next=node;  
	        curr=curr.next;  
	    }  
	    while(list1!=null){  
	        curr.next=list1;  
	        curr=curr.next;  
	        list1=list1.next;  
	    }  
	    while(list2!=null){  
	        curr.next=list2;  
	        curr=curr.next;  
	        list2=list2.next;  
	    }  
	    return dummy.next;  
	}
}
```

**Explanation**
1. **Initialization**:
    
    - `dummy` is a dummy node to simplify edge cases and provide an easy return point.
    - `curr` is a pointer to build the new list starting from the dummy node.
2. **Merge Lists While Both Have Elements**:
    
    - The loop continues while both `list1` and `list2` are not `null`.
    - Compare the current nodes of `list1` and `list2`.
    - Append the smaller node to the merged list and move the pointer of the chosen list forward.
3. **Append Remaining Elements**:
    
    - If `list1` still has elements, append all remaining nodes to the merged list.
    - If `list2` still has elements, append all remaining nodes to the merged list.
4. **Return the Merged List**:
    
    - The merged list starts from `dummy.next`.