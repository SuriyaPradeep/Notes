#array #Math 
### Question
Given an integer array `nums`, return _an array_ `answer` _such that_ `answer[i]` _is equal to the product of all the elements of_ `nums` _except_ `nums[i]`.

The product of any prefix or suffix of `nums` is **guaranteed** to fit in a **32-bit** integer.

You must write an algorithm that runs in `O(n)` time and without using the division operation.

**Example 1:**

**Input:** nums = [1,2,3,4]
**Output:** [24,12,8,6]

**Example 2:**

**Input:** nums = [-1,1,0,-3,3]
**Output:** [0,0,9,0,0]

### Solution
```java
class Solution{
	public int[] productExceptSelf(int[] nums) {  
	    int prod=1,n=nums.length;  
	    int[] ans=new int[n];  
	    Arrays.fill(ans,1);  
	    for(int i=0;i<n;i++){  
	        ans[i]*=prod;  
	        prod*=nums[i];  
	    }  
	    prod=1;  
	    for(int i=n-1;i>=0;i--){  
	        ans[i]*=prod;  
	        prod*=nums[i];  
	    }  
	    return ans;  
	}
}
```

**Explanation**
1. **Initialization**:
    
    - You initialize `prod` to 1, which will be used to store the cumulative product.
    - You initialize `ans`, the result array, and fill it with 1s. This array will store the final product values.
    - You also store the length of the input array in `n`.
2. **First Pass (Left Products)**:
    
    - You iterate through the array from left to right.
    - For each element at index `i`, you multiply the current value in `ans[i]` by `prod`, which is the cumulative product of all previous elements.
    - You then update `prod` by multiplying it with the current element, so it becomes the cumulative product up to the current index.
3. **Second Pass (Right Products)**:
    
    - You reset `prod` to 1.
    - You iterate through the array from right to left.
    - For each element at index `i`, you multiply the current value in `ans[i]` by `prod`, which is now the cumulative product of all elements to the right of the current index.
    - You then update `prod` by multiplying it with the current element, so it becomes the cumulative product from the current index to the end.
4. **Return Result**:
    
    - The `ans` array now contains the product of all elements except the element at each index, and you return it.

