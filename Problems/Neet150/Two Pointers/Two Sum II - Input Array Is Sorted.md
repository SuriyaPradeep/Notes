### Question
Given a **1-indexed** array of integers `numbers` that is already **_sorted in non-decreasing order_**, find two numbers such that they add up to a specific `target` number. Let these two numbers be `numbers[index1]` and `numbers[index2]` where `1 <= index1 < index2 <= numbers.length`.

Return _the indices of the two numbers,_ `index1` _and_ `index2`_, **added by one** as an integer array_ `[index1, index2]` _of length 2._

The tests are generated such that there is **exactly one solution**. You **may not** use the same element twice.

Your solution must use only constant extra space.

**Example 1:**

**Input:** numbers = [2,7,11,15], target = 9
**Output:** [1,2]
**Explanation:** The sum of 2 and 7 is 9. Therefore, index1 = 1, index2 = 2. We return [1, 2].

**Example 2:**

**Input:** numbers = [2,3,4], target = 6
**Output:** [1,3]
**Explanation:** The sum of 2 and 4 is 6. Therefore index1 = 1, index2 = 3. We return [1, 3].

**Example 3:**

**Input:** numbers = [-1,0], target = -1
**Output:** [1,2]
**Explanation:** The sum of -1 and 0 is -1. Therefore index1 = 1, index2 = 2. We return [1, 2].

### Solution
```java
class Solutin{  
	public int[] twoSum(int[] numbers, int target) {  
	    int left=0,right=numbers.length-1;  
	    while(left<right){  
	        int sum=numbers[left]+numbers[right];  
	        if(sum==target){  
	            return new int[]{left+1,right+1};  
	        }else if(target<sum){  
	            right--;  
	        }else{  
	            left++;  
	        }  
	    }  
	    return new int[]{-1,-1};  
	}
}
```

**Explanation**
1. **Initialize Pointers**:
    
    - `int left = 0;` starts the left pointer at the beginning of the array.
    - `int right = numbers.length - 1;` starts the right pointer at the end of the array.
2. **While Loop**:
    
    - `while (left < right)` ensures the loop continues as long as the left pointer is to the left of the right pointer.
3. **Calculate Sum**:
    
    - `int sum = numbers[left] + numbers[right];` calculates the sum of the elements at the current left and right pointers.
4. **Check Sum**:
    
    - `if (sum == target)` checks if the calculated sum equals the target. If so, it returns the 1-based indices of the two numbers (i.e., `left + 1` and `right + 1`).
5. **Adjust Pointers**:
    
    - `else if (sum > target)` moves the `right` pointer to the left (i.e., `right--`) if the sum is greater than the target. This is because the array is sorted, and moving the pointer left will reduce the sum.
    - `else` moves the `left` pointer to the right (i.e., `left++`) if the sum is less than the target. This increases the sum by moving to a higher value.
6. **Return No Solution**:
    
    - `return new int[]{-1, -1};` returns `[-1, -1]` if no two numbers sum up to the target. This is a fallback in case no valid pair is found.
