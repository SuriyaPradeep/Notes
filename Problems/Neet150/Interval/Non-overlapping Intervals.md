#2DArray #intervals 
### Question
Given an array of intervals `intervals` where `intervals[i] = [starti, endi]`, return _the minimum number of intervals you need to remove to make the rest of the intervals non-overlapping_.

**Example 1:**

**Input:** intervals = [[1,2],[2,3],[3,4],[1,3]]
**Output:** 1
**Explanation:** [1,3] can be removed and the rest of the intervals are non-overlapping.

**Example 2:**

**Input:** intervals = [[1,2],[1,2],[1,2]]
**Output:** 2
**Explanation:** You need to remove two [1,2] to make the rest of the intervals non-overlapping.

**Example 3:**

**Input:** intervals = [[1,2],[2,3]]
**Output:** 0
**Explanation:** You don't need to remove any of the intervals since they're already non-overlapping.

### Solution
```java
class Solution{
	public int eraseOverlapIntervals(int[][] intervals) {  
	    Arrays.sort(intervals,(a,b)->(a[1]-b[1]));  
	    int end=intervals[0][1];  
	    int count=1;  
	    for(int i=1;i<intervals.length;i++){  
	        if(intervals[i][0]>=end){  
	            end=intervals[i][1];  
	            count++;  
	        }  
	    }  
	    return intervals.length-count;  
	}
}
```

**Explanation**
1. **Sorting the Intervals**:
    
    - The intervals are first sorted based on their ending points. This means that intervals with earlier end times will come first in the sorted order.
2. **Initialization**:
    
    - An `end` variable is initialized to the end time of the first interval. This variable keeps track of the end time of the last interval that was added to the non-overlapping set.
    - A `count` variable is initialized to 1, representing the number of non-overlapping intervals selected.
3. **Iterating through Intervals**:
    
    - The algorithm iterates through the sorted list of intervals starting from the second interval.
    - For each interval, it checks if its start time is greater than or equal to the `end` time of the last selected interval. If this is true, it means the current interval does not overlap with the last selected interval.
    - If the interval does not overlap, the `end` time is updated to the end time of the current interval, and the `count` of non-overlapping intervals is incremented.
4. **Calculating the Result**:
    
    - After the loop, the total number of intervals that were removed is determined by subtracting the `count` of non-overlapping intervals from the total number of intervals. This gives the minimum number of intervals that need to be removed to eliminate all overlaps.
