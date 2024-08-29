#binary-search 
### Question
There is an integer array `nums` sorted in ascending order (with **distinct** values).

Prior to being passed to your function, `nums` is **possibly rotated** at an unknown pivot index `k` (`1 <= k < nums.length`) such that the resulting array is `[nums[k], nums[k+1], ..., nums[n-1], nums[0], nums[1], ..., nums[k-1]]` (**0-indexed**). For example, `[0,1,2,4,5,6,7]` might be rotated at pivot index `3` and become `[4,5,6,7,0,1,2]`.

Given the array `nums` **after** the possible rotation and an integer `target`, return _the index of_ `target` _if it is in_ `nums`_, or_ `-1` _if it is not in_ `nums`.

You must write an algorithm with `O(log n)` runtime complexity.

**Example 1:**

**Input:** nums = [4,5,6,7,0,1,2], target = 0
**Output:** 4

**Example 2:**

**Input:** nums = [4,5,6,7,0,1,2], target = 3
**Output:** -1

**Example 3:**

**Input:** nums = [1], target = 0
**Output:** -1

### Solution
```java
class Solution{
	public int search(int[] nums, int target) {  
	    int left=0,right=nums.length-1;  
	    while(left<=right){  
	        int mid=(left+right)/2;  
	        if(nums[mid]==target){  
	            return mid;  
	        }else if(nums[left]<=nums[mid]){  
	            if(nums[left]<=target && nums[mid]>target){  
	                right=mid-1;  
	            }else{  
	                left=mid+1;  
	            }  
	        }else{  
	            if(nums[mid]<target && nums[right]>=target){  
	                left=mid+1;  
	            }else{  
	                right=mid-1;  
	            }  
	        }  
	    }  
	    return -1;  
	}
}
```

**Explanation**
1. **Initialization**:
    
    - Set `left` to 0 and `right` to the last index of the array.
2. **Binary Search Loop**:
    
    - Continue the loop as long as `left` is less than or equal to `right`.
3. **Mid Calculation**:
    
    - Calculate the middle index `mid` by taking the average of `left` and `right`.
4. **Check Mid Condition**:
    
    - If the element at `mid` is equal to the target (`nums[mid] == target`), return `mid` as the index where the target is found.
5. **Determine Sorted Half**:
    
    - Check if the left half of the array (`nums[left]` to `nums[mid]`) is sorted:
        - If `nums[left] <= nums[mid]`, then the left half is sorted.
            - Check if the target is within this sorted left half (`nums[left] <= target < nums[mid]`):
                - If yes, adjust `right` to `mid - 1` to search within the left half.
                - If no, adjust `left` to `mid + 1` to search in the right half.
    - Otherwise, the right half of the array (`nums[mid]` to `nums[right]`) is sorted:
        - Check if the target is within this sorted right half (`nums[mid] < target <= nums[right]`):
            - If yes, adjust `left` to `mid + 1` to search within the right half.
            - If no, adjust `right` to `mid - 1` to search in the left half.
6. **Return Result**:
    
    - If the loop completes without finding the target, return `-1` indicating the target is not present in the array.

