#2DArray #intervals 
### Question
Given an array of meeting time interval objects consisting of start and end times `[[start_1,end_1],[start_2,end_2],...] (start_i < end_i)`, find the minimum number of days required to schedule all meetings without any conflicts.

**Example 1:**

```java
Input: intervals = [(0,40),(5,10),(15,20)]

Output: 2
```


Explanation:  
day1: (0,40)  
day2: (5,10),(15,20)

**Example 2:**

```java
Input: intervals = [(4,9)]

Output: 1
```

### Solution
```java
class Solution{
	public int minMeetingRooms(List<Interval> intervals) {  
	    if(intervals.size()==0){  
	        return 0;  
	    }  
	    int n=intervals.size();  
	    int[] start=new int[n];  
	    int[] end=new int[n];  
	    for(int i=0;i<n;i++){  
	        start[i]=intervals.get(i).start;  
	        end[i]=intervals.get(i).end;  
	    }  
	    Arrays.sort(start);  
	    Arrays.sort(end);  
	    int res,count,s,e;  
	    res=count=s=e=0;  
	    while(s<start.length){  
	        if(start[s]<end[e]){  
	            s++;  
	            count++;  
	        }else{  
	            e++;  
	            count--;  
	        }  
	        res=Math.max(res,count);  
	    }  
	    return res;  
	}
}
```

**Explanation**
1. **Extract Start and End Times**:
    
    - It extracts the start and end times from each meeting interval into two separate arrays, `start` and `end`.
2. **Sort the Times**:
    
    - The `start` array is sorted to order the meetings by their starting times.
    - The `end` array is sorted to order the meetings by their ending times.
3. **Two-Pointer Technique**:
    
    - Two pointers, `s` and `e`, are used to traverse the `start` and `end` arrays, respectively.
    - A `count` variable tracks the number of ongoing meetings (i.e., meetings that have started but not yet ended).
4. **Calculate Meeting Rooms**:
    
    - As long as the start time of the next meeting (`start[s]`) is before the end time of the earliest ending meeting (`end[e]`), a new meeting room is required (`count` is incremented).
    - If the start time of the next meeting is after or exactly at the end time of the earliest ending meeting, the meeting room is freed up (`count` is decremented), and the end pointer `e` is moved to the next meeting.
    - The `res` variable keeps track of the maximum value of `count` encountered, which represents the peak number of simultaneous meetings.
5. **Return Result**:
    
    - The function returns `res`, the maximum number of meeting rooms required at any time.