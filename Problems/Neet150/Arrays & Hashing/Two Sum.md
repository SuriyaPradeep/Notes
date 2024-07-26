#hashmap 
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
	    HashMap<Integer,Integer>hash=new HashMap<>();  
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

### Explanation
1. **Initialize a HashMap**:
    
    - A `HashMap<Integer, Integer>` named `hash` is created to store the elements of the array and their corresponding indices.
    - The keys of the HashMap are the elements of the array, and the values are their indices.
2. **Iterate Through the Array**:
    
    - A `for` loop iterates through each element in the array `nums`.
3. **Calculate Complement**:
    
    - For each element `nums[i]`, calculate the complement as `target - nums[i]`.
    - The complement is the value needed to add to `nums[i]` to reach the target.
4. **Check for Complement in HashMap**:
    
    - Check if the `hash` contains the complement.
    - If the `hash` contains the complement, return the indices of the complement and the current element. These indices are `hash.get(complement)` and `i`.
5. **Add Element to HashMap**:
    
    - If the complement is not found in the `hash`, add the current element and its index to the `hash`.
    - `hash.put(nums[i], i)` stores the current element and its index.
6. **Return Result**:
    
    - If no pair is found by the end of the loop, return `new int[]{-1, -1}`.
