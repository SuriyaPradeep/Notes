#string #recursion 
### Question
Given a string `s`, partition `s` such that every substring of the partition is a **palindrome**. Return _all possible palindrome partitioning of_ `s`.

**Example 1:**

**Input:** s = "aab"
**Output:** [["a","a","b"],["aa","b"]]

**Example 2:**

**Input:** s = "a"
**Output:** [["a"]]

### Solution
```java
class Solution{
	public List<List<String>> partition(String s) {  
	    if(s==null || s.length()==0){  
	        return new ArrayList<>();  
	    }  
	    List<List<String>> ans=new ArrayList<>();  
	    List<String> list=new ArrayList<>();  
	    helper(ans,list,s);  
	    return ans;  
	}  
	public void helper(List<List<String>> ans,List<String> list,String s){  
	    if(s==null || s.length()==0){  
	        ans.add(new ArrayList<>(list));  
	        return;  
	    }  
	    for(int i=1;i<=s.length();i++){  
	        String temp=s.substring(0,i);  
	        if(!isPalindrome(temp)){  
	            continue;  
	        }  
	        list.add(temp);  
	        helper(ans,list,s.substring(i,s.length()));  
	        list.remove(list.size()-1);  
	    }  
	}  
	public boolean isPalindrome(String str){  
	    int left=0,right=str.length()-1;  
	    while(left<right){  
	        if(str.charAt(left)!=str.charAt(right)){  
	            return false;  
	        }  
	        left++;  
	        right--;  
	    }  
	    return true;  
	}
}
```

**Explanation**
1. **Main Function: `partition(String s)`**

- **Purpose:**
    - To return a list of all possible partitions of the string `s` where each substring in the partition is a palindrome.
- **Steps:**
    - First, it checks if the input string `s` is `null` or empty. If so, it returns an empty list.
    - It initializes `ans` as an empty list of lists (`List<List<String>>`) to store the final results.
    - It initializes `list` as an empty list (`List<String>`) to store the current partition being explored.
    - It calls the helper function `helper` to start the backtracking process.

2. **Helper Function: `helper(List<List<String>> ans, List<String> list, String s)`**

- **Purpose:**
    - To perform the backtracking and generate all possible palindromic partitions.
- **Parameters:**
    - `ans`: The final list of lists where each list contains one valid partition of palindromic substrings.
    - `list`: A temporary list that stores the current partition being explored.
    - `s`: The remaining substring that still needs to be partitioned.
- **Base Case:**
    - If `s` is empty (`s.length() == 0`), this means that the current partition in `list` is complete, so it adds a copy of `list` to `ans`.
- **Main Logic:**
    - The loop iterates through possible substrings of `s` using the index `i`. For each possible prefix `s.substring(0, i)`:
        - It checks if this prefix is a palindrome using the `isPalindrome` function.
        - If the prefix is a palindrome, it:
            1. Adds the palindrome substring `temp` to `list`.
            2. Recursively calls `helper` with the remaining substring `s.substring(i)`.
            3. After the recursive call, it removes the last element from `list` (backtracking) to explore other possible partitions.

3. **Helper Function: `isPalindrome(String str)`**

- **Purpose:**
    - To check whether a given string `str` is a palindrome.
- **Logic:**
    - It uses two pointers, `left` and `right`, starting at the beginning and end of the string, respectively.
    - It compares the characters at these two pointers. If they differ, it returns `false`.
    - If all characters match as the pointers move towards each other, it returns `true`, indicating that `str` is a palindrome.