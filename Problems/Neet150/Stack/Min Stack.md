#stack 
### Question
Design a stack that supports push, pop, top, and retrieving the minimum element in constant time.

Implement the `MinStack` class:

- `MinStack()` initializes the stack object.
- `void push(int val)` pushes the element `val` onto the stack.
- `void pop()` removes the element on the top of the stack.
- `int top()` gets the top element of the stack.
- `int getMin()` retrieves the minimum element in the stack.

You must implement a solution with `O(1)` time complexity for each function.

**Example 1:**

**Input**
["MinStack","push","push","push","getMin","pop","top","getMin"]
[[],[-2],[0],[-3],[],[],[],[]]

**Output**
[null,null,null,null,-3,null,0,-2]

**Explanation**
MinStack minStack = new MinStack();
minStack.push(-2);
minStack.push(0);
minStack.push(-3);
minStack.getMin(); // return -3
minStack.pop();
minStack.top();    // return 0
minStack.getMin(); // return -2


### Solution
```java
class Solution{
	class Node{  
	    int val;  
	    int min;  
	    Node next;  
	    public Node(int val,int min,Node next){  
	        this.val=val;  
	        this.min=min;  
	        this.next=next;  
	    }  
	}  
	Node head;  
	public MinStack() {  
	    head=null;  
	}  
	  
	public void push(int val) {  
	    if(head==null){  
	        head=new Node(val,val,null);  
	    }else{  
	        head=new Node(val,Math.min(head.min,val),head);  
	    }  
	}  
	  
	public void pop() {  
	    if(head!=null){  
	        head=head.next;  
	    }  
	}  
	  
	public int top() {  
	    if(head!=null){  
	        return head.val;  
	    }  
	    return -1;  
	}  
	  
	public int getMin() {  
	    if(head!=null){  
	        return head.min;  
	    }  
	    return -1;  
	}
}
```

**Explanation**
**Class Definitions and Fields**

1. **Node Class**:
    
    - The `Node` class contains three fields: `val` for the node's value, `min` for the minimum value up to that node, and `next` for the reference to the next node.
    - The constructor initializes these fields.
2. **MinStack Class**:
    
    - The `MinStack` class has a single field `head`, which is a reference to the top node of the stack.

**Methods**

1. **Constructor**:
    
    - `public MinStack()`: Initializes the `head` to `null`, indicating an empty stack.
2. **push**:
    
    - `public void push(int val)`: Adds a new node to the stack. If the stack is empty, the new node's `min` value is set to its `val`. Otherwise, the new node's `min` value is the minimum of the current head's `min` value and the new value.
3. **pop**:
    
    - `public void pop()`: Removes the top node from the stack by setting the `head` to the `next` node. This operation effectively removes the reference to the current top node, allowing it to be garbage collected.
4. **top**:
    
    - `public int top()`: Returns the value of the top node. If the stack is empty, it returns `-1`.
5. **getMin**:
    
    - `public int getMin()`: Returns the minimum value in the stack. If the stack is empty, it returns `-1`.