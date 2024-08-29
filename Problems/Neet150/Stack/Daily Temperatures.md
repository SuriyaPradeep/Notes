#stack 
### Question
Given an array of integers `temperatures` represents the daily temperatures, return _an array_ `answer` _such that_ `answer[i]` _is the number of days you have to wait after the_ `ith` _day to get a warmer temperature_. If there is no future day for which this is possible, keep `answer[i] == 0` instead.

**Example 1:**

**Input:** temperatures = [73,74,75,71,69,72,76,73]
**Output:** [1,1,4,2,1,1,0,0]

**Example 2:**

**Input:** temperatures = [30,40,50,60]
**Output:** [1,1,1,0]

**Example 3:**

**Input:** temperatures = [30,60,90]
**Output:** [1,1,0]

### Solution
```java
class Solution{
	public int[] dailyTemperatures(int[] temperatures) {  
	    int[] ans=new int[temperatures.length];  
	    Stack<Integer>stack=new Stack<>();  
	    for(int i=0;i<temperatures.length;i++){  
	        while(!stack.isEmpty() && temperatures[i]>temperatures[stack.peek()]){  
	            int index=stack.pop();  
	            ans[index]=i-index;  
	        }  
	        stack.push(i);  
	    }  
	    return ans;  
	}
}
```

**Explanation**
- **Initialization**:
    
    - `int[] ans = new int[temperatures.length];` initializes the result array with zeros. This array will store the number of days until a warmer temperature for each day.
    - `Stack<Integer> stack = new Stack<>();` initializes a stack to store the indices of temperatures.
- **Iterating through Temperatures**:
    
    - For each temperature in the array, you do the following:
        - Use a `while` loop to compare the current temperature with the temperature at the index stored on the top of the stack.
        - If the current temperature is higher than the temperature at the index on top of the stack, it means we've found a warmer day for that previous temperature. Pop the index from the stack and calculate the difference in days.
        - Push the current index onto the stack to wait for a future warmer day.
- **Return the Result**:
    
    - After processing all temperatures, return the `ans` array.
