#stack 
### Question
Given a string `s` containing just the characters `'('`, `')'`, `'{'`, `'}'`, `'['` and `']'`, determine if the input string is valid.

An input string is valid if:

1. Open brackets must be closed by the same type of brackets.
2. Open brackets must be closed in the correct order.
3. Every close bracket has a corresponding open bracket of the same type.

**Example 1:**

**Input:** s = "()"
**Output:** true

**Example 2:**

**Input:** s = "()[]{}"
**Output:** true

**Example 3:**

**Input:** s = "(]"
**Output:** false

### Solution
```java
class Solution{
	public boolean isValid(String s) {  
	    Stack<Character>stack=new Stack<>();  
	    char[] parentheses=s.toCharArray();  
	    Set<Character> set=Set.of('(', '[', '{');  
	    for(char c:parentheses){  
	        if(set.contains(c)){  
	            stack.add(c);  
	        }else{  
	            if(stack.isEmpty()){  
	                return false;  
	            }  
	            char top=stack.pop();  
	            if(top=='(' && c!=')' || top=='[' && c!=']' || top=='{' && c!='}'){  
	                return false;  
	            }  
	        }  
	    }  
	    return stack.isEmpty();  
	}
}
```

**Explanation**
1. **Stack Initialization**:
    
    - `Stack<Character> stack = new Stack<>();` initializes an empty stack to keep track of opening brackets.
2. **Convert String to Character Array**:
    
    - `char[] parentheses = s.toCharArray();` converts the input string to a character array for iteration.
3. **Set of Opening Brackets**:
    
    - `Set<Character> set = Set.of('(', '[', '{');` initializes an immutable set containing the opening brackets.
4. **Iterate through Characters**:
    
    - For each character in the string, check if it is an opening bracket.
    - If it is, push it onto the stack.
    - If it is a closing bracket, check if the stack is empty (indicating a mismatch).
    - Pop the top of the stack and check if it matches the current closing bracket.
5. **Final Check**:
    
    - Ensure the stack is empty at the end. If it is not, there are unmatched opening brackets.
