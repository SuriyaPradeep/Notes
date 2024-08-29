#array #2pointer 
### Question
You are given an integer array `height` of length `n`. There are `n` vertical lines drawn such that the two endpoints of the `ith` line are `(i, 0)` and `(i, height[i])`.

Find two lines that together with the x-axis form a container, such that the container contains the most water.

Return _the maximum amount of water a container can store_.

**Notice** that you may not slant the container.

**Example 1:**

![](https://s3-lc-upload.s3.amazonaws.com/uploads/2018/07/17/question_11.jpg)

**Input:** height = [1,8,6,2,5,4,8,3,7]
**Output:** 49
**Explanation:** The above vertical lines are represented by array [1,8,6,2,5,4,8,3,7]. In this case, the max area of water (blue section) the container can contain is 49.

**Example 2:**

**Input:** height = [1,1]
**Output:** 1

### Solution
```java
class Solution{
	public int maxArea(int[] height) {  
	    int max=Integer.MIN_VALUE;  
	    int left=0,right=height.length-1;  
	    while(left<right){  
	        int currHeight=Math.min(height[left],height[right]);  
	        int area=currHeight*(right-left);  
	        max=Math.max(max,area);  
	        if(height[left]<=height[right]){  
	            left++;  
	        }else{  
	            right--;  
	        }  
	    }  
	    return max;  
	}
}
```

**Explanation**
1. **Initialize Variables**:
    
    - `max` is initialized to `Integer.MIN_VALUE` to ensure that any valid area calculation will be larger initially.
    - `left` and `right` pointers are initialized to the start and end of the `height` array, respectively.
2. **Loop until Pointers Meet**:
    
    - The `while (left < right)` loop continues until the `left` and `right` pointers meet.
3. **Calculate Current Area**:
    
    - `currHeight` is calculated as the minimum of the heights at the `left` and `right` pointers. This ensures that the height of the container is determined by the shorter line.
    - `area` is then calculated as the product of `currHeight` and the distance between the pointers (`right - left`).
4. **Update Maximum Area**:
    
    - `max = Math.max(max, area)` updates the maximum area if the current area is larger than the previously recorded maximum.
5. **Move Pointers**:
    
    - The pointer corresponding to the shorter height is moved inward to potentially find a larger area. If the height at `left` is less than or equal to the height at `right`, the `left` pointer is incremented. Otherwise, the `right` pointer is decremented.
6. **Return Maximum Area**:
    
    - After the loop completes, the function returns the maximum area found.

