#array #recursion 
### Question
Given an integer array `nums` that may contain duplicates, return _all possible_ _subsets_ _(the power set)_.

The solution set **must not** contain duplicate subsets. Return the solution in **any order**.

**Example 1:**

**Input:** nums = [1,2,2]
**Output:** [[],[1],[1,2],[1,2,2],[2],[2,2]]

**Example 2:**

**Input:** nums = [0]
**Output:** [[],[0]]

### Solution
```java
class Solution{
	public List<List<Integer>> subsetsWithDup(int[] nums) {  
	    List<List<Integer>> ans=new ArrayList<>();  
	    List<Integer> list=new ArrayList<>();  
	    Arrays.sort(nums);  
	    ans.add(new ArrayList<>());  
	    helper(ans,list,nums,0,true);  
	    return ans;  
	}  
	public void helper(List<List<Integer>> ans,List<Integer> list,int[] nums,int n,boolean isPick){  
	    if(n>=nums.length){  
	        return;  
	    }  
	    if(n==0 || nums[n]!=nums[n-1] || isPick){  
	        list.add(nums[n]);  
	        helper(ans,list,nums,n+1,true);  
	        ans.add(new ArrayList<>(list));  
	        list.remove(list.size()-1);  
	    }  
	    helper(ans,list,nums,n+1,false);  
	}
}
```

**Explanation**
1. **Main Function `subsetsWithDup`:**

- **Input:**
    - `nums`: An array of integers, which may include duplicates.
- **Output:**
    - A list of lists (`List<List<Integer>>`) where each inner list is a unique subset of `nums`.
- **Steps:**
    - **Sorting the array:** `Arrays.sort(nums);`
        - Sorting ensures that duplicate elements are adjacent, which helps in avoiding duplicate subsets.
    - **Initial setup:**
        - An empty subset (`[]`) is added to the result list (`ans.add(new ArrayList<>());`).
        - The recursive helper function is called starting from index `0` with an empty subset (`list`) and a flag `isPick` set to `true`.

2. **Helper Function `helper`:**

- **Parameters:**
    - `ans`: The list that stores all valid subsets.
    - `list`: A temporary list that stores the current subset being built.
    - `nums`: The sorted input array.
    - `n`: The current index in the array.
    - `isPick`: A boolean flag that indicates whether the element at index `n-1` was picked or not.
- **Base Case:**
    - `if(n >= nums.length)`: If `n` reaches or exceeds the length of `nums`, the recursion ends.
- **Recursive Case:**
    - The main logic is to decide whether to include the current element (`nums[n]`) in the current subset (`list`).
    - **Include the current element:**
        - The element is added to `list` if one of the following conditions is met:
            1. It’s the first element (`n == 0`).
            2. The current element is different from the previous element (`nums[n] != nums[n-1]`).
            3. The previous element was picked (`isPick == true`).
        - After adding the element, the `helper` function is called recursively to process the next index (`n + 1`) with `isPick` set to `true`.
        - The current subset (`list`) is then added to `ans`.
        - After the recursive call, the last element is removed from `list` to backtrack.
    - **Exclude the current element:**
        - The function is called recursively with the next index (`n + 1`), but this time with `isPick` set to `false`, indicating that the current element is not included in the subset.