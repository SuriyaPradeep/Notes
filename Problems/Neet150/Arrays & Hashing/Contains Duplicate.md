#set #array #hashmap
### Question
Given an integer array `nums`, return `true` if any value appears **at least twice** in the array, and return `false` if every element is distinct.

**Example 1:**
**Input:** nums = [1,2,3,1]
**Output:** true

**Example 2:**
**Input:** nums = [1,2,3,4]
**Output:** false

**Example 3:**
**Input:** nums = [1,1,1,3,3,4,3,2,4,2]
**Output:** true

### Solution
```java
class Solution{
	public boolean containsDuplicate(int[] nums) {  
	    HashSet<Integer> set=new HashSet<>();  
	    for(int num:nums){  
	        if(!set.add(num)){  
	            return true;  
	        }  
	    }  
	    return false;  
	}
}
```

### Explanation
1. **Initialize a HashSet**:
    
    - A `HashSet` named `set` is created to store the unique elements encountered in the array.
    - `HashSet` is used because it offers average O(1) time complexity for insert and lookup operations.
2. **Iterate Through the Array**:
    
    - A `for` loop iterates through each element `num` in the array `nums`.
3. **Check for Duplicates**:
    
    - For each element `num`, attempt to add it to the `set` using `set.add(num)`.
    - The `add` method of `HashSet` returns `true` if the element was successfully added (i.e., it was not already present in the set).
    - If `add` returns `false`, it means the element `num` is already in the set, indicating a duplicate.
4. **Return Result**:
    
    - If a duplicate is found (i.e., `set.add(num)` returns `false`), the method returns `true` immediately.
    - If the loop completes without finding any duplicates, the method returns `false`.
