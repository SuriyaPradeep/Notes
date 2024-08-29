#topK #array #hashmap 
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
	    HashMap<Integer,Integer> hash=new HashMap<>();  
	    for(int num:nums){  
	        hash.put(num,hash.getOrDefault(num,0)+1);  
	    }  
	    List<Integer>[] freq=new List[nums.length+1];  
	    for(Map.Entry<Integer,Integer> map:hash.entrySet()){  
	        int frequency=map.getValue();  
	        if(freq[frequency]==null){  
	            freq[frequency]=new ArrayList<>();  
	        }  
	        freq[frequency].add(map.getKey());  
	    }  
	    int count=0;  
	    int[] ans=new int[k];  
	    for(int i=freq.length-1;i>0 && count<k;i--){  
	        if(freq[i]!=null){  
	            for(int num:freq[i]){  
	                if(count!=k){  
	                    ans[count++]=num;  
	                }  
	            }  
	        }  
	    }  
	    return ans;  
	}
}
```

**Explanation**
1. **Counting Frequencies**: You use a `HashMap` to count the frequency of each element in the array.
2. **Bucket Sort by Frequency**: You create an array of lists, where the index represents the frequency, and each list contains the elements that have that frequency.
3. **Collecting Results**: You iterate through the frequency array from the highest frequency to the lowest, collecting elements until you have kkk elements.

