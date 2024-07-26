#hashmap 
### Question
Given an integer array `nums` and an integer `k`, return _the_ `k` _most frequent elements_. You may return the answer in **any order**.

**Example 1:**

**Input:** nums = [1,1,1,2,2,3], k = 2
**Output:** [1,2]

**Example 2:**

**Input:** nums = [1], k = 1
**Output:** [1]

### Solution
```java
class Solution{
	public int[] topKFrequent(int[] nums, int k) {  
	    HashMap<Integer,Integer>hash=new HashMap<>();  
	    for(int num:nums){  
	        hash.put(num,hash.getOrDefault(num,0)+1);  
	    }  
	    List<Integer>[] list=new List[nums.length+1];  
	    for(Map.Entry<Integer,Integer> map:hash.entrySet()){  
	        int freq=map.getValue();  
	        if(list[freq]==null){  
	            list[freq]=new ArrayList<>();  
	        }  
	        list[freq].add(map.getKey());  
	    }  
	    int[] ans=new int[k];  
	    int j=0;  
	    for(int i=list.length-1;i>=0 && k>j;i--){  
	        if(list[i]!=null){  
	            for(int num:list[i]){  
	                ans[j++]=num;  
	            }  
	        }  
	    }  
	    return ans;  
	}
}
```

### Explanation
- **Count the Frequencies**:
    
    - Initialize a `HashMap<Integer, Integer>` named `hash` to store the frequency of each element in `nums`.
    - Iterate through the array `nums`, and for each element `num`, increment its count in the `hash` map using `hash.getOrDefault(num, 0) + 1`.
- **Bucket Sort by Frequency**:
    
    - Create an array of lists named `list` where the index represents the frequency of elements, and each list at index `i` contains the elements with frequency `i`.
    - Iterate through the `hash` map's entries, and for each entry, get the frequency `freq` and add the corresponding key to the list at `list[freq]`.
- **Collect the Top `k` Frequent Elements**:
    
    - Initialize an integer array `ans` of size `k` to store the result.
    - Iterate through the `list` array from the highest frequency to the lowest frequency, and for each non-null list, add its elements to `ans` until `k` elements are added.
- **Return the Result**:
    
    - Return the `ans` array containing the top `k` frequent elements.

