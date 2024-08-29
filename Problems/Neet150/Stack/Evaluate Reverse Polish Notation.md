#stack #Math 
### Question
You are given an array of strings `tokens` that represents an arithmetic expression in a [Reverse Polish Notation](http://en.wikipedia.org/wiki/Reverse_Polish_notation).

Evaluate the expression. Return _an integer that represents the value of the expression_.

**Note** that:

- The valid operators are `'+'`, `'-'`, `'*'`, and `'/'`.
- Each operand may be an integer or another expression.
- The division between two integers always **truncates toward zero**.
- There will not be any division by zero.
- The input represents a valid arithmetic expression in a reverse polish notation.
- The answer and all the intermediate calculations can be represented in a **32-bit** integer.

**Example 1:**

**Input:** tokens = ["2","1","+","3","*"]
**Output:** 9
**Explanation:** ((2 + 1) * 3) = 9

**Example 2:**

**Input:** tokens = ["4","13","5","/","+"]
**Output:** 6
**Explanation:** (4 + (13 / 5)) = 6

**Example 3:**

**Input:** tokens = ["10","6","9","3","+","-11","*","/","*","17","+","5","+"]
**Output:** 22
**Explanation:** ((10 * (6 / ((9 + 3) * -11))) + 17) + 5
= ((10 * (6 / (12 * -11))) + 17) + 5
= ((10 * (6 / -132)) + 17) + 5
= ((10 * 0) + 17) + 5
= (0 + 17) + 5
= 17 + 5
= 22

### Solution
```java
class Solution{
	public int evalRPN(String[] tokens) {  
	    Stack<Integer>stack=new Stack<>();  
	    Set<String>set= Set.of("+","-","*","/");  
	    for(String token:tokens){  
	        if(set.contains(token)){  
	            int num2=stack.pop(),num1=stack.pop();  
	            stack.push(calculate(num1,num2,token));  
	        }else{  
	            stack.push(Integer.parseInt(token));  
	        }  
	    }  
	    return stack.pop();  
	}  
	public int calculate(int num1,int num2,String operator){  
	    switch(operator){  
	        case "+":  
	            return num1+num2;  
	        case "-":  
	            return num1-num2;  
	        case "*":  
	            return num1*num2;  
	        case "/":  
	            return num1/num2;  
	        default:  
	            return -1;  
	    }  
	}
}
```

**Explanation**
1. **Initialization**:
    
    - A `Stack<Integer>` is used to store the operands.
    - A `Set<String>` is created to contain the operators (`+`, `-`, `*`, `/`) for easy checking.
2. **Iteration through Tokens**:
    
    - For each token in the input array:
        - If the token is an operator, pop the top two elements from the stack, perform the operation, and push the result back onto the stack.
        - If the token is an operand, parse it as an integer and push it onto the stack.
3. **Calculate Method**:
    
    - This method takes two integers and an operator, performs the specified operation, and returns the result.
4. **Result**:
    
    - The final result is the single remaining element in the stack after processing all tokens.
