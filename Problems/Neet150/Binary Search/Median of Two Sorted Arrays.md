#binary-search 
### Question
Given two sorted arrays `nums1` and `nums2` of size `m` and `n` respectively, return **the median** of the two sorted arrays.

The overall run time complexity should be `O(log (m+n))`.

**Example 1:**

**Input:** nums1 = [1,3], nums2 = [2]
**Output:** 2.00000
**Explanation:** merged array = [1,2,3] and median is 2.

**Example 2:**

**Input:** nums1 = [1,2], nums2 = [3,4]
**Output:** 2.50000
**Explanation:** merged array = [1,2,3,4] and median is (2 + 3) / 2 = 2.5.

### Solution
```java
class Solution{
	public double findMedianSortedArrays(int[] nums1, int[] nums2) {  
	    int n1=nums1.length,n2=nums2.length;  
	    if(n1>n2){  
	        return findMedianSortedArrays(nums2,nums1);  
	    }  
	    int n=n1+n2;  
	    int leftPartition=(n+1)/2;  
	    int left=0,right=n1;  
	    while(left<=right){  
	        int mid1=(left+right)/2;  
	        int mid2=leftPartition-mid1;  
	        int l1=mid1>0?nums1[mid1-1]:Integer.MIN_VALUE;  
	        int l2=mid2>0?nums2[mid2-1]:Integer.MIN_VALUE;  
	        int r1=mid1<n1?nums1[mid1]:Integer.MAX_VALUE;  
	        int r2=mid2<n2?nums2[mid2]:Integer.MAX_VALUE;  
	        if(l1<=r2 && l2<=r1){  
	            if(n%2==1){  
	                return Math.max(l1,l2);  
	            }else{  
	                return (double)((Math.max(l1,l2)+Math.min(r1,r2))/2.0);  
	            }  
	        }else if(l1>r2){  
	            right=mid1-1;  
	        }else{  
	            left=mid1+1;  
	        }  
	    }  
	    return -1;  
	}
}
```

**Explanation**
1. **Initial Setup**:
    
    - `n1` and `n2` store the lengths of `nums1` and `nums2`.
    - Ensure `nums1` is the smaller array. If not, swap the arrays by calling the function recursively with swapped arguments.
    - `n` is the total length of both arrays combined.
    - `leftPartition` is the number of elements that should be in the left partition.
2. **Binary Search Initialization**:
    
    - Initialize the binary search on `nums1` with `left` set to 0 and `right` set to `n1`.
3. **Binary Search Loop**:
    
    - Calculate `mid1`, the partition index for `nums1`.
    - Calculate `mid2`, the partition index for `nums2`, which ensures `leftPartition` elements are in the left partition.
    - Compute `l1`, `l2`, `r1`, and `r2`:
        - `l1`: The element just before the partition in `nums1`. If `mid1` is 0, set it to `Integer.MIN_VALUE`.
        - `l2`: The element just before the partition in `nums2`. If `mid2` is 0, set it to `Integer.MIN_VALUE`.
        - `r1`: The element at the partition in `nums1`. If `mid1` is `n1`, set it to `Integer.MAX_VALUE`.
        - `r2`: The element at the partition in `nums2`. If `mid2` is `n2`, set it to `Integer.MAX_VALUE`.
4. **Checking Partitions**:
    
    - If `l1 <= r2` and `l2 <= r1`, the partitions are correct:
        - If the total number of elements `n` is odd, return the maximum of `l1` and `l2` (the median).
        - If `n` is even, return the average of the maximum of `l1` and `l2` and the minimum of `r1` and `r2`.
    - If `l1 > r2`, move the `right` pointer to `mid1 - 1`.
    - If `l1 <= r2`, move the `left` pointer to `mid1 + 1`.
5. **Edge Case Handling**:
    
    - Return -1 if no valid partition is found, though this scenario shouldn't occur with valid inputs.