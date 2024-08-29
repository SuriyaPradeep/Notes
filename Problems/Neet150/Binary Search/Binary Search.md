#binary-search 
### Question
Given an array of integers `nums` which is sorted in ascending order, and an integer `target`, write a function to search `target` in `nums`. If `target` exists, then return its index. Otherwise, return `-1`.

You must write an algorithm with `O(log n)` runtime complexity.

**Example 1:**

**Input:** nums = [-1,0,3,5,9,12], target = 9
**Output:** 4
**Explanation:** 9 exists in nums and its index is 4

**Example 2:**

**Input:** nums = [-1,0,3,5,9,12], target = 2
**Output:** -1
**Explanation:** 2 does not exist in nums so return -1

### Solution
```java
class Solution{  
	public int search(int[] nums, int target) {  
	    int left=0,right=nums.length-1;  
	    while(left<=right){  
	        int mid=(left+right)/2;  
	        if(nums[mid]==target){  
	            return mid;  
	        }else if(nums[mid]>target){  
	            right=mid-1;  
	        }else{  
	            left=mid+1;  
	        }  
	    }  
	    return -1;  
	}
}
```

**Explanation**
1. **Initialization**:
    
    - Define two pointers, `left` and `right`, which represent the start and end of the array, respectively. Initially, `left` is set to 0, and `right` is set to the last index of the array.
2. **Binary Search Loop**:
    
    - Continue the loop as long as `left` is less than or equal to `right`.
3. **Mid Calculation**:
    
    - Calculate the middle index `mid` by taking the average of `left` and `right`.
4. **Check Mid Value**:
    
    - If the value at the middle index `nums[mid]` is equal to the target, return the middle index `mid` as the target is found.
5. **Adjust Search Range**:
    
    - If the value at the middle index `nums[mid]` is greater than the target, adjust the search range by setting `right` to `mid - 1`. This narrows the search to the left half of the current range.
    - If the value at the middle index `nums[mid]` is less than the target, adjust the search range by setting `left` to `mid + 1`. This narrows the search to the right half of the current range.
6. **Target Not Found**:
    
    - If the loop ends without finding the target, return -1 indicating that the target is not present in the array.