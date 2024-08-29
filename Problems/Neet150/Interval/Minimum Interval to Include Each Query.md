#intervals #priority-queue 
### Question
You are given a 2D integer array `intervals`, where `intervals[i] = [lefti, righti]` describes the `ith` interval starting at `lefti` and ending at `righti` **(inclusive)**. The **size** of an interval is defined as the number of integers it contains, or more formally `righti - lefti + 1`.

You are also given an integer array `queries`. The answer to the `jth` query is the **size of the smallest interval** `i` such that `lefti <= queries[j] <= righti`. If no such interval exists, the answer is `-1`.

Return _an array containing the answers to the queries_.

**Example 1:**

**Input:** intervals = [[1,4],[2,4],[3,6],[4,4]], queries = [2,3,4,5]
**Output:** [3,3,1,4]
**Explanation:** The queries are processed as follows:
- Query = 2: The interval [2,4] is the smallest interval containing 2. The answer is 4 - 2 + 1 = 3.
- Query = 3: The interval [2,4] is the smallest interval containing 3. The answer is 4 - 2 + 1 = 3.
- Query = 4: The interval [4,4] is the smallest interval containing 4. The answer is 4 - 4 + 1 = 1.
- Query = 5: The interval [3,6] is the smallest interval containing 5. The answer is 6 - 3 + 1 = 4.

**Example 2:**

**Input:** intervals = [[2,3],[2,5],[1,8],[20,25]], queries = [2,19,5,22]
**Output:** [2,-1,4,6]
**Explanation:** The queries are processed as follows:
- Query = 2: The interval [2,3] is the smallest interval containing 2. The answer is 3 - 2 + 1 = 2.
- Query = 19: None of the intervals contain 19. The answer is -1.
- Query = 5: The interval [2,5] is the smallest interval containing 5. The answer is 5 - 2 + 1 = 4.
- Query = 22: The interval [20,25] is the smallest interval containing 22. The answer is 25 - 20 + 1 = 6.

### Solution
```java
class Solution{
	class Pair{  
	    int key;  
	    int value;  
	    public Pair(int key,int value){  
	        this.key=key;  
	        this.value=value;  
	    }  
	}  
	public int[] minInterval(int[][] intervals, int[] queries) {  
	    int[] queriesSorted=queries.clone();  
	    HashMap<Integer,Integer> map=new HashMap<>();  
	    PriorityQueue<Pair> pq=new PriorityQueue<>((a,b)->(a.key-b.key));  
	    int n=intervals.length;  
	    int m=queries.length;  
	    Arrays.sort(queriesSorted);  
	    Arrays.sort(intervals,(a,b)->(a[0]-b[0]));  
	    int i=0;  
	    for(int query:queriesSorted){  
	        while(i<n && intervals[i][0]<=query){  
	            int l=intervals[i][0];  
	            int r=intervals[i][1];  
	            int size=r-l+1;  
	            pq.add(new Pair(size,r));  
	            i++;  
	        }  
	        while(!pq.isEmpty() && pq.peek().value<query){  
	            pq.poll();  
	        }  
	        map.put(query,pq.isEmpty()?-1:pq.peek().key);  
	    }  
	    int[] ans=new int[m];  
	    i=0;  
	    for(int query:queries){  
	        ans[i++]=map.get(query);  
	    }  
	    return ans;  
	}
}
```

**Explanation**
1. **Input**: The method takes two inputs: a list of intervals (each defined by a start and end point) and a list of query points.
    
2. **Sorting**:
    
    - The intervals are sorted based on their starting points.
    - The queries are also sorted in ascending order. This sorting helps efficiently match intervals to queries as we process them.
3. **Priority Queue**:
    
    - A priority queue (or min-heap) is used to keep track of intervals, specifically storing them based on their sizes (i.e., the difference between their start and end points). The smallest interval is always at the top of this queue.
4. **Processing Queries**:
    
    - The method iterates over each query in the sorted query list. For each query, it considers all intervals that start before or at the query point.
    - These intervals are added to the priority queue. If an interval ends before the current query point (meaning it cannot cover the query), it is removed from the queue.
5. **Storing Results**:
    
    - After processing the intervals for a query, the method checks the priority queue. If the queue is not empty, the smallest interval size that can cover the query is recorded. If no interval can cover the query, the method records `-1`.
6. **Final Output**:

    - The method finally compiles the results for each original query and returns them in the form of an array. This array contains the smallest interval sizes corresponding to each query, or `-1` if no interval covers a query.