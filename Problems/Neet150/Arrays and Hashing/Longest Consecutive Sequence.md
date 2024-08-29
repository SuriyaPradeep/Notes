#set #array 
### Question
Given an unsorted array of integers `nums`, return _the length of the longest consecutive elements sequence._

You must write an algorithm that runs in `O(n)` time.

**Example 1:**

**Input:** nums = [100,4,200,1,3,2]
**Output:** 4
**Explanation:** The longest consecutive elements sequence is `[1, 2, 3, 4]`. Therefore its length is 4.

**Example 2:**

**Input:** nums = [0,3,7,2,5,8,4,6,0,1]
**Output:** 9

### Solution
```java
class Solution{
	public int longestConsecutive(int[] nums) {  
	    HashSet<Integer> set=new HashSet<>();  
	    for(int num:nums){  
	        set.add(num);  
	    }  
	    int max=0;  
	    for(int num:nums){  
	        int left=num-1;  
	        int right=num+1;  
	        while(set.remove(left)){  
	            left--;  
	        }  
	        while(set.remove(right)){  
	            right++;  
	        }  
	        max=Math.max(max,right-left-1);  
	        if(set.isEmpty()){  
	            return max;  
	        }  
	    }  
	    return max;  
	}
}
```

**Explanation**
1. **HashSet Initialization**:
    
    - **Purpose**: Store all unique numbers from the array.
    - **Reason**: Provides O(1)O(1)O(1) average time complexity for checking existence and removing elements.
2. **First Loop (Add Elements to HashSet)**:
    
    - **Purpose**: Populate the `HashSet` with all numbers from the `nums` array.
    - **Reason**: This allows quick access and modification operations.
3. **Second Loop (Process Each Number)**:
    
    - **Purpose**: Find and process consecutive sequences starting from each number in the array.
    - **Checking Sequence Start**: For each number, check if it is the start of a consecutive sequence by looking for `num - 1` in the set. If it is not found, then `num` is the start of a sequence.
4. **Remove Consecutive Elements**:
    
    - **Left Removal**: Remove all elements less than `num` to find the start of the sequence.
    - **Right Removal**: Remove all elements greater than `num` to extend the sequence.
5. **Calculate Length**:
    
    - **Length Calculation**: After removing elements, `right` will point to the next non-consecutive number, and `left` will point to the previous non-consecutive number.
    - **Length Formula**: The length of the sequence is `right - left - 1` because `right` is one past the end of the sequence, and `left` is one before the start.
6. **Update Maximum Length**:
    
    - **Purpose**: Keep track of the maximum length of consecutive sequences found so far.
7. **Early Exit (Optional)**:
    
    - **Check**: If the `HashSet` is empty, it means all numbers have been processed, so the function returns the maximum length found so far. This is an optimization to stop early if no more sequences are possible.
8. **Return Result**:
    
    - **Purpose**: Return the maximum length of any consecutive sequence found.

