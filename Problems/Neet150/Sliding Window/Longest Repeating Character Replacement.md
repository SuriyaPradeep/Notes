#string #slidingWindow #hashmap 
### Question
You are given a string `s` and an integer `k`. You can choose any character of the string and change it to any other uppercase English character. You can perform this operation at most `k` times.

Return _the length of the longest substring containing the same letter you can get after performing the above operations_.

**Example 1:**

**Input:** s = "ABAB", k = 2
**Output:** 4
**Explanation:** Replace the two 'A's with two 'B's or vice versa.

**Example 2:**

**Input:** s = "AABABBA", k = 1
**Output:** 4
**Explanation:** Replace the one 'A' in the middle with 'B' and form "AABBBBA".
The substring "BBBB" has the longest repeating letters, which is 4.
There may exists other ways to achieve this answer too.
### Solution
```java
class Solution{
	public int characterReplacement(String s, int k) {  
	    int[] count=new int[26];  
	    int maxLen=0,mostFreq=0;  
	    for(int i=0,j=0;j<s.length();j++){  
	        char c=s.charAt(j);  
	        count[c-'A']++;  
	        mostFreq=Math.max(mostFreq,count[c-'A']);  
	        int letterChange=(j-i+1)-mostFreq;  
	        if(letterChange>k){  
	            c=s.charAt(i++);  
	            count[c-'A']--;  
	        }  
	        maxLen=Math.max(maxLen,j-i+1);  
	    }  
	    return maxLen;  
	}
}
```

**Explanation**
1. **Initialization**:
    
    - `count`: an array to keep track of the frequency of each character in the current window. Since the input is uppercase English letters, the size of the array is 26.
    - `maxLen`: stores the maximum length of the substring found.
    - `mostFreq`: keeps track of the most frequent character count in the current window.
2. **Sliding Window Technique**:
    
    - Use two pointers, `i` (left) and `j` (right), to represent the current window in `s`.
    - Iterate through `s` with `j` and update the frequency of the character `c` at position `j`.
3. **Update Most Frequent Character**:
    
    - Update `mostFreq` with the maximum frequency of any character in the current window.
4. **Check Window Validity**:
    
    - Calculate the number of character changes needed to make all characters in the current window the same as the most frequent character: `letterChange = (j - i + 1) - mostFreq`.
    - If `letterChange` exceeds `k`, it means more than `k` replacements are needed, so move the left pointer `i` to the right to shrink the window until it becomes valid again.
5. **Update Maximum Length**:
    
    - Update `maxLen` with the maximum length of the valid window found so far.
6. **Return Result**:
    
    - Return the `maxLen`, which is the length of the longest substring that can be obtained by replacing at most `k` characters.
