#array #hashmap #set 
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

**Explanation**
1. **Initialization**: You initialize a `HashSet` to store unique integers from the array.
2. **Iteration**: You iterate through each element in the array.
3. **Adding to Set**: For each element, you try to add it to the set.
    - If `set.add(num)` returns `false`, it means the element is already in the set, indicating a duplicate.
4. **Return Value**: If a duplicate is found, the method returns `true`. If the loop completes without finding any duplicates, the method returns `false`.

