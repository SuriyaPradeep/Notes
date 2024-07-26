#hashmap 
### Question
Given two strings `s` and `t`, return `true` _if_ `t` _is an anagram of_ `s`_, and_ `false` _otherwise_.

An **Anagram** is a word or phrase formed by rearranging the letters of a different word or phrase, typically using all the original letters exactly once.

**Example 1:**

**Input:** s = "anagram", t = "nagaram"
**Output:** true

**Example 2:**

**Input:** s = "rat", t = "car"
**Output:** false


### Solution 
```java
class Solution{
	public boolean isAnagram(String s, String t) {  
	    int[] count=new int[26];  
	    for(char c:s.toCharArray()){  
	        count[c-'a']++;  
	    }  
	    for(char c:t.toCharArray()){  
	        count[c-'a']--;  
	    }  
	    for(int i=0;i<26;i++){  
	        if(count[i]!=0){  
	            return false;  
	        }  
	    }  
	    return true;  
	}
}
```

### Explanation
1. **Initialize a Count Array**:
    
    - An integer array `count` of size 26 is created to store the frequency of each character in the strings.
    - The array size 26 corresponds to the 26 letters of the English alphabet (a-z).
2. **Count Characters in String `s`**:
    
    - Iterate through each character `c` in the string `s`.
    - For each character `c`, increment the corresponding index in the `count` array. The index is calculated as `c - 'a'`, which converts the character to an index from 0 to 25.
3. **Count Characters in String `t`**:
    
    - Iterate through each character `c` in the string `t`.
    - For each character `c`, decrement the corresponding index in the `count` array.
4. **Check for Anagram**:
    
    - Iterate through the `count` array.
    - If any value in the `count` array is not zero, it means the strings `s` and `t` do not have the same characters in the same frequency, so they are not anagrams.
    - If all values in the `count` array are zero, the strings are anagrams.

