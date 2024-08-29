#recursion 
### Question
Given an array of **distinct** integers `candidates` and a target integer `target`, return _a list of all **unique combinations** of_ `candidates` _where the chosen numbers sum to_ `target`_._ You may return the combinations in **any order**.

The **same** number may be chosen from `candidates` an **unlimited number of times**. Two combinations are unique if the frequency of at least one of the chosen numbers is different.

The test cases are generated such that the number of unique combinations that sum up to `target` is less than `150` combinations for the given input.

**Example 1:**

**Input:** candidates = [2,3,6,7], target = 7
**Output:** [[2,2,3],[7]]
**Explanation:**
2 and 3 are candidates, and 2 + 2 + 3 = 7. Note that 2 can be used multiple times.
7 is a candidate, and 7 = 7.
These are the only two combinations.

**Example 2:**

**Input:** candidates = [2,3,5], target = 8
**Output:** [[2,2,2,2],[2,3,3],[3,5]]

**Example 3:**

**Input:** candidates = [2], target = 1
**Output:** []

### Solution
```java
class Solution{
	public List<List<Integer>> combinationSum(int[] candidates, int target) {  
	    List<List<Integer>> ans=new ArrayList<>();  
	    List<Integer> list=new ArrayList<>();  
	    helper(ans,list,candidates,target,0);  
	    return ans;  
	}  
	public void helper(List<List<Integer>> ans,List<Integer> list,int[] candidates,int target,int n){  
	    if(n==candidates.length || target<0){  
	        return;  
	    }  
	    if(target==0){  
	        ans.add(new ArrayList<>(list));  
	        return;  
	    }  
	    list.add(candidates[n]);  
	    helper(ans,list,candidates,target-candidates[n],n);  
	    list.remove(list.size()-1);  
	    helper(ans,list,candidates,target,n+1);  
	}
}
```
**Explanation**
1. **`combinationSum(int[] candidates, int target)`**:
    
    - **Purpose**: This method initializes the process of finding all valid combinations that sum up to the target.
    - **Steps**:
        - Create an empty list `ans` to store all valid combinations.
        - Create an empty list `list` to represent the current combination being explored.
        - Call the helper method `helper(ans, list, candidates, target, 0)` to start the search from the first candidate.
        - Return `ans`, which will contain all valid combinations.
2. **`helper(List<List<Integer>> ans, List<Integer> list, int[] candidates, int target, int n)`**:
    
    - **Purpose**: This method is a recursive helper function that explores different combinations by either including or excluding the current candidate.
    - **Parameters**:
        - `ans`: The list of lists where all valid combinations are stored.
        - `list`: The current combination being explored.
        - `candidates`: The array of candidate numbers.
        - `target`: The remaining target value that needs to be met.
        - `n`: The current index in the `candidates` array.
    - **Base Cases**:
        - **Out of bounds or negative target**: If `n` equals the length of `candidates` or if `target` becomes negative, return without doing anything. This indicates that the current path is invalid.
        - **Target reached**: If `target` is exactly 0, it means the current combination sums up to the target. Add a copy of `list` to `ans`.
    - **Recursive Case**:
        - **Include the current candidate (`candidates[n]`)**: Add `candidates[n]` to `list` and make a recursive call to explore further by reducing the target by `candidates[n]` and keeping `n` the same (since the current candidate can be reused).
        - **Backtrack**: After the recursive call, remove the last element from `list` to undo the inclusion of `candidates[n]`.
        - **Exclude the current candidate**: Make another recursive call to explore the scenario where you skip the current candidate and move on to the next one by increasing `n`.