#2pointer #array 
### Question
Given an integer array nums, return all the triplets `[nums[i], nums[j], nums[k]]` such that `i != j`, `i != k`, and `j != k`, and `nums[i] + nums[j] + nums[k] == 0`.

Notice that the solution set must not contain duplicate triplets.

**Example 1:**

**Input:** nums = [-1,0,1,2,-1,-4]
**Output:** [[-1,-1,2],[-1,0,1]]
**Explanation:** 
nums[0] + nums[1] + nums[2] = (-1) + 0 + 1 = 0.
nums[1] + nums[2] + nums[4] = 0 + 1 + (-1) = 0.
nums[0] + nums[3] + nums[4] = (-1) + 2 + (-1) = 0.
The distinct triplets are [-1,0,1] and [-1,-1,2].
Notice that the order of the output and the order of the triplets does not matter.

**Example 2:**

**Input:** nums = [0,1,1]
**Output:** []
**Explanation:** The only possible triplet does not sum up to 0.

**Example 3:**

**Input:** nums = [0,0,0]
**Output:** [[0,0,0]]
**Explanation:** The only possible triplet sums up to 0.

### Solution
```java
class Solution{
	public List<List<Integer>> threeSum(int[] nums) {  
	    HashSet<List<Integer>> set=new HashSet<>();  
	    Arrays.sort(nums);  
	    int n=nums.length;;  
	    for(int i=0;i<n-2 && nums[i]<=0;){  
	        int left=i+1,right=n-1;  
	        while(left<right){  
	            int sum=nums[i]+nums[left]+nums[right];  
	            if(sum==0){  
	                set.add(Arrays.asList(nums[i],nums[left],nums[right]));  
	                left++;  
	                while(left<right && nums[left]==nums[left-1]){  
	                    left++;  
	                }  
	            }else if(sum>0){  
	                right--;  
	                while(right>left &&nums[right]==nums[right+1]){  
	                    right--;  
	                }  
	            }else{  
	                left++;  
	                while(left<right && nums[left]==nums[left-1]){  
	                    left++;  
	                }  
	            }  
	        }  
	        i++;  
	        while(i<n-3 && nums[i]==nums[i-1]){  
	            i++;  
	        }  
	    }  
	    return new ArrayList<>(set);  
	}
}
```

**Explanation**
1. **Sort the Array**:
    
    - `Arrays.sort(nums);` sorts the input array to facilitate the two-pointer approach and handle duplicates efficiently.
2. **Iterate through the Array**:
    
    - `for (int i = 0; i < n - 2; i++) {` iterates through the array, fixing one element at a time.
    - `if (i > 0 && nums[i] == nums[i - 1]) { continue; }` skips duplicate elements to avoid redundant triplets.
3. **Initialize Two Pointers**:
    
    - `int left = i + 1, right = n - 1;` initializes the two pointers for the remaining part of the array.
4. **Calculate Sum**:
    
    - `int sum = nums[i] + nums[left] + nums[right];` calculates the sum of the triplet.
    - If `sum == 0`, a valid triplet is found, and it is added to the result list.
    - Adjust pointers: move `left` and `right` inward while skipping duplicate elements.
5. **Avoid Duplicates for Two Pointers**:
    
    - `while (left < right && nums[left] == nums[left - 1]) { left++; }` ensures that we skip duplicate elements for the `left` pointer.
    - `while (left < right && nums[right] == nums[right + 1]) { right--; }` ensures that we skip duplicate elements for the `right` pointer.
