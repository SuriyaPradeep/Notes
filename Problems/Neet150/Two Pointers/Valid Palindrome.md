#string #2pointer
### Question
A phrase is a **palindrome** if, after converting all uppercase letters into lowercase letters and removing all non-alphanumeric characters, it reads the same forward and backward. Alphanumeric characters include letters and numbers.

Given a string `s`, return `true` _if it is a **palindrome**, or_ `false` _otherwise_.

**Example 1:**

**Input:** s = "A man, a plan, a canal: Panama"
**Output:** true
**Explanation:** "amanaplanacanalpanama" is a palindrome.

**Example 2:**

**Input:** s = "race a car"
**Output:** false
**Explanation:** "raceacar" is not a palindrome.

**Example 3:**

**Input:** s = " "
**Output:** true
**Explanation:** s is an empty string "" after removing non-alphanumeric characters.
Since an empty string reads the same forward and backward, it is a palindrome.

### Solution
```java
class Solution{
	public boolean isPalindrome(String s) {  
	    s=s.toLowerCase();  
	    char[] chars=s.toCharArray();  
	    int left=0,right=chars.length-1;  
	    while(left<right){  
	        char l=chars[left];  
	        char r=chars[right];  
	        if(!Character.isLetterOrDigit(l)){  
	            left++;  
	        }else if(!Character.isLetterOrDigit(r)){  
	            right--;  
	        }else{  
	            if(l!=r){  
	                return false;  
	            }  
	            left++;  
	            right--;  
	        }  
	    }  
	    return true;  
	}
}
```

**Explanation**
1. **Convert to Lowercase**:
    
    - `s = s.toLowerCase();` ensures that the comparison is case-insensitive by converting the entire string to lowercase. This allows you to treat 'A' and 'a' as equal.
2. **Convert to Character Array**:
    
    - `char[] chars = s.toCharArray();` converts the string into an array of characters to facilitate easier index-based access.
3. **Initialize Pointers**:
    
    - `int left = 0, right = chars.length - 1;` initializes two pointers: `left` starts at the beginning of the array and `right` starts at the end.
4. **While Loop**:
    
    - `while (left < right)` ensures that the loop continues until the pointers cross each other or meet.
5. **Skip Non-Alphanumeric Characters**:
    
    - `if (!Character.isLetterOrDigit(l))` checks if the character at the `left` pointer is not alphanumeric. If so, the `left` pointer is incremented to skip the non-alphanumeric character.
    - `else if (!Character.isLetterOrDigit(r))` does the same for the `right` pointer, decrementing it if the character is not alphanumeric.
6. **Compare Characters**:
    
    - `if (l != r)` compares the characters pointed to by `left` and `right`. If they are not equal, the string is not a palindrome, and the method returns `false`.
7. **Update Pointers**:
    
    - `left++` and `right--` move the pointers towards the center of the string after a successful comparison.
8. **Return Result**:
    
    - If the loop completes without finding any mismatches, the string is a palindrome, and the method returns `true`.
