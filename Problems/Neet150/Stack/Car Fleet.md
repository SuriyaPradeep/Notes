#stack #sorting 
### Question
There are `n` cars at given miles away from the starting mile 0, traveling to reach the mile `target`.

You are given two integer array `position` and `speed`, both of length `n`, where `position[i]` is the starting mile of the `ith` car and `speed[i]` is the speed of the `ith` car in miles per hour.

A car cannot pass another car, but it can catch up and then travel next to it at the speed of the slower car.

A **car fleet** is a car or cars driving next to each other. The speed of the car fleet is the **minimum** speed of any car in the fleet.

If a car catches up to a car fleet at the mile `target`, it will still be considered as part of the car fleet.

Return the number of car fleets that will arrive at the destination.

**Example 1:**

**Input:** target = 12, position = [10,8,0,5,3], speed = [2,4,1,1,3]

**Output:** 3

**Explanation:**

- The cars starting at 10 (speed 2) and 8 (speed 4) become a fleet, meeting each other at 12. The fleet forms at `target`.
- The car starting at 0 (speed 1) does not catch up to any other car, so it is a fleet by itself.
- The cars starting at 5 (speed 1) and 3 (speed 3) become a fleet, meeting each other at 6. The fleet moves at speed 1 until it reaches `target`.

**Example 2:**

**Input:** target = 10, position = [3], speed = [3]

**Output:** 1

**Explanation:**

There is only one car, hence there is only one fleet.

**Example 3:**

**Input:** target = 100, position = [0,2,4], speed = [4,2,1]

**Output:** 1

**Explanation:**

- The cars starting at 0 (speed 4) and 2 (speed 2) become a fleet, meeting each other at 4. The car starting at 4 (speed 1) travels to 5.
- Then, the fleet at 4 (speed 2) and the car at position 5 (speed 1) become one fleet, meeting each other at 6. The fleet moves at speed 1 until it reaches `target`.

### Solution
```java
class Solution{
	public int carFleet(int target, int[] position, int[] speed) {  
	    Stack<Double> stack=new Stack<>();  
	    int[][] posAndSpeed=new int[position.length][2];  
	    for(int i=0;i<position.length;i++){  
	        posAndSpeed[i][0]=position[i];  
	        posAndSpeed[i][1]=speed[i];  
	    }  
	    Arrays.sort(posAndSpeed,(a,b)->b[0]-a[0]);  
	    for(int i=0;i<posAndSpeed.length;i++){  
	        double time=(double)(target-posAndSpeed[i][0])/(double)posAndSpeed[i][1];  
	        if(stack.isEmpty()){  
	            stack.push(time);  
	        }else{  
	            if(time>stack.peek()){  
	                stack.push(time);  
	            }  
	        }  
	    }  
	    return stack.size();  
	}
}
```

**Explanation**
1. **Initialization**:
    
    - A `Stack<Double>` is used to store the times it takes for each car (or fleet) to reach the target.
    - An `int[][] posAndSpeed` array combines positions and speeds for easier sorting.
2. **Combining Position and Speed**:
    
    - The `posAndSpeed` array is filled with the position and speed of each car.
3. **Sorting**:
    
    - The `posAndSpeed` array is sorted by position in descending order so that cars closer to the target are processed first.
4. **Calculating Times and Forming Fleets**:
    
    - For each car, calculate the time it takes to reach the target.
    - Use the stack to determine whether the current car forms a new fleet or joins an existing one.
        - If the stack is empty or the current car's time is greater than the time of the car on top of the stack, push the current car's time onto the stack, indicating a new fleet.
        - If the current car's time is less than or equal to the time on the stack, it means the current car joins the fleet of the car on the stack.
5. **Return the Result**:
    
    - The size of the stack represents the number of fleets.
