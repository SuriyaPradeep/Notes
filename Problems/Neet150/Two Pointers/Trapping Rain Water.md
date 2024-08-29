#array #2pointer 
### Question
Given `n` non-negative integers representing an elevation map where the width of each bar is `1`, compute how much water it can trap after raining.

**Example 1:**

![](https://assets.leetcode.com/uploads/2018/10/22/rainwatertrap.png)

**Input:** height = [0,1,0,2,1,0,1,3,2,1,2,1]
**Output:** 6
**Explanation:** The above elevation map (black section) is represented by array [0,1,0,2,1,0,1,3,2,1,2,1]. In this case, 6 units of rain water (blue section) are being trapped.

**Example 2:**

**Input:** height = [4,2,0,3,2,5]
**Output:** 9

### Solution
```java
class Solution{
	public int trap(int[] height) {  
	    int left=0,right=height.length-1;  
	    int leftMax=height[left],rightMax=height[right];  
	    int water=0;  
	    while(left<right){  
	        if(leftMax<rightMax){  
	            left++;  
	            if(height[left]>=leftMax){  
	                leftMax=height[left];  
	            }else{  
	                water+=leftMax-height[left];  
	            }  
	        }else{  
	            right--;  
	            if(height[right]>=rightMax){  
	                rightMax=height[right];  
	            }else{  
	                water+=rightMax-height[right];  
	            }  
	        }  
	    }  
	    return water;  
	}
}
```

**Explanation**
1. **Initialize Pointers and Variables**:
    
    - `int left = 0, right = height.length - 1;` initializes two pointers at the beginning and end of the array.
    - `int leftMax = height[left], rightMax = height[right];` initializes the maximum heights seen so far from the left and right.
    - `int water = 0;` initializes the total amount of trapped water to 0.
2. **Loop until Pointers Meet**:
    
    - `while (left < right)` continues the loop as long as the `left` pointer is less than the `right` pointer.
3. **Determine the Lower Max Height**:
    
    - If `leftMax < rightMax`, the potential for trapping water depends on the left side.
    - Otherwise, it depends on the right side.
4. **Move Pointers and Calculate Water**:
    
    - If the left side is the limiting factor, move the `left` pointer to the right.
        - Update `leftMax` if the new height is greater or equal to `leftMax`.
        - Otherwise, add the difference between `leftMax` and the new height to `water`.
    - If the right side is the limiting factor, move the `right` pointer to the left.
        - Update `rightMax` if the new height is greater or equal to `rightMax`.
        - Otherwise, add the difference between `rightMax` and the new height to `water`.
5. **Return Total Water**:
    
    - After the loop completes, return the total amount of trapped water.
