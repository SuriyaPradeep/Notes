#array #recursion 
### Question
Given an array `nums` of distinct integers, return _all the possible permutations_. You can return the answer in **any order**.

**Example 1:**

**Input:** nums = [1,2,3]
**Output:** [[1,2,3],[1,3,2],[2,1,3],[2,3,1],[3,1,2],[3,2,1]]

**Example 2:**

**Input:** nums = [0,1]
**Output:** [[0,1],[1,0]]

**Example 3:**

**Input:** nums = [1]
**Output:** [[1]]

### Solution
```java
class Solution{
	public List<List<Integer>> permute(int[] nums) {  
	    List<List<Integer>> ans=new ArrayList<>();  
	    helper(ans,nums,0);  
	    return ans;  
	}  
	public void helper(List<List<Integer>> ans,int[] nums,int n){  
	    if(n==nums.length){  
	        List<Integer> list=new ArrayList<>();  
	        for(int num:nums){  
	            list.add(num);  
	        }  
	        ans.add(list);  
	        return;  
	    }  
	    for(int i=n;i<nums.length;i++){  
	        swap(nums,i,n);  
	        helper(ans,nums,n+1);  
	        swap(nums,i,n);  
	    }  
	}  
	public void swap(int[] nums,int i,int j){  
	    int temp=nums[i];  
	    nums[i]=nums[j];  
	    nums[j]=temp;  
	}
}
```

**Explanation**
1. **Main Function `permute`:**
    
    - It takes an integer array `nums` as input and returns a list of lists, where each inner list is a permutation of `nums`.
    - It initializes an empty list `ans` to store the permutations and then calls the `helper` function to generate permutations recursively.
2. **Helper Function `helper`:**
    
    - This function is responsible for generating the permutations by swapping elements in the `nums` array.
    - It takes the current list `ans`, the array `nums`, and an index `n` as arguments.
    - The base case checks if `n` is equal to the length of `nums`, meaning all positions in the array have been fixed. At this point, the current permutation is added to the list `ans`.
    - If `n` is not the last index, the function loops through the array, swapping the element at index `n` with every element from `n` to the end of the array. It then recursively calls itself with `n + 1`, effectively generating permutations by fixing each element in turn.
    - After the recursive call, the elements are swapped back to restore the original order, ensuring the function explores all possible permutations.
3. **Swap Function `swap`:**
    
    - This simple utility function swaps two elements in the array `nums` at indices `i` and `j`.