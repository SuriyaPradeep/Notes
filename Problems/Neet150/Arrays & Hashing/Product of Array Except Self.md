#array 
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
	    int n=nums.length;  
	    int[] prefix=new int[n];  
	    Arrays.fill(prefix,1);  
	    int prod=1;  
	    for(int i=0;i<n;i++){  
	        prefix[i]*=prod;  
	        prod*=nums[i];  
	    }  
	    int[] suffix=new int[n];  
	    Arrays.fill(suffix,1);  
	    prod=1;  
	    for(int i=n-1;i>=0;i--){  
	        suffix[i]*=prod;  
	        prod*=nums[i];  
	    }  
	    int[] ans=new int[n];  
	    for(int i=0;i<n;i++){  
	        ans[i]=prefix[i]*suffix[i];  
	    }  
	    return ans;  
	}
}
```

### Explanation
1. **Initialize Prefix Product Array**:
    
    - An array `prefix` is created to store the prefix products, i.e., the product of all elements before the current index.
    - Initialize `prefix` with 1: `Arrays.fill(prefix, 1)`.
2. **Calculate Prefix Products**:
    
    - Iterate through the array from left to right.
    - Use a variable `prod` to keep track of the running product.
    - Update `prefix[i]` to be the product of all previous elements.
    - Update `prod` to include the current element.
3. **Initialize Suffix Product Array**:
    
    - An array `suffix` is created to store the suffix products, i.e., the product of all elements after the current index.
    - Initialize `suffix` with 1: `Arrays.fill(suffix, 1)`.
4. **Calculate Suffix Products**:
    
    - Iterate through the array from right to left.
    - Use a variable `prod` to keep track of the running product.
    - Update `suffix[i]` to be the product of all subsequent elements.
    - Update `prod` to include the current element.
5. **Calculate the Final Result**:
    
    - An array `ans` is created to store the result.
    - Iterate through the array and set `ans[i]` to be the product of `prefix[i]` and `suffix[i]`.
6. **Return the Result**:
    
    - Return the array `ans` which contains the product of all elements except the current element.
