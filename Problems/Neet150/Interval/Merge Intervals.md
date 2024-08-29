#2DArray #intervals 
### Question
Given an array of `intervals` where `intervals[i] = [starti, endi]`, merge all overlapping intervals, and return _an array of the non-overlapping intervals that cover all the intervals in the input_.

**Example 1:**

**Input:** intervals = [[1,3],[2,6],[8,10],[15,18]]
**Output:** [[1,6],[8,10],[15,18]]
**Explanation:** Since intervals [1,3] and [2,6] overlap, merge them into [1,6].

**Example 2:**

**Input:** intervals = [[1,4],[4,5]]
**Output:** [[1,5]]
**Explanation:** Intervals [1,4] and [4,5] are considered overlapping.

### Solution
```java
class Solution{
	public int[][] merge(int[][] intervals) {  
	    Arrays.sort(intervals,(a,b)->(a[0]-b[0]));  
	    int start=intervals[0][0];  
	    int end=intervals[0][1];  
	    List<int[]> list=new ArrayList<>();  
	    for(int i=1;i<intervals.length;i++){  
	        int[] interval=intervals[i];  
	        if(interval[0]<=end){  
	            start=Math.min(start,interval[0]);  
	            end=Math.max(end,interval[1]);  
	        }else{  
	            list.add(new int[]{start,end});  
	            start=interval[0];  
	            end=interval[1];  
	        }  
	    }  
	    list.add(new int[]{start,end});  
	    return list.toArray(new int[list.size()][]);  
	}
}
```

**Explanation**
1. **Sorting the Intervals**:
    
    - The method begins by sorting the intervals based on their starting points. This ensures that once sorted, any overlapping intervals will be adjacent to each other in the list.
2. **Initialization**:
    
    - After sorting, the method initializes two variables, `start` and `end`, to represent the start and end of the first interval in the list. A list is also initialized to store the merged intervals.
3. **Iterating Through the Intervals**:
    
    - The method then loops through the rest of the intervals (starting from the second one). For each interval, it checks if there is an overlap with the current interval being tracked (represented by `start` and `end`).
4. **Merging Overlapping Intervals**:
    
    - If the current interval overlaps with the tracked interval (i.e., its start is less than or equal to the tracked end), the method updates the `end` to be the maximum of the current end and the tracked end. This ensures that any overlapping intervals are merged together.
5. **Handling Non-Overlapping Intervals**:
    
    - If the current interval does not overlap (i.e., its start is greater than the tracked end), the method adds the tracked interval to the list of merged intervals. Then, it updates the `start` and `end` to the current interval, starting a new interval for potential merging.
6. **Final Addition**:
    
    - After the loop, the last tracked interval is added to the list of merged intervals, ensuring that no interval is left out.
7. **Conversion to Final Format**:
    
    - Finally, the list of merged intervals is converted into the required format (a two-dimensional array) and returned.