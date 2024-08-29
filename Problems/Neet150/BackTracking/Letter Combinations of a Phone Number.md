#string #recursion 
### Question
Given a string containing digits from `2-9` inclusive, return all possible letter combinations that the number could represent. Return the answer in **any order**.

A mapping of digits to letters (just like on the telephone buttons) is given below. Note that 1 does not map to any letters.

![](https://assets.leetcode.com/uploads/2022/03/15/1200px-telephone-keypad2svg.png)

**Example 1:**

**Input:** digits = "23"
**Output:** ["ad","ae","af","bd","be","bf","cd","ce","cf"]

**Example 2:**

**Input:** digits = ""
**Output:** []

**Example 3:**

**Input:** digits = "2"
**Output:** ["a","b","c"]

### Solution
```java
class Solution{
	public List<String> letterCombinations(String digits) {  
	    if(digits==null || digits.length()==0){  
	        return new ArrayList<>();  
	    }  
	    List<String> ans=new ArrayList<>();  
	    HashMap<Character,String> keyPair=new HashMap<>(){{  
	        put('2',"abc");  
	        put('3',"def");  
	        put('4',"ghi");  
	        put('5',"jkl");  
	        put('6',"mno");  
	        put('7',"pqrs");  
	        put('8',"tuv");  
	        put('9',"wxyz");  
	    }};  
	    helper(ans,digits,keyPair,"");  
	    return ans;  
	}  
	public void helper(List<String> ans,String digits,HashMap<Character,String> keyPair,String s){  
	    if(digits==null || digits.length()==0){  
	        ans.add(s);  
	        return;  
	    }  
	    char digit=digits.charAt(0);  
	    String letters=keyPair.get(digit);  
	    for(char letter:letters.toCharArray()){  
	        helper(ans,digits.substring(1),keyPair,s+letter);  
	    }  
	}
}
```

**Explanation**
The task is to generate all possible letter combinations that can be formed from a string of digits, using the mapping of digits to letters as found on a traditional phone keypad. For example, the digit '2' corresponds to the letters "abc", '3' to "def", and so on.

**Main Method**

The main function is responsible for initiating the process. It checks if the input string of digits is either `null` or empty. If it is, the function immediately returns an empty list because no combinations can be formed.

If the input is valid, the function then creates a mapping of each digit (from '2' to '9') to its corresponding letters using a `HashMap`. This map acts as a lookup table that will be used later to retrieve the possible letters for each digit.

The function then calls a helper method, which is where the main logic for generating combinations occurs. It passes the list to store results, the digits to be processed, the digit-to-letter map, and an initially empty string that will build up the combinations.

**Helper Method**

The helper function is a recursive method, which means it calls itself to break down the problem into smaller parts until a base case is reached.

- **Base Case:**
    
    - The method checks if the string of digits is empty. If it is, it means that all digits have been processed, and the current combination of letters is complete. This complete combination is then added to the result list.
- **Recursive Case:**
    
    - The method focuses on the first digit of the remaining string of digits. It retrieves the corresponding letters from the map.
    - For each letter that corresponds to this digit, the helper function recursively calls itself with the updated combination (adding the current letter) and the rest of the digits.

This recursive process continues until all possible combinations have been generated. Once the recursion completes, the main method returns the list of all generated combinations.