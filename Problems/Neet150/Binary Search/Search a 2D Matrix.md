#binary-search #2DArray 
### Question
You are given an `m x n` integer matrix `matrix` with the following two properties:

- Each row is sorted in non-decreasing order.
- The first integer of each row is greater than the last integer of the previous row.

Given an integer `target`, return `true` _if_ `target` _is in_ `matrix` _or_ `false` _otherwise_.

You must write a solution in `O(log(m * n))` time complexity.

**Example 1:**

![](https://assets.leetcode.com/uploads/2020/10/05/mat.jpg)

**Input:** matrix = [[1,3,5,7],[10,11,16,20],[23,30,34,60]], target = 3
**Output:** true

**Example 2:**

![](https://assets.leetcode.com/uploads/2020/10/05/mat2.jpg)

**Input:** matrix = [[1,3,5,7],[10,11,16,20],[23,30,34,60]], target = 13
**Output:** false

### Solution
```java
class Solution{
	public boolean searchMatrix(int[][] matrix, int target) {  
	    int rows=matrix.length,cols=matrix[0].length;  
	    int n=rows*cols;  
	    int left=0,right=n-1;  
	    while(left<=right){  
	        int mid=(left+right)/2;  
	        int num=matrix[mid/cols][mid%cols];  
	        if(num==target){  
	            return true;  
	        }else if(num>target){  
	            right=mid-1;  
	        }else{  
	            left=mid+1;  
	        }  
	    }  
	    return false;  
	}
}
```

1. **Initialization**:
    
    - Determine the number of rows (`rows`) and columns (`cols`) in the matrix.
    - Calculate the total number of elements (`n`) in the matrix as `rows * cols`.
    - Define two pointers, `left` and `right`, representing the start and end of the flattened version of the matrix. Initialize `left` to 0 and `right` to `n - 1`.
2. **Binary Search Loop**:
    
    - Continue the loop as long as `left` is less than or equal to `right`.
3. **Mid Calculation**:
    
    - Calculate the middle index `mid` by taking the average of `left` and `right`.
4. **Map Mid to 2D Matrix**:
    
    - Convert the `mid` index from the flattened array back to the 2D matrix format using integer division and modulo operations:
        - `mid / cols` gives the row index.
        - `mid % cols` gives the column index.
    - Retrieve the value at the calculated position in the matrix (`num = matrix[mid / cols][mid % cols]`).
5. **Check Mid Value**:
    
    - If `num` equals the target, return `true` as the target is found.
    - If `num` is greater than the target, adjust the search range by setting `right` to `mid - 1`.
    - If `num` is less than the target, adjust the search range by setting `left` to `mid + 1`.
6. **Target Not Found**:
    
    - If the loop ends without finding the target, return `false` indicating that the target is not present in the matrix.
