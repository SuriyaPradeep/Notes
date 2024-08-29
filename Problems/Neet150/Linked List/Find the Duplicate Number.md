#array #linked-list 
### Question
Given an array of integers `nums` containing `n + 1` integers where each integer is in the range `[1, n]` inclusive.

There is only **one repeated number** in `nums`, return _this repeated number_.

You must solve the problem **without** modifying the array `nums` and uses only constant extra space.

**Example 1:**

**Input:** nums = [1,3,4,2,2]
**Output:** 2

**Example 2:**

**Input:** nums = [3,1,3,4,2]
**Output:** 3

**Example 3:**

**Input:** nums = [3,3,3,3,3]
**Output:** 3

### Solution
```java
class Solution{
	public int findDuplicate(int[] nums) {  
	    int slow1,fast;  
	    slow1=fast=nums[0];  
	    do{  
	        slow1=nums[slow1];  
	        fast=nums[nums[fast]];  
	    }while(fast!=slow1);  
	    int slow2=nums[0];  
	    while(slow1!=slow2){  
	        slow1=nums[slow1];  
	        slow2=nums[slow2];  
	    }  
	    return slow1;  
	}
}
```

**Explanation**
1. **Initialization**:
    
    - Both `slow1` and `fast` start at the first element (`nums[0]`).
2. **First Phase (Cycle Detection)**:
    
    - `slow1` and `fast` move through the array at different speeds.
    - Because there is a duplicate, this setup creates a cycle, and `slow1` and `fast` will eventually meet within this cycle.
3. **Second Phase (Finding the Duplicate)**:
    
    - Once a cycle is detected, a new pointer `slow2` is initialized at the start of the array.
    - Both `slow1` and `slow2` move one step at a time. The point at which they meet is the duplicate number.

