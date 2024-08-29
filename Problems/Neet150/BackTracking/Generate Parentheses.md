#recursion 
### Question
Given `n` pairs of parentheses, write a function to _generate all combinations of well-formed parentheses_.

**Example 1:**

**Input:** n = 3
**Output:** ["((()))","(()())","(())()","()(())","()()()"]

**Example 2:**

**Input:** n = 1
**Output:** ["()"]

### Solution
```java
class Solution{
	public List<String> generateParenthesis(int n) {  
	    List<String> ans=new ArrayList<>();  
	    backTrack(ans,"",0,0,n);  
	    return ans;  
	}  
	public void backTrack(List<String> ans,String str,int openN,int closeN,int n){  
	    if(openN==n && closeN==n){  
	        ans.add(str);  
	        return;  
	    }  
	    if(openN<n){  
	        backTrack(ans,str+"(",openN+1,closeN,n);  
	    }  
	    if(closeN<openN){  
	        backTrack(ans,str+")",openN,closeN+1,n);  
	    }  
	}
}
```

**Explanation**
1. **Initialize**:
        - Create an empty list to store the resulting combinations.
        - Start the backtracking process with an initial empty string and counters for open and close parentheses set to zero.

2. **Backtracking Method**:
    - **Base Case**:
        - If the count of both open and close parentheses reaches `n`, add the current string to the result list. This indicates a complete valid combination.
    - **Recursive Case**:
        - If the count of open parentheses used is less than `n`, add an open parenthesis and make a recursive call.
        - If the count of close parentheses used is less than the count of open parentheses, add a close parenthesis and make a recursive call.