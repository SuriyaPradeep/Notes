#priority-queue 
### Question
You are given an array of CPU `tasks`, each represented by letters A to Z, and a cooling time, `n`. Each cycle or interval allows the completion of one task. Tasks can be completed in any order, but there's a constraint: **identical** tasks must be separated by at least `n` intervals due to cooling time.

​Return the _minimum number of intervals_ required to complete all tasks.

**Example 1:**

**Input:** tasks = ["A","A","A","B","B","B"], n = 2

**Output:** 8

**Explanation:** A possible sequence is: A -> B -> idle -> A -> B -> idle -> A -> B.

After completing task A, you must wait two cycles before doing A again. The same applies to task B. In the 3rd interval, neither A nor B can be done, so you idle. By the 4th cycle, you can do A again as 2 intervals have passed.

**Example 2:**

**Input:** tasks = ["A","C","A","B","D","B"], n = 1

**Output:** 6

**Explanation:** A possible sequence is: A -> B -> C -> D -> A -> B.

With a cooling interval of 1, you can repeat a task after just one other task.

**Example 3:**

**Input:** tasks = ["A","A","A", "B","B","B"], n = 3

**Output:** 10

**Explanation:** A possible sequence is: A -> B -> idle -> idle -> A -> B -> idle -> idle -> A -> B.

There are only two types of tasks, A and B, which need to be separated by 3 intervals. This leads to idling twice between repetitions of these tasks.

### Solution
```java
class Solution{
	class Pair{  
	    int key;  
	    int val;  
	    public Pair(int key,int val){  
	        this.key=key;  
	        this.val=val;  
	    }  
	}  
	public int leastInterval(char[] tasks, int n) {  
	    PriorityQueue<Integer> pq=new PriorityQueue<>((a,b)->b-a);  
	    Queue<Pair> q=new LinkedList<>();  
	    int[] count=new int[26];  
	    for(char task:tasks){  
	        count[task-'A']++;  
	    }  
	    for(int freq:count){  
	        if(freq>0){  
	            pq.add(freq);  
	        }  
	    }  
	    int time=0;  
	    while(!pq.isEmpty() || !q.isEmpty()){  
	        time++;  
	        if(!pq.isEmpty()){  
	            int val=pq.poll();  
	            val--;  
	            if(val>0){  
	                q.add(new Pair(time+n,val));  
	            }  
	        }  
	        if(!q.isEmpty() && q.peek().key==time){  
	            pq.add(q.poll().val);  
	        }  
	    }  
	    return time;  
	}
}
```

**Explanation**
1. **Task Frequency Calculation**:
    
    - The function starts by counting the frequency of each task. Since tasks are represented as characters (`A` to `Z`), an array `count` of size 26 is used to store the frequency of each task.
2. **Priority Queue for Task Execution**:
    
    - A max-heap (using a priority queue `pq`) is then constructed based on the frequencies of tasks. This heap will always allow the most frequent task to be processed first.
3. **Queue for Cooling Period**:
    
    - A separate queue `q` is used to manage the cooling period for tasks. The queue stores pairs of the time when a task can be executed again (after cooling) and its remaining frequency.
4. **Simulation of Task Execution**:
    
    - The process is simulated using a `time` counter that increments with each time unit.
    - At each time unit, the function checks if there is a task that can be executed (from the priority queue). If a task is executed, its frequency is decreased, and if the task still has remaining instances, it's added to the cooling queue with the time when it can be executed again.
    - The function also checks the cooling queue to see if any tasks have completed their cooling period and can be added back to the priority queue.
5. **Completion**:
    
    - The simulation continues until both the priority queue and the cooling queue are empty, meaning all tasks have been executed.
    - The `time` counter, which tracks the total time units, is returned as the result.