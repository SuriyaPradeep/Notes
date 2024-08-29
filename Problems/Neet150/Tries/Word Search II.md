#tries #2DArray 
### Question
Given an `m x n` `board` of characters and a list of strings `words`, return _all words on the board_.

Each word must be constructed from letters of sequentially adjacent cells, where **adjacent cells** are horizontally or vertically neighboring. The same letter cell may not be used more than once in a word.

**Example 1:**

![](https://assets.leetcode.com/uploads/2020/11/07/search1.jpg)

**Input:** board = [["o","a","a","n"],["e","t","a","e"],["i","h","k","r"],["i","f","l","v"]], words = ["oath","pea","eat","rain"]
**Output:** ["eat","oath"]

**Example 2:**

![](https://assets.leetcode.com/uploads/2020/11/07/search2.jpg)

**Input:** board = [["a","b"],["c","d"]], words = ["abcb"]
**Output:** []


### Solution
```java
class Solution{
	class Trie{  
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
	     public Trie(){  
	         root=new Node('\0');  
	     }  
	     public void insert(String word){  
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
	 }  
	 public List<String> findWords(char[][] board, String[] words) {  
	     Trie trie=new Trie();  
	     Trie.Node root=trie.root;  
	     List<String> res=new ArrayList<>();  
	     for(String word:words){  
	         trie.insert(word);  
	     }  
	     int n=board.length,m=board[0].length;  
	     for(int i=0;i<n;i++){  
	         for(int j=0;j<m;j++){  
	             dfs(board,res,root,"",i,j,n,m);  
	         }  
	     }  
	     return res;  
	 }  
	public void dfs(char[][] board,List<String> res,Trie.Node root,String path,int i,int j,int n,int m){  
	     if(i<0 || i>=n || j<0 || j>=m || board[i][j]=='#' || root.child[board[i][j]-'a']==null){  
	         return;  
	     }  
	     Trie.Node curr=root.child[board[i][j]-'a'];  
	    path+=board[i][j];  
	    char temp=board[i][j];  
	    board[i][j]='#';  
	     if(curr.isWord){  
	         res.add(path);  
	         curr.isWord=false;  
	     }  
	    dfs(board,res,curr,path,i+1,j,n,m);  
	    dfs(board,res,curr,path,i-1,j,n,m);  
	    dfs(board,res,curr,path,i,j+1,n,m);  
	    dfs(board,res,curr,path,i,j-1,n,m);  
	    board[i][j]=temp;  
	}
}
```

**Explanation**
1. **Trie Implementation:**

- **`Node` Class:**
    - Represents each node in the Trie.
    - `char val`: Holds the character represented by this node.
    - `Node[] child`: An array of child nodes, one for each letter ('a' to 'z').
    - `boolean isWord`: Marks whether this node represents the end of a valid word.
- **`Trie` Class:**
    - Manages the root node of the Trie.
    - `insert(String word)`: Inserts a word into the Trie by iterating over its characters and creating new nodes if necessary.

2. **`findWords` Method:**

- **Purpose:**
    - Finds all the words from the list `words` that can be formed by traversing the `board`.
- **Steps:**
    1. Initializes the Trie and inserts all words into it.
    2. Iterates over each cell in the board and calls the DFS function to explore possible words starting from that cell.

3. **`dfs` Method:**

- **Purpose:**
    - Recursively explores the board starting from a given cell to find all valid words.
- **Parameters:**
    - `board`: The 2D character board.
    - `res`: The list where found words are stored.
    - `root`: The current Trie node being explored.
    - `path`: The current string formed by the characters traversed so far.
    - `i, j`: The current cell's coordinates.
    - `n, m`: The dimensions of the board.
- **Process:**
    1. **Base Conditions:**
        - The DFS terminates if the current cell is out of bounds, has already been visited (`board[i][j] == '#'`), or if there is no corresponding child node in the Trie for the character at `board[i][j]`.
    2. **Recursive Exploration:**
        - The current character is appended to `path`.
        - The cell is temporarily marked as visited by setting `board[i][j]` to `'#'`.
        - If the current node marks the end of a valid word, that word is added to `res`.
        - The DFS then continues in all four possible directions: down, up, right, and left.
        - After exploring, the cell is reset to its original character to allow other paths to use it.

Explanation of Key Concepts

1. **Trie Structure:**
    
    - The Trie is used to efficiently check for the presence of a word or prefix in the list of words. Each path from the root to a node represents a prefix, and if a node's `isWord` is `true`, then the path from the root to that node forms a complete word in the dictionary.
2. **DFS Traversal:**
    
    - DFS is used to explore all possible paths starting from each cell on the board. The recursion allows the function to backtrack and explore other potential paths that can form valid words.
3. **Base Conditions in DFS:**
    
    - The DFS stops if the current path cannot lead to any valid word (due to out-of-bounds, revisiting, or lack of a matching child node). This prevents unnecessary computations and ensures that only valid paths are explored.

Key Points to Consider

- **Efficiency:**
    - The combination of Trie and DFS makes the solution efficient for large boards and word lists, as the Trie reduces the number of unnecessary paths explored during the DFS.
- **Avoiding Duplicates:**
    - Once a word is found, it is added to the result list, and the `isWord` flag is set to `false` to prevent the same word from being found multiple times from different starting points.

