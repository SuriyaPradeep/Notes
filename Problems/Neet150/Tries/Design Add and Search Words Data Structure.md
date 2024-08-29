#tries 
### Question
Design a data structure that supports adding new words and finding if a string matches any previously added string.

Implement the `WordDictionary` class:

- `WordDictionary()` Initializes the object.
- `void addWord(word)` Adds `word` to the data structure, it can be matched later.
- `bool search(word)` Returns `true` if there is any string in the data structure that matches `word` or `false` otherwise. `word` may contain dots `'.'` where dots can be matched with any letter.

**Example:**

**Input**
["WordDictionary","addWord","addWord","addWord","search","search","search","search"]
[[],["bad"],["dad"],["mad"],["pad"],["bad"],[".ad"],["b.."]]
**Output**
[null,null,null,null,false,true,true,true]

**Explanation**
WordDictionary wordDictionary = new WordDictionary();
wordDictionary.addWord("bad");
wordDictionary.addWord("dad");
wordDictionary.addWord("mad");
wordDictionary.search("pad"); // return False
wordDictionary.search("bad"); // return True
wordDictionary.search(".ad"); // return True
wordDictionary.search("b.."); // return True

### Solution

```java
class WordDictionary {  
  
    class Node{  
        char val;  
        Node[] child;  
        boolean isWord;  
  
        public Node(char val){  
            this.val=val;  
            child=new Node[26];  
            isWord=false;  
        }  
    }  
  
    Node root;  
  
    public WordDictionary() {  
        root=new Node('\0');  
    }  
  
    public void addWord(String word) {  
        char[] chars=word.toCharArray();  
        Node curr=root;  
        for(char c:chars){  
            if(curr.child[c-'a']==null){  
                curr.child[c-'a']=new Node(c);  
            }  
            curr=curr.child[c-'a'];  
        }  
        curr.isWord=true;  
    }  
  
    public boolean helper(String word,Node root,int start){  
        for(int i=start;i<word.length();i++){  
            char c=word.charAt(i);  
            if(c=='.'){  
                for(Node child:root.child){  
                    if(child!=null && helper(word,child,i+1)){  
                        return true;  
                    }  
                }  
                return false;  
            }  
            if(root.child[c-'a']==null){  
                return false;  
            }  
            root=root.child[c-'a'];  
        }  
        return root.isWord;  
    }  
  
    public boolean search(String word) {  
        return helper(word,root,0);  
    }  
}
```

**Explanation**
1. **Trie Structure**:
    
    - The Trie is made up of nodes, where each node represents a single character of a word. Each node has an array of child nodes corresponding to the 26 letters of the English alphabet. There is also a flag to indicate whether the node represents the end of a valid word.
2. **Adding Words**:
    
    - To add a word to the Trie, the word is broken down into its individual characters. Starting from the root node, the Trie is traversed, and new nodes are created as needed for each character. Once all characters are added, the last node is marked to indicate that it represents the end of a word.
3. **Searching for Words**:
    
    - Searching for a word involves navigating through the Trie according to the characters in the word. If a character matches a child node, the search proceeds to the next character. If the wildcard character `'.'` is encountered, the search recursively explores all possible child nodes at that position. The search is successful if the traversal ends at a node marked as the end of a word.