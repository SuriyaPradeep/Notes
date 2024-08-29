#slidingWindow #priority-queue 
### Question
You are given an array of integers `nums`, there is a sliding window of size `k` which is moving from the very left of the array to the very right. You can only see the `k` numbers in the window. Each time the sliding window moves right by one position.

Return _the max sliding window_.

**Example 1:**

**Input:** nums = [1,3,-1,-3,5,3,6,7], k = 3
**Output:** [3,3,5,5,6,7]
**Explanation:** 
Window position                Max
---------------               -----
[1  3  -1] -3  5  3  6  7       **3**
 1 [3  -1  -3] 5  3  6  7       **3**
 1  3 [-1  -3  5] 3  6  7      ** 5**
 1  3  -1 [-3  5  3] 6  7       **5**
 1  3  -1  -3 [5  3  6] 7       **6**
 1  3  -1  -3  5 [3  6  7]      **7**

**Example 2:**

**Input:** nums = [1], k = 1
**Output:** [1]

### Solution
```java
class Solution{
	public int[] maxSlidingWindow(int[] nums, int k) {  
	    int n=nums.length;  
	    int[] res=new int[n-k+1];  
	    PriorityQueue<Integer>pq=new PriorityQueue<>((a,b)->(nums[b]-nums[a]));  
	    for(int i=0;i<n;i++){  
	        while(!pq.isEmpty() && (i-pq.peek())>=k){  
	            pq.poll();  
	        }  
	        pq.add(i);  
	        if(i-k+1>=0){  
	            res[i-k+1]=nums[pq.peek()];  
	        }  
	    }  
	    return res;  
	}
}
```

**Explanation**
1. **Initialization**:
    
    - Get the length of `nums` (`n`).
    - Initialize an array `res` of size `n - k + 1` to store the result.
    - Use a `PriorityQueue` (`pq`) to maintain a max-heap of indices based on the values in `nums`.
2. **Iterate Through the Array**:
    
    - For each element in `nums` (index `i`):
        - Remove indices from the heap that are outside the current window.
        - Add the current index to the heap.
        - If the current index is within the valid window range (`i - k + 1 >= 0`), store the maximum value in `res`.
3. **Return Result**:
    
    - Return the array `res` containing the maximum values for each sliding window.
