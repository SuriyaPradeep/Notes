#priority-queue #topK 
### Question
Given an integer array `nums` and an integer `k`, return _the_ `kth` _largest element in the array_.

Note that it is the `kth` largest element in the sorted order, not the `kth` distinct element.

Can you solve it without sorting?

**Example 1:**

**Input:** nums = [3,2,1,5,6,4], k = 2
**Output:** 5

**Example 2:**

**Input:** nums = [3,2,3,1,2,4,5,5,6], k = 4
**Output:** 4

### Solution
```java
class Solution{
	public int findKthLargest(int[] nums, int k) {  
	    Queue<Integer> pq=new PriorityQueue<>((a,b)->b-a);  
	    for(int num:nums){  
	        pq.add(num);  
	    }  
	    for(int i=0;i<k-1;i++){  
	        pq.poll();  
	    }  
	    return pq.poll();  
	}
}
```

**Explanation**
- **Using a Max-Heap:**
    
    - A max-heap (a type of priority queue where the largest element is always at the top) can be used to solve this problem.
    - First, insert all elements of the array into the max-heap.
    - The max-heap will automatically keep the largest element at the top.
    - Then, remove the top element (the largest) from the heap `k-1` times. After these removals, the element at the top of the heap is the k-th largest element.