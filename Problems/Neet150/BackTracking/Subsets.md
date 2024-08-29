#array #recursion 
### Question
Given an integer array `nums` of **unique** elements, return _all possible_ _subsets_  _(the power set)_.The solution set **must not** contain duplicate subsets. Return the solution in **any order**.

**Example 1:**

**Input:** nums = [1,2,3]
**Output:** [[],[1],[2],[1,2],[3],[1,3],[2,3],[1,2,3]]

**Example 2:**

**Input:** nums = [0]
**Output:** [[],[0]]
### Solution
```java
class Solution{
	public List<List<Integer>> subsets(int[] nums) {  
	    List<List<Integer>> ans=new ArrayList<>();  
	    List<Integer> list=new ArrayList<>();  
	    helper(ans,list,nums,0);  
	    return ans;  
	}  
	public void helper(List<List<Integer>> ans,List<Integer> list,int[] nums,int n){  
	    if(n>=nums.length){  
	        ans.add(new ArrayList<>(list));  
	        return;  
	    }  
	    list.add(nums[n]);  
	    helper(ans,list,nums,n+1);  
	    list.remove(list.size()-1);  
	    helper(ans,list,nums,n+1);  
	}
}
```

**Explanation**
1. **`subsets(int[] nums)`**:
    
    - **Purpose**: This method initializes the process of finding all subsets of the input array `nums`.
    - **Steps**:
        - Create an empty list `ans` that will store all the subsets.
        - Create an empty list `list` that represents the current subset being explored.
        - Call the helper method `helper(ans, list, nums, 0)` to start generating subsets from the first element.
        - Return `ans` which now contains all the subsets of `nums`.
2. **`helper(List<List<Integer>> ans, List<Integer> list, int[] nums, int n)`**:
    
    - **Purpose**: This method is a recursive helper function that generates subsets by either including or excluding the current element `nums[n]`.
    - **Parameters**:
        - `ans`: The list of lists where all subsets are stored.
        - `list`: The current subset being explored.
        - `nums`: The original array of numbers.
        - `n`: The current index in the array `nums` that the method is considering.
    - **Base Case**: If `n` is greater than or equal to the length of `nums`, it means you've considered all elements in the array. At this point:
        - Add the current subset `list` (as a new `ArrayList`) to `ans`.
        - Return from the recursion.
    - **Recursive Case**:
        - **Include the current element (`nums[n]`)**: Add `nums[n]` to `list`, then recursively call `helper` for the next index (`n + 1`).
        - **Backtrack**: After the recursive call, remove the last element from `list` to undo the inclusion of `nums[n]` and explore the case where you exclude it.
        - **Exclude the current element**: After backtracking, make a recursive call to `helper` without including `nums[n]`.