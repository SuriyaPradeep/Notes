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
	        stringBuilder.append(str.length()+"@"+str);  
	    }  
	    return stringBuilder.toString();  
	}  
	  
	public List<String> decode(String str) {  
	    List<String> list = new ArrayList<>();  
	    int i=0;  
	    while(i<str.length()) {  
	        int j=i;  
	        while(str.charAt(j)!='@'){   
	            j++;  
	        }  
	        int length=Integer.valueOf(str.substring(i, j));  
	        i=j+1+length;  
	        list.add(str.substring(j + 1, i));  
	    }  
	    return list;        
	}
}
```

### Explanation
**Encode**
- **Initialize StringBuilder**: Use a `StringBuilder` to efficiently construct the result string.
- **Iterate Over List**: For each string in the input list:
    - Append the length of the string followed by the `@` character.
    - Append the string itself.
- **Return Result**: Convert the `StringBuilder` to a string and return it.

**Decode**
1. **Initialize List**: Create an empty list to store the decoded strings.
2. **Iterate Over Encoded String**: Use a loop to process the encoded string:
    - Find the position of the next `@` character to determine the length of the next string.
    - Extract the length and parse it as an integer.
    - Use the length to extract the actual string.
    - Add the extracted string to the result list.
    - Move the pointer to the start of the next length indicator.
3. **Return Result**: Return the list of decoded strings.

