#string #slidingWindow #hashmap 
### Question
Given two strings `s1` and `s2`, return `true` _if_ `s2` _contains a permutation of_ `s1`_, or_ `false` _otherwise_.

In other words, return `true` if one of `s1`'s permutations is the substring of `s2`.

**Example 1:**

**Input:** s1 = "ab", s2 = "eidbaooo"
**Output:** true
**Explanation:** s2 contains one permutation of s1 ("ba").

**Example 2:**

**Input:** s1 = "ab", s2 = "eidboaoo"
**Output:** false

### Solution
```java
class Solution{
	public boolean checkInclusion(String s1, String s2) {  
	    int l1=s1.length(),l2=s2.length();  
	    if(l1>l2){  
	        return false;  
	    }  
	    int[] arr1=new int[26];  
	    int[] arr2=new int[26];  
	    for(char c:s1.toCharArray()){  
	        arr1[c-'a']++;  
	    }  
	    for(int i=0;i<l1;i++){  
	        char c=s2.charAt(i);  
	        arr2[c-'a']++;  
	    }  
	    if(checkSame(arr1,arr2)){  
	        return true;  
	    }  
	    for(int i=l1;i<l2;i++){  
	        arr2[s2.charAt(i-l1)-'a']--;  
	        arr2[s2.charAt(i)-'a']++;  
	        if(checkSame(arr1,arr2)){  
	            return true;  
	        }  
	    }  
	    return false;  
	}  
	public boolean checkSame(int[] arr1,int[] arr2){  
	    for(int i=0;i<26;i++){  
	        if(arr1[i]!=arr2[i]){  
	            return false;  
	        }  
	    }  
	    return true;  
	}
}
```

**Explanation**
1. **Initialization**:
    
    - Get the lengths of `s1` (`l1`) and `s2` (`l2`).
    - If `l1` is greater than `l2`, return `false` immediately because it's impossible for `s2` to contain a permutation of `s1`.
2. **Character Frequency Arrays**:
    
    - Two arrays `arr1` and `arr2` of size 26 (for each letter in the alphabet) are used to store the frequency of characters in `s1` and the first `l1` characters of `s2`, respectively.
    - Populate `arr1` with the frequencies of characters in `s1`.
    - Populate `arr2` with the frequencies of the first `l1` characters in `s2`.
3. **Initial Check**:
    
    - Compare `arr1` and `arr2` using the `checkSame` method. If they are the same, it means `s2` contains a permutation of `s1` within the first `l1` characters.
4. **Sliding Window**:
    
    - Iterate through `s2` from `l1` to `l2 - 1` using a sliding window approach:
        - For each new character in the window, decrement the count of the character that is sliding out of the window (`s2.charAt(i-l1)`) and increment the count of the new character (`s2.charAt(i)`).
        - After updating `arr2`, compare it with `arr1` using the `checkSame` method. If they match, return `true`.
5. **Return Result**:
    
    - If no permutation is found in any window, return `false`.
