#string #slidingWindow #hashmap 
### Question
Given two strings `s` and `t` of lengths `m` and `n` respectively, return _the **minimum window**_ **_substring_** _of_ `s` _such that every character in_ `t` _(**including duplicates**) is included in the window_. If there is no such substring, return _the empty string_ `""`.

The testcases will be generated such that the answer is **unique**.

**Example 1:**

**Input:** s = "ADOBECODEBANC", t = "ABC"
**Output:** "BANC"
**Explanation:** The minimum window substring "BANC" includes 'A', 'B', and 'C' from string t.

**Example 2:**

**Input:** s = "a", t = "a"
**Output:** "a"
**Explanation:** The entire string s is the minimum window.

**Example 3:**

**Input:** s = "a", t = "aa"
**Output:** ""
**Explanation:** Both 'a's from t must be included in the window.
Since the largest window of s only has one 'a', return empty string.

### Solution
```java
class Solution{
	public String minWindow(String s, String t) {  
	    int l1=s.length(),l2=t.length();  
	    if(l2>l1){  
	        return "";  
	    }  
	    int start=0,minLen=Integer.MAX_VALUE;  
	    HashMap<Character,Integer>hashMap=new HashMap<>();  
	    for(char c:t.toCharArray()){  
	        hashMap.put(c,hashMap.getOrDefault(c,0)+1);  
	    }  
	    int matches=0;  
	    for(int i=0,j=0;j<l1;j++){  
	        char c=s.charAt(j);  
	        if(hashMap.containsKey(c)){  
	            hashMap.put(c,hashMap.get(c)-1);  
	            if(hashMap.get(c)==0){  
	                matches++;  
	            }  
	        }  
	        while(matches==hashMap.size()){  
	            if(j-i+1<minLen){  
	                minLen=j-i+1;  
	                start=i;  
	            }  
	            c=s.charAt(i++);  
	            if(hashMap.containsKey(c)){  
	                if(hashMap.get(c)==0){  
	                    matches--;  
	                }  
	                hashMap.put(c,hashMap.get(c)+1);  
	            }  
	        }  
	    }  
	    return minLen==Integer.MAX_VALUE?"":s.substring(start,start+minLen);  
	}
}
```

**Explanation**
1. **Initialization**:
    
    - `l1` and `l2` store the lengths of `s` and `t` respectively.
    - If `t` is longer than `s`, it returns an empty string because it's impossible for `s` to contain `t`.
    - `start` and `minLen` are used to track the start of the minimum window and its length.
    - `hashMap` stores the character counts of `t`.
2. **Populate the HashMap**:
    
    - Iterate through `t` to populate the `hashMap` with character counts.
3. **Sliding Window Technique**:
    
    - Use two pointers, `i` (left) and `j` (right), to represent the current window in `s`.
    - `matches` keeps track of how many unique characters from `t` have their required counts in the current window.
4. **Expand the Window**:
    
    - For each character `c` at position `j` in `s`, if `c` is in `hashMap`, decrement its count in `hashMap`.
    - If the count of `c` becomes zero, increment `matches`.
5. **Contract the Window**:
    
    - While `matches` equals the size of `hashMap` (meaning the current window contains all characters of `t` with the required counts), check if the current window size is smaller than `minLen`.
    - If it is, update `start` and `minLen`.
    - Move the left pointer `i` to the right to try to minimize the window size, updating the counts in `hashMap` and `matches` accordingly.
6. **Return the Result**:
    
    - If `minLen` was updated from its initial value, return the substring starting at `start` with length `minLen`.
    - If not, return an empty string (no valid window was found).