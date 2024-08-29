#string #hashmap 
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
	    for(int num:count){  
	        if(num!=0){  
	            return false;  
	        }  
	    }  
	    return true;  
	}
}
```

**Explanation**
1. **Initialization**: You initialize an integer array `count` of size 26 to store the frequency of each character for the lowercase English letters.
2. **Count Characters in `s`**: You iterate through each character in string `s` and increment the corresponding position in the `count` array.
3. **Count Characters in `t`**: You iterate through each character in string `t` and decrement the corresponding position in the `count` array.
4. **Check for Anagram**: Finally, you check if all elements in the `count` array are zero. If any element is not zero, it means the strings are not anagrams.

