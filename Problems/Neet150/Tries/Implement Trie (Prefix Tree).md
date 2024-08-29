#tries 
### Question
A [**trie**](https://en.wikipedia.org/wiki/Trie) (pronounced as "try") or **prefix tree** is a tree data structure used to efficiently store and retrieve keys in a dataset of strings. There are various applications of this data structure, such as autocomplete and spellchecker.

Implement the Trie class:

- `Trie()` Initializes the trie object.
- `void insert(String word)` Inserts the string `word` into the trie.
- `boolean search(String word)` Returns `true` if the string `word` is in the trie (i.e., was inserted before), and `false` otherwise.
- `boolean startsWith(String prefix)` Returns `true` if there is a previously inserted string `word` that has the prefix `prefix`, and `false` otherwise.

**Example 1:**

**Input**
["Trie", "insert", "search", "search", "startsWith", "insert", "search"]
[[], ["apple"], ["apple"], ["app"], ["app"], ["app"], ["app"]]
**Output**
[null, null, true, false, true, null, true]

**Explanation**
Trie trie = new Trie();
trie.insert("apple");
trie.search("apple");   // return True
trie.search("app");     // return False
trie.startsWith("app"); // return True
trie.insert("app");
trie.search("app");     // return True


### Solution
```java
class Trie {  
  
    class Node{  
        char val;  
        Node[] next;  
        boolean isWord;  
        public Node(char val){  
            this.val=val;  
            next=new Node[26];  
            isWord=false;  
        }  
    }  
  
    Node root;  
  
    public Trie() {  
        root=new Node('\0');  
    }  
  
    public void insert(String word) {  
        Node curr=root;  
        char[] chars=word.toCharArray();  
        for(char c:chars){  
            if(curr.next[c-'a']==null){  
                curr.next[c-'a']=new Node(c);  
            }  
            curr=curr.next[c-'a'];  
        }  
        curr.isWord=true;  
    }  
  
    public Node helper(String word){  
        char[] chars=word.toCharArray();  
        Node curr=root;  
        for(char c:chars){  
            if(curr.next[c-'a']==null){  
                return null;  
            }  
            curr=curr.next[c-'a'];  
        }  
        return curr;  
    }  
  
    public boolean search(String word) {  
        Node res=helper(word);  
        return res!=null && res.isWord;  
    }  
  
    public boolean startsWith(String prefix) {  
        Node res=helper(prefix);  
        return res!=null;  
    }  
}
```

**Explanation**

Class Structure

1. **Node Class**:
    
    - Represents a single character in a word.
        
    - Contains:
        
        - `char val`: The character this node represents.
        - `Node[] next`: An array of 26 `Node` references, corresponding to each letter in the alphabet (`a` to `z`).
        - `boolean isWord`: Indicates whether this node marks the end of a valid word.
    - The constructor initializes a `Node` with a character value, an array for child nodes (each representing the next character in the alphabet), and a flag `isWord` set to `false`.
        
2. **Trie Class**:
    
    - Contains:
        - `Node root`: The root of the Trie, which is an empty node that does not represent any character (`'\0'`).

Methods

1. **Trie Constructor**:
    
    - Initializes the Trie with a root node that does not contain any character (denoted by `'\0'`).
2. **`insert(String word)`**:
    
    - Adds a word to the Trie.
    - Iterates over each character of the word.
    - For each character:
        - Checks if the corresponding child node exists in the current node's `next` array.
        - If it does not exist, a new `Node` is created for that character.
        - Moves to the next node in the chain.
    - After processing all characters, marks the last node as a complete word by setting `isWord` to `true`.
3. **`helper(String word)`**:
    
    - A helper method used to traverse the Trie according to the given word or prefix.
    - Starts at the root and moves down the Trie, following the nodes corresponding to each character in the string.
    - Returns the last node reached, or `null` if the string cannot be fully matched.
4. **`search(String word)`**:
    
    - Checks if a word exists in the Trie.
    - Calls `helper(word)` to traverse the Trie.
    - Returns `true` if the last node corresponds to the end of a word (`isWord` is `true`), otherwise returns `false`.
5. **`startsWith(String prefix)`**:
    
    - Checks if any word in the Trie starts with the given prefix.
    - Calls `helper(prefix)` to traverse the Trie.
    - Returns `true` if the prefix can be fully matched, otherwise returns `false`.