#topK #priority-queue #2DArray 
### Question
Given an array of `points` where `points[i] = [xi, yi]` represents a point on the **X-Y** plane and an integer `k`, return the `k` closest points to the origin `(0, 0)`.

The distance between two points on the **X-Y** plane is the Euclidean distance (i.e., `√(x1 - x2)2 + (y1 - y2)2`).

You may return the answer in **any order**. The answer is **guaranteed** to be **unique** (except for the order that it is in).

**Example 1:**

![](https://assets.leetcode.com/uploads/2021/03/03/closestplane1.jpg)

**Input:** points = [[1,3],[-2,2]], k = 1
**Output:** [[-2,2]]
**Explanation:**
The distance between (1, 3) and the origin is sqrt(10).
The distance between (-2, 2) and the origin is sqrt(8).
Since sqrt(8) < sqrt(10), (-2, 2) is closer to the origin.
We only want the closest k = 1 points from the origin, so the answer is just [[-2,2]].

**Example 2:**

**Input:** points = [[3,3],[5,-1],[-2,4]], k = 2
**Output:** [[3,3],[-2,4]]
**Explanation:** The answer [[-2,4],[3,3]] would also be accepted.

### Solution
```java
class Solution{
	public int[][] kClosest(int[][] points, int k) {  
	    Queue<int[]> pq=new PriorityQueue<>((a, b)->Double.compare(distance(a), distance(b)));  
	    for(int[] point:points){  
	        pq.add(point);  
	    }  
	    int[][] ans=new int[k][2];  
	    for(int i=0;i<k;i++){  
	        int[] point=pq.poll();  
	        ans[i][0]=point[0];  
	        ans[i][1]=point[1];  
	    }  
	    return ans;  
	}  
	public double distance(int[] point){  
	    int x=point[0];  
	    int y=point[1];  
	    x=x*x;  
	    y=y*y;  
	    double xy=x+y;  
	    return Math.sqrt(xy);  
	}
}
```

**Explanation**
1. **Max-Heap Implementation**:
    
    - The `PriorityQueue` is used as a max-heap by reversing the comparator (i.e., comparing `b` with `a`), which keeps the farthest point at the top of the heap.
    - By maintaining only `k` elements in the heap, the largest element (farthest point) is efficiently removed whenever the size exceeds `k`.
2. **Distance Calculation**:
    
    - The `distance` method now calculates the squared distance without taking the square root, which is unnecessary for comparison.
3. **Heap Size Control**:
    
    - By keeping the heap size limited to `k`, the solution becomes more efficient, especially when the input `points` array is large.

