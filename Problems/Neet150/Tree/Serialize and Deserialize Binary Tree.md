#tree #recursion 
### Question
Serialization is the process of converting a data structure or object into a sequence of bits so that it can be stored in a file or memory buffer, or transmitted across a network connection link to be reconstructed later in the same or another computer environment.

Design an algorithm to serialize and deserialize a binary tree. There is no restriction on how your serialization/deserialization algorithm should work. You just need to ensure that a binary tree can be serialized to a string and this string can be deserialized to the original tree structure.

**Clarification:** The input/output format is the same as [how LeetCode serializes a binary tree](https://support.leetcode.com/hc/en-us/articles/360011883654-What-does-1-null-2-3-mean-in-binary-tree-representation-). You do not necessarily need to follow this format, so please be creative and come up with different approaches yourself.

**Example 1:**

![](https://assets.leetcode.com/uploads/2020/09/15/serdeser.jpg)

**Input:** root = [1,2,3,null,null,4,5]
**Output:** [1,2,3,null,null,4,5]

**Example 2:**

**Input:** root = []
**Output:** []

### Solution
```java
public class Codec {  
    int i=0;  
    // Encodes a tree to a single string.  
    public String serialize(TreeNode root) {  
        List<String> ans=new ArrayList<>();  
        dfsSerialize(root,ans);  
        return String.join(",",ans);  
    }  
    public void dfsSerialize(TreeNode root,List<String> list){  
        if(root==null){  
            list.add("N");  
            return;  
        }  
        list.add(String.valueOf(root.val));  
        dfsSerialize(root.left,list);  
        dfsSerialize(root.right,list);  
    }  
  
    // Decodes your encoded data to tree.  
    public TreeNode deserialize(String data) {  
        this.i=0;  
        return dfsDeserialize(data.split(","));  
    }  
    public TreeNode dfsDeserialize(String[] tokens){  
        if(i>=tokens.length || tokens[this.i].equals("N")){  
            this.i++;  
            return null;  
        }  
        TreeNode node=new TreeNode(Integer.parseInt(tokens[this.i++]));  
        node.left=dfsDeserialize(tokens);  
        node.right=dfsDeserialize(tokens);  
        return node;  
    }  
}
```

**Explanation**
1. **Instance Variable `i`**:
    - `int i = 0;`: This variable is used to track the current position in the `tokens` array during the deserialization process. It's reset at the start of deserialization and incremented as you process each token.

2. `serialize(TreeNode root)`:

This method converts a binary tree into a single string.

- **Parameters**:
    
    - `TreeNode root`: The root of the binary tree to be serialized.
- **Process**:
    
    - It creates an empty `List<String>` called `ans` to store the serialized values.
    - It then calls the helper method `dfsSerialize`, which performs a depth-first traversal of the tree, adding the values of nodes to `ans`. `null` nodes are represented as `"N"` in the list.
    - Finally, it joins the elements of `ans` into a single string separated by commas.
- **Output**:
    
    - A single string representing the tree.

3. `dfsSerialize(TreeNode root, List<String> list)`:

This is a helper method for the `serialize` method, which performs a depth-first search (DFS) to serialize the tree.

- **Parameters**:
    
    - `TreeNode root`: The current node being processed.
    - `List<String> list`: The list to which the serialized values are being added.
- **Process**:
    
    - If the current node (`root`) is `null`, it adds `"N"` to the list to represent a `null` node and returns.
    - If the node is not `null`, it adds the node’s value (`root.val`) to the list.
    - It then recursively calls itself to process the left and right children of the node.

4. `deserialize(String data)`:

This method converts the serialized string back into a binary tree.

- **Parameters**:
    
    - `String data`: The serialized string representing the tree.
- **Process**:
    
    - It splits the input string `data` into an array of tokens using `data.split(",")`. Each element in the array corresponds to a node's value or `"N"` for `null`.
    - It resets `i` to `0` to start from the beginning of the tokens array.
    - It calls the helper method `dfsDeserialize` to reconstruct the tree.
- **Output**:
    
    - The root of the reconstructed binary tree.

5. `dfsDeserialize(String[] tokens)`:

This is a helper method for the `deserialize` method, which performs a DFS to reconstruct the tree.

- **Parameters**:
    
    - `String[] tokens`: The array of tokens representing the serialized tree.
- **Process**:
    
    - If `i` is beyond the length of the tokens array (`i >= tokens.length`) or if the current token (`tokens[i]`) is `"N"`, it returns `null` and increments `i`. This handles `null` nodes and base cases where the DFS should terminate.
    - If the current token is a number, it creates a new `TreeNode` with the value of the current token and increments `i`.
    - It then recursively calls `dfsDeserialize` to reconstruct the left and right subtrees and assigns them to `node.left` and `node.right`, respectively.
    - The method returns the `node`, which represents the current subtree.
- **Output**:
    
    - The `TreeNode` that represents the root of the current subtree.