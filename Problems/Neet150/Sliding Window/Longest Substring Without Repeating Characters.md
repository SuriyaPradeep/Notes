#hashmap #slidingWindow #string 
### Question
Given a string `s`, find the length of the **longest**  **substring** without repeating characters.

**Example 1:**

**Input:** s = "abcabcbb"
**Output:** 3
**Explanation:** The answer is "abc", with the length of 3.

**Example 2:**

**Input:** s = "bbbbb"
**Output:** 1
**Explanation:** The answer is "b", with the length of 1.

**Example 3:**

**Input:** s = "pwwkew"
**Output:** 3
**Explanation:** The answer is "wke", with the length of 3.
Notice that the answer must be a substring, "pwke" is a subsequence and not a substring.

### Solution
```java
class Solution{
	public int lengthOfLongestSubstring(String s) {  
	    HashMap<Character,Integer> hashMap=new HashMap<>();  
	    char[] chars=s.toCharArray();  
	    int maxLen=0;  
	    for(int i=0,j=0;j<chars.length;j++){  
	        char c=chars[j];  
	        if(hashMap.containsKey(c)){  
	            i=Math.max(i,hashMap.get(c)+1);  
	        }  
	        hashMap.put(c,j);  
	        maxLen=Math.max(maxLen,(j-i+1));  
	    }  
	    return maxLen;  
	}
}
```

**Explanation**
1. **Initialize Variables**:
    
    - `HashMap<Character, Integer> hashMap`: This hashmap is used to store the characters of the string as keys and their corresponding latest indices as values.
    - `char[] chars`: Converts the string `s` to a character array for easy access to each character.
    - `int maxLen = 0`: This variable stores the length of the longest substring without repeating characters found so far.
2. **Sliding Window Approach**:
    
    - Two pointers `i` and `j` are used to represent the current window of characters being considered. Initially, both are set to 0.
3. **Iterate Through Characters**:
    
    - The loop iterates through the characters of the string using the `j` pointer.
4. **Check for Repeating Characters**:
    
    - For each character `c = chars[j]`, check if `c` is already present in the hashmap.
    - If `c` is present, it means we have encountered a repeating character. Update the `i` pointer to the position right after the previous occurrence of `c`. Use `Math.max(i, hashMap.get(c) + 1)` to ensure `i` doesn't move backward.
5. **Update HashMap**:
    
    - Update the hashmap with the current character and its index: `hashMap.put(c, j)`.
6. **Calculate and Update Maximum Length**:
    
    - Calculate the length of the current window as `(j - i + 1)` and update `maxLen` if this length is greater than the previously recorded `maxLen`.
7. **Return Maximum Length**:
    
    - After the loop finishes, return the value of `maxLen`.

