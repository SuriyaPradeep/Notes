#binary-search 
### Question
Suppose an array of length `n` sorted in ascending order is **rotated** between `1` and `n` times. For example, the array `nums = [0,1,2,4,5,6,7]` might become:

- `[4,5,6,7,0,1,2]` if it was rotated `4` times.
- `[0,1,2,4,5,6,7]` if it was rotated `7` times.

Notice that **rotating** an array `[a[0], a[1], a[2], ..., a[n-1]]` 1 time results in the array `[a[n-1], a[0], a[1], a[2], ..., a[n-2]]`.

Given the sorted rotated array `nums` of **unique** elements, return _the minimum element of this array_.

You must write an algorithm that runs in `O(log n) time.`

**Example 1:**

**Input:** nums = [3,4,5,1,2]
**Output:** 1
**Explanation:** The original array was [1,2,3,4,5] rotated 3 times.

**Example 2:**

**Input:** nums = [4,5,6,7,0,1,2]
**Output:** 0
**Explanation:** The original array was [0,1,2,4,5,6,7] and it was rotated 4 times.

**Example 3:**

**Input:** nums = [11,13,15,17]
**Output:** 11
**Explanation:** The original array was [11,13,15,17] and it was rotated 4 times.

### Solution
```java
class Solution{
	public int findMin(int[] nums) {  
	    int left=0,right=nums.length-1;  
	    while(left<=right){  
	        int mid=(left+right)/2;  
	        if(mid!=0 && nums[mid-1]>nums[mid]){  
	            return nums[mid];  
	        }else if(nums[left]<=nums[mid] && nums[mid]>nums[right]){  
	            left=mid+1;  
	        }else{  
	            right=mid-1;  
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
4. **Check Mid Conditions**:
    
    - If `mid` is not the first element (`mid != 0`) and the element before `mid` is greater than the element at `mid` (`nums[mid-1] > nums[mid]`), it means the element at `mid` is the minimum element. Return `nums[mid]`.
5. **Adjust Search Range**:
    
    - If the element at `left` is less than or equal to the element at `mid` and the element at `mid` is greater than the element at `right` (`nums[left] <= nums[mid] && nums[mid] > nums[right]`), it means the smallest value is in the right part of the array. Set `left` to `mid + 1`.
    - Otherwise, the smallest value is in the left part of the array. Set `right` to `mid - 1`.
6. **Return Result**:
    
    - If the loop completes without finding the minimum element, return `-1`. However, this case shouldn't happen for a correctly rotated sorted array.

### Example Walkthrough

Consider `nums = [4, 5, 6, 7, 0, 1, 2]`:

- Initial state: `left = 0`, `right = 6`
- First iteration:
    - `mid = (0 + 6) / 2 = 3`
    - `nums[mid] = 7`
    - `nums[mid - 1] = 6`
    - `nums[left] = 4`
    - `nums[right] = 2`
    - Since `nums[left] <= nums[mid]` and `nums[mid] > nums[right]`, update `left` to `mid + 1 = 4`
- Second iteration:
    - `left = 4`, `right = 6`
    - `mid = (4 + 6) / 2 = 5`
    - `nums[mid] = 1`
    - `nums[mid - 1] = 0`
    - `nums[left] = 0`
    - `nums[right] = 2`
    - Since `nums[mid - 1] <= nums[mid]` and `nums[mid] <= nums[right]`, update `right` to `mid - 1 = 4`
- Third iteration:
    - `left = 4`, `right = 4`
    - `mid = (4 + 4) / 2 = 4`
    - `nums[mid] = 0`
    - Since `mid != 0` and `nums[mid - 1] > nums[mid]` (7 > 0), return `nums[mid] = 0`