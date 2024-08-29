#linked-list 
### Question
A linked list of length `n` is given such that each node contains an additional random pointer, which could point to any node in the list, or `null`.

Construct a [**deep copy**](https://en.wikipedia.org/wiki/Object_copying#Deep_copy) of the list. The deep copy should consist of exactly `n` **brand new** nodes, where each new node has its value set to the value of its corresponding original node. Both the `next` and `random` pointer of the new nodes should point to new nodes in the copied list such that the pointers in the original list and copied list represent the same list state. **None of the pointers in the new list should point to nodes in the original list**.

For example, if there are two nodes `X` and `Y` in the original list, where `X.random --> Y`, then for the corresponding two nodes `x` and `y` in the copied list, `x.random --> y`.

Return _the head of the copied linked list_.

The linked list is represented in the input/output as a list of `n` nodes. Each node is represented as a pair of `[val, random_index]` where:

- `val`: an integer representing `Node.val`
- `random_index`: the index of the node (range from `0` to `n-1`) that the `random` pointer points to, or `null` if it does not point to any node.

Your code will **only** be given the `head` of the original linked list.

**Example 1:**

![](https://assets.leetcode.com/uploads/2019/12/18/e1.png)

**Input:** head = [[7,null],[13,0],[11,4],[10,2],[1,0]]
**Output:** [[7,null],[13,0],[11,4],[10,2],[1,0]]

**Example 2:**

![](https://assets.leetcode.com/uploads/2019/12/18/e2.png)

**Input:** head = [[1,1],[2,1]]
**Output:** [[1,1],[2,1]]

**Example 3:**

**![](https://assets.leetcode.com/uploads/2019/12/18/e3.png)**

**Input:** head = [[3,null],[3,0],[3,null]]
**Output:** [[3,null],[3,0],[3,null]]


### Solution
```java
class Solution{
	private class Node{  
	    int val;  
	    Node next;  
	    Node random;  
	    public Node(int val) {  
	        this.val = val;  
	        this.next = null;  
	        this.random = null;  
	    }  
	}  
	public Node copyRandomList(Node head) {  
	    HashMap<Node,Node>hashMap=new HashMap<>();  
	    Node curr=head;  
	    while(curr!=null){  
	        hashMap.put(curr,new Node(curr.val));  
	        curr=curr.next;  
	    }  
	    curr=head;  
	    while(curr!=null){  
	        hashMap.get(curr).next=hashMap.get(curr.next);  
	        hashMap.get(curr).random=hashMap.get(curr.random);  
	        curr=curr.next;  
	    }  
	    return hashMap.get(head);  
	}
}
```

**Explanation**
1. **Node Class**:
    
    - A `Node` class with an integer value `val`, and two pointers `next` and `random`.
2. **First Pass**:
    
    - Traverse the original list and create a new node for each original node, storing these new nodes in a hash map where the key is the original node and the value is the new node.
3. **Second Pass**:
    
    - Traverse the original list again to set the `next` and `random` pointers for each new node using the hash map.
4. **Return**:
    
    - Return the new head node, which is the copy of the original head node.