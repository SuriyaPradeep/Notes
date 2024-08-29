#array 
You are given an integer array `nums`. You are initially positioned at the array's **first index**, and each element in the array represents your maximum jump length at that position.

Return `true` _if you can reach the last index, or_ `false` _otherwise_.

**Example 1:**

**Input:** nums = [2,3,1,1,4]
**Output:** true
**Explanation:** Jump 1 step from index 0 to 1, then 3 steps to the last index.

**Example 2:**

**Input:** nums = [3,2,1,0,4]
**Output:** false
**Explanation:** You will always arrive at index 3 no matter what. Its maximum jump length is 0, which makes it impossible to reach the last index.

### Solution
```java
class Solution{
	public boolean canJump(int[] nums) {  
	    int n=nums.length;  
	    int goal=n-1;  
	    for(int i=n-2;i>=0;i--){  
	        if(nums[i]+i>=goal){  
	            goal=i;  
	        }  
	    }  
	    return goal==0;  
	}
}
```

**Explanation**
1. **Initialization:**
    
    - `n = nums.length;`: This stores the length of the input array `nums`.
    - `goal = n - 1;`: The initial goal is set to the last index of the array. The objective is to determine if you can reach this goal starting from earlier indices.
2. **Looping Backward Through the Array:**
    
    - The loop starts from the second-to-last element (`i = n - 2`) and iterates backward to the start of the array (`i >= 0`).
    - For each index `i`, it checks if it's possible to reach the current goal from that index. Specifically, it checks if `nums[i] + i >= goal`.
        - `nums[i] + i`: This represents the farthest index you can reach from index `i`.
        - If you can reach or surpass the current goal from index `i`, it updates the goal to `i`. This means you now need to determine if you can reach index `i` from an earlier index.
3. **Returning the Result:**
    
    - After the loop finishes, the method returns `goal == 0`.
    - If `goal` is 0, it means you can reach the last index starting from the first index. If `goal` is not 0, it means there's no way to reach the last index from the first index.