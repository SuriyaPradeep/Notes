#sorting #hashmap 
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
	    HashMap<String,List<String>>hash=new HashMap<>();  
	    for(String str:strs){  
	        char[] chars=str.toCharArray();  
	        Arrays.sort(chars);  
	        String sorted=new String(chars);  
	        if(!hash.containsKey(sorted)){  
	            hash.put(sorted,new ArrayList<>());  
	        }  
	        hash.get(sorted).add(str);  
	    }  
	    List<List<String>>ans=new ArrayList<>();  
	    for(Map.Entry<String,List<String>>map:hash.entrySet()){  
	        ans.add(map.getValue());  
	    }  
	    return ans;  
	}
}
```

### Explanation
1. **Initialize a HashMap**:
    
    - A `HashMap<String, List<String>>` named `hash` is created to store the sorted version of the strings as keys and lists of anagrams as values.
2. **Iterate Through the Array of Strings**:
    
    - A `for` loop iterates through each string `str` in the array `strs`.
3. **Sort the Characters in Each String**:
    
    - Convert the string `str` to a character array: `char[] chars = str.toCharArray()`.
    - Sort the character array: `Arrays.sort(chars)`.
    - Convert the sorted character array back to a string: `String sorted = new String(chars)`.
4. **Group the Anagrams**:
    
    - Check if the sorted string `sorted` is already a key in the `hash` map.
    - If it is not a key, create a new entry with the sorted string as the key and an empty list as the value: `hash.put(sorted, new ArrayList<>())`.
    - Add the original string `str` to the list corresponding to the sorted string key: `hash.get(sorted).add(str)`.
5. **Collect the Results**:
    
    - Initialize a list `ans` to store the groups of anagrams: `List<List<String>> ans = new ArrayList<>()`.
    - Iterate through the entries in the `hash` map and add each list of anagrams to the `ans` list.
6. **Return the Result**:
    
    - Return the list `ans` which contains the grouped anagrams.

