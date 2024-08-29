#stack 
### Question
Given an array of integers `heights` representing the histogram's bar height where the width of each bar is `1`, return _the area of the largest rectangle in the histogram_.

**Example 1:**

![](https://assets.leetcode.com/uploads/2021/01/04/histogram.jpg)

**Input:** heights = [2,1,5,6,2,3]
**Output:** 10
**Explanation:** The above is a histogram where width of each bar is 1.
The largest rectangle is shown in the red area, which has an area = 10 units.

**Example 2:**

![](https://assets.leetcode.com/uploads/2021/01/04/histogram-1.jpg)

**Input:** heights = [2,4]
**Output:** 4

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
	    public int getKey(){  
	        return key;  
	    }  
	    public int getValue() {  
	        return value;  
	    }  
	}  
	public int largestRectangleArea(int[] heights) {  
	    Stack<Pair> stack=new Stack<>();  
	    int max=0;  
	    for(int i=0;i<heights.length;i++){  
	        int start=i;  
	        while(!stack.isEmpty() && heights[i]<stack.peek().getValue()){  
	            Pair pair=stack.pop();  
	            int index=pair.getKey();  
	            int height=pair.getValue();  
	            max=Math.max(max,(height*(i-index)));  
	            start=index;  
	        }  
	        stack.push(new Pair(start,heights[i]));  
	    }  
	    while(!stack.isEmpty()){  
	        Pair pair=stack.pop();  
	        int index=pair.getKey();  
	        int height=pair.getValue();  
	        max=Math.max(max,(height*(heights.length-index)));  
	    }  
	    return max;  
	}
}
```

**Explanation**
