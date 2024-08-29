#string 
### Question
Design an algorithm to encode a list of strings to a single string. The encoded string is then decoded back to the original list of strings.

Please implement `encode` and `decode`

**Example 1:**

```java
Input: ["neet","code","love","you"]

Output:["neet","code","love","you"]
```


**Example 2:**

```java
Input: ["we","say",":","yes"]

Output: ["we","say",":","yes"]
```

### Solution
```java
class Solution{
	public String encode(List<String> strs) {  
	    StringBuilder stringBuilder=new StringBuilder();  
	    for(String str:strs){  
	        int n=str.length();  
	        stringBuilder.append(n+"#"+str);  
	    }  
	    return stringBuilder.toString();  
	}  
	  
	public List<String> decode(String str) {  
	    List<String> strs=new ArrayList<>();  
	    for(int i=0;i<str.length();){  
	        int len,j=i;  
	        while(str.charAt(j)!='#'){  
	            j++;  
	        }  
	        len=Integer.valueOf(str.substring(i,j));  
	        strs.add(str.substring(j,j+len+1));  
	        i=j+len+1;  
	    }  
	    return strs;  
	}
}
```

**Explanation**

**Encoding**

1. **Initialization**: You initialize a `StringBuilder` to construct the encoded string.
2. **Iteration**: You iterate through each string in the list.
3. **Concatenation**: For each string, you append its length followed by a delimiter `#` and the string itself to the `StringBuilder`.
4. **Return**: You return the constructed string.

**Decoding**

1. **Initialization**: You initialize an empty list to store the decoded strings.
2. **Iteration**: You iterate through the encoded string.
3. **Extract Length**: You find the length of each string by locating the delimiter `#`.
4. **Extract String**: You extract the string of the given length and add it to the list.
5. **Continue**: You continue the process until the end of the encoded string.