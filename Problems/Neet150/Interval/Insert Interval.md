#2DArray #intervals 
### Question
You are given an array of non-overlapping intervals `intervals` where `intervals[i] = [starti, endi]` represent the start and the end of the `ith` interval and `intervals` is sorted in ascending order by `starti`. You are also given an interval `newInterval = [start, end]` that represents the start and end of another interval.

Insert `newInterval` into `intervals` such that `intervals` is still sorted in ascending order by `starti` and `intervals` still does not have any overlapping intervals (merge overlapping intervals if necessary).

Return `intervals` _after the insertion_.

**Note** that you don't need to modify `intervals` in-place. You can make a new array and return it.

**Example 1:**

**Input:** intervals = [[1,3],[6,9]], newInterval = [2,5]
**Output:** [[1,5],[6,9]]

**Example 2:**

**Input:** intervals = [[1,2],[3,5],[6,7],[8,10],[12,16]], newInterval = [4,8]
**Output:** [[1,2],[3,10],[12,16]]
**Explanation:** Because the new interval [4,8] overlaps with [3,5],[6,7],[8,10].

### Solution
```java
class Solution{
	public int[][] insert(int[][] intervals, int[] newInterval) {  
	    List<int[]> ans=new ArrayList<>();  
	    for(int[] interval:intervals){  
	        if(interval[0]>newInterval[1]){  
	            ans.add(newInterval);  
	            newInterval=interval;  
	        }else if(interval[1]<newInterval[0]){  
	            ans.add(interval);  
	        }else{  
	            newInterval[0]=Math.min(interval[0],newInterval[0]);  
	            newInterval[1]=Math.max(interval[1],newInterval[1]);  
	        }  
	    }  
	    ans.add(newInterval);  
	    return ans.toArray(new int[ans.size()][]);  
	}
}
```

**Explanation**
1. **Initialization**: The method starts by creating an empty list to hold the final set of intervals after insertion and merging.
    
2. **Iterating Through Intervals**: The method then loops through each interval in the existing list. For each interval, it checks how it relates to the new interval that needs to be inserted.
    
3. **Non-Overlapping Case (New Interval Comes Before)**: If the current interval in the list starts after the new interval ends, it means there is no overlap, and the new interval is inserted before the current interval. The method then continues processing with the current interval now considered the new interval.
    
4. **Non-Overlapping Case (New Interval Comes After)**: If the current interval ends before the new interval starts, there’s no overlap, so the current interval is added to the final list as is, and the new interval remains unchanged.
    
5. **Merging Overlapping Intervals**: If the current interval overlaps with the new interval, the method merges them by adjusting the start to the earliest start time and the end to the latest end time. This ensures the intervals are combined into a single, larger interval.
    
6. **Final Addition**: After all intervals have been processed, the last remaining interval (whether merged or not) is added to the final list.
    
7. **Conversion to Final Format**: Finally, the list of intervals is converted into the required format (a two-dimensional array) and returned.

