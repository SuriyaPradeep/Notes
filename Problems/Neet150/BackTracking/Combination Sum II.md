Given a collection of candidate numbers (`candidates`) and a target number (`target`), find all unique combinations in `candidates` where the candidate numbers sum to `target`.

Each number in `candidates` may only be used **once** in the combination.

**Note:** The solution set must not contain duplicate combinations.

**Example 1:**

**Input:** candidates = [10,1,2,7,6,1,5], target = 8
**Output:** 
[
[1,1,6],
[1,2,5],
[1,7],
[2,6]
]

**Example 2:**

**Input:** candidates = [2,5,2,1,2], target = 5
**Output:** 
[
[1,2,2],
[5]
]

### Solution
```java
class Solution{
	public List<List<Integer>> combinationSum2(int[] candidates, int target) {  
	    List<List<Integer>> ans=new ArrayList<>();  
	    List<Integer> list=new ArrayList<>();  
	    Arrays.sort(candidates);  
	    helper(ans,list,candidates,target,0);  
	    return ans;  
	}  
	public void helper(List<List<Integer>> ans,List<Integer> list,int[] candidates,int target,int n){  
	    if(target==0){  
	        ans.add(new ArrayList<>(list));  
	        return;  
	    }  
	    for(int i=n;i<candidates.length;i++){  
	        if(i!=n && candidates[i]==candidates[i-1]){  
	            continue;  
	        }  
	        if(candidates[i]>target){  
	            continue;  
	        }  
	        list.add(candidates[i]);  
	        helper(ans,list,candidates,target-candidates[i],i+1);  
	        list.remove(list.size()-1);  
	    }  
	}
}
```

**Explanation**
1. **Main Function `combinationSum2`:**

- **Input:**
    - `candidates`: An array of integers.
    - `target`: The target sum value.
- **Output:**
    - A list of lists (`List<List<Integer>>`) where each inner list is a unique combination of elements from `candidates` that add up to `target`.
- **Steps:**
    - **Sorting the array:** `Arrays.sort(candidates);` The array is sorted to make it easier to handle duplicates and to stop early when the current candidate exceeds the target.
    - **Calling the helper function:** The `helper` function is invoked to generate the combinations recursively. The initial call starts with an empty list (`list`) and index `n = 0`.

2. **Helper Function `helper`:**

- **Parameters:**
    - `ans`: The list that stores all the valid combinations.
    - `list`: A temporary list to store the current combination being built.
    - `candidates`: The input array.
    - `target`: The remaining sum required to reach the target.
    - `n`: The current index in the array from which the function will start considering candidates.
- **Base Case:**
    - `if(target == 0)`: When `target` is reduced to `0`, it means a valid combination has been found. The current combination (`list`) is added to `ans`.
- **Recursive Case:**
    - The loop iterates over the candidates starting from index `n`. For each candidate:
        1. **Skip Duplicates:** `if(i != n && candidates[i] == candidates[i - 1]) continue;`
            - This check ensures that the same number at the same level of recursion isn't considered twice, preventing duplicate combinations.
        2. **Prune the Search:** `if(candidates[i] > target) continue;`
            - Since the array is sorted, if the current candidate is greater than the remaining `target`, there's no point in continuing further, as all subsequent candidates will also be too large.
        3. **Include the Candidate:**
            - The candidate is added to the current combination (`list.add(candidates[i]);`), and the `helper` function is called recursively with the updated `target` (`target - candidates[i]`) and the next index (`i + 1`) to continue searching for valid combinations.
        4. **Backtrack:**
            - After exploring the current path, the last element added is removed from `list` (`list.remove(list.size() - 1);`) to backtrack and explore other potential combinations.