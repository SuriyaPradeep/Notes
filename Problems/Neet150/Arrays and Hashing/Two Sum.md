#hashmap #array 
### Question
Given an array of integers `nums` and an integer `target`, return _indices of the two numbers such that they add up to `target`_.

You may assume that each input would have **_exactly_ one solution**, and you may not use the _same_ element twice.

You can return the answer in any order.

**Example 1:**

**Input:** nums = [2,7,11,15], target = 9
**Output:** [0,1]
**Explanation:** Because nums[0] + nums[1] == 9, we return [0, 1].

**Example 2:**

**Input:** nums = [3,2,4], target = 6
**Output:** [1,2]

**Example 3:**

**Input:** nums = [3,3], target = 6
**Output:** [0,1]

### Solution
```java
class Solution{
	public int[] twoSum(int[] nums, int target) {  
	    HashMap<Integer,Integer> hash=new HashMap<>();  
	    for(int i=0;i<nums.length;i++){  
	        int complement=target-nums[i];  
	        if(hash.containsKey(complement)){  
	            return new int[]{hash.get(complement),i};  
	        }  
	        hash.put(nums[i],i);  
	    }  
	    return new int[]{-1,-1};  
	}
}
```

**Explanation**
1. **Initialization**: You initialize a `HashMap` to store the values and their corresponding indices from the array.
2. **Iteration**: You iterate through each element in the array.
3. **Finding Complement**: For each element, you calculate its complement with respect to the target (i.e., `target - nums[i]`).
4. **Check for Complement**: You check if the complement exists in the `HashMap`.
    - If it exists, you return the indices of the current element and the complement.
5. **Storing Values**: If the complement does not exist, you store the current element and its index in the `HashMap`.
6. **Return**: If no such pair is found, you return `{-1, -1}`.

