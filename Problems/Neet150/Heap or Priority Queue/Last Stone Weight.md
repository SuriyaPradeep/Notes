#priority-queue 
### Question
You are given an array of integers `stones` where `stones[i]` is the weight of the `ith` stone.

We are playing a game with the stones. On each turn, we choose the **heaviest two stones** and smash them together. Suppose the heaviest two stones have weights `x` and `y` with `x <= y`. The result of this smash is:

- If `x == y`, both stones are destroyed, and
- If `x != y`, the stone of weight `x` is destroyed, and the stone of weight `y` has new weight `y - x`.

At the end of the game, there is **at most one** stone left.

Return _the weight of the last remaining stone_. If there are no stones left, return `0`.

**Example 1:**

**Input:** stones = [2,7,4,1,8,1]
**Output:** 1
**Explanation:** 
We combine 7 and 8 to get 1 so the array converts to [2,4,1,1,1] then,
we combine 2 and 4 to get 2 so the array converts to [2,1,1,1] then,
we combine 2 and 1 to get 1 so the array converts to [1,1,1] then,
we combine 1 and 1 to get 0 so the array converts to [1] then that's the value of the last stone.

**Example 2:**

**Input:** stones = [1]
**Output:** 1

### Solution
```java
class Solution{
	public int lastStoneWeight(int[] stones) {  
	    if(stones.length==1){  
	        return stones[0];  
	    }  
	    Queue<Integer> pq=new PriorityQueue<>((a,b)->(b-a));  
	    for(int stone:stones){  
	        pq.add(stone);  
	    }  
	    while(pq.size()>1){  
	        int stone1=pq.poll();  
	        int stone2=pq.poll();  
	        if(stone1!=stone2){  
	            pq.add(stone1-stone2);  
	        }  
	    }  
	    return pq.size()==1?pq.poll():0;  
	}
}
```

**Explanation**
1. **Initial Check**:
    
    - The function first checks if there is only one stone. If so, it returns that stone's weight because there's no other stone to smash it with.
2. **Using a Max-Heap**:
    
    - A max-heap (priority queue) is used to manage the stones. In a max-heap, the largest element is always at the top. This allows the function to efficiently retrieve the heaviest stones at each step.
3. **Inserting Stones into the Heap**:
    
    - All stones are inserted into the max-heap. The heap automatically organizes itself so that the largest stone is always accessible.
4. **Simulating the Smashing Process**:
    
    - The function repeatedly removes the two heaviest stones from the heap.
    - If the stones have the same weight, both are destroyed, and nothing is added back to the heap.
    - If the stones have different weights, the difference between them is computed, and this difference is treated as a new stone. This new stone is then added back to the heap.
    - This process continues until there is only one stone or no stones left in the heap.
5. **Returning the Final Stone**:
    
    - After all possible collisions, if one stone remains, its weight is returned as the result.
    - If no stones remain, the function returns `0`, indicating that all stones have been destroyed.

