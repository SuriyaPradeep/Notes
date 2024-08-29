#array 
### Question
You are given a **0-indexed** array of integers `nums` of length `n`. You are initially positioned at `nums[0]`.

Each element `nums[i]` represents the maximum length of a forward jump from index `i`. In other words, if you are at `nums[i]`, you can jump to any `nums[i + j]` where:

- `0 <= j <= nums[i]` and
- `i + j < n`

Return _the minimum number of jumps to reach_ `nums[n - 1]`. The test cases are generated such that you can reach `nums[n - 1]`.

**Example 1:**

**Input:** nums = [2,3,1,1,4]
**Output:** 2
**Explanation:** The minimum number of jumps to reach the last index is 2. Jump 1 step from index 0 to 1, then 3 steps to the last index.

**Example 2:**

**Input:** nums = [2,3,0,1,4]
**Output:** 2

### Solution
```java
class Solution{
public int jump(int[] nums) {  
    int left=0,right=0,farthest=0,n=nums.length,res=0;  
    while(right<n-1){  
        for(int i=left;i<=right;i++){  
            farthest=Math.max(farthest,nums[i]+i);  
        }  
        left=right+1;  
        right=farthest;  
        res++;  
    }  
    return res;  
}
}
```
**Explanation**
Variables:

- **`left`:** The starting index of the current range of indices being considered.
- **`right`:** The ending index of the current range of indices being considered.
- **`farthest`:** The farthest index that can be reached by jumping from any index in the current range `[left, right]`.
- **`n`:** The length of the array `nums`.
- **`res`:** The result, which keeps track of the minimum number of jumps needed.

How It Works:

1. **Initialization:**
    
    - `left` and `right` are both initialized to 0, indicating that the first step is to explore how far we can go starting from the first index.
    - `farthest` is initialized to 0 and will be updated to the farthest index we can reach from the current range `[left, right]`.
    - `res` is initialized to 0 to count the number of jumps.
2. **Main Loop (while `right < n - 1`):**
    
    - The loop runs as long as `right` is less than `n - 1` (i.e., as long as we haven't reached the last index).
    - Inside the loop, we iterate over the current range `[left, right]` and calculate the farthest index that can be reached from any of these indices. This is done using `farthest = Math.max(farthest, nums[i] + i);`, where `nums[i] + i` gives the maximum index reachable from index `i`.
3. **Update `left` and `right`:**
    
    - After determining the farthest index that can be reached from the current range, `left` is updated to `right + 1` to start the next range of indices.
    - `right` is updated to `farthest` to represent the end of the new range.
    - `res` is incremented by 1, indicating that a jump has been made.
4. **Return the Result:**
    
    - The loop continues until `right` reaches or exceeds `n - 1` (i.e., we can reach or surpass the last index).
    - The method then returns `res`, which is the minimum number of jumps needed to reach the last index.