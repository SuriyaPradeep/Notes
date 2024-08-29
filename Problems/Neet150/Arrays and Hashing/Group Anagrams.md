#string #hashmap 
### Question
Given an array of strings `strs`, group **the anagrams** together. You can return the answer in **any order**.

An **Anagram** is a word or phrase formed by rearranging the letters of a different word or phrase, typically using all the original letters exactly once.

**Example 1:**

**Input:** strs = ["eat","tea","tan","ate","nat","bat"]
**Output:** [["bat"],["nat","tan"],["ate","eat","tea"]]

**Example 2:**

**Input:** strs = [""]
**Output:** [[""]]

**Example 3:**

**Input:** strs = ["a"]
**Output:** [["a"]]

### Solution
```java
class Solution{
	public List<List<String>> groupAnagrams(String[] strs) {  
	    HashMap<String,List<String>> hash=new HashMap<>();  
	    for(String str:strs){  
	        char[] chars=str.toCharArray();  
	        Arrays.sort(chars);  
	        String sortedStr=new String(chars);  
	        if(!hash.containsKey(sortedStr)){  
	            hash.put(sortedStr,new ArrayList<>());  
	        }  
	        hash.get(sortedStr).add(str);  
	    }  
	    return new ArrayList<>(hash.values());  
	}
}
```

1. **Initialization**: You initialize a `HashMap` to map the sorted version of each string to a list of its anagrams.
2. **Iteration**: You iterate through each string in the input array.
3. **Sorting**: For each string, you convert it to a character array, sort the array, and then convert it back to a string. This sorted string acts as the key in the `HashMap`.
4. **Grouping Anagrams**: You check if the sorted string key is already in the `HashMap`.
    - If it is not, you add a new entry with the sorted string as the key and a new list as the value.
    - You then add the original string to the list corresponding to the sorted string key.
5. **Return**: Finally, you return the values of the `HashMap` as a list of lists.

