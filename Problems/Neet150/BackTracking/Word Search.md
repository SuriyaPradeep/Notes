#2DArray #recursion 
### Question
Given an `m x n` grid of characters `board` and a string `word`, return `true` _if_ `word` _exists in the grid_.

The word can be constructed from letters of sequentially adjacent cells, where adjacent cells are horizontally or vertically neighboring. The same letter cell may not be used more than once.

**Example 1:**

![](https://assets.leetcode.com/uploads/2020/11/04/word2.jpg)

**Input:** board = [["A","B","C","E"],["S","F","C","S"],["A","D","E","E"]], word = "ABCCED"
**Output:** true

**Example 2:**

![](https://assets.leetcode.com/uploads/2020/11/04/word-1.jpg)

**Input:** board = [["A","B","C","E"],["S","F","C","S"],["A","D","E","E"]], word = "SEE"
**Output:** true

**Example 3:**

![](https://assets.leetcode.com/uploads/2020/10/15/word3.jpg)

**Input:** board = [["A","B","C","E"],["S","F","C","S"],["A","D","E","E"]], word = "ABCB"

### Solution
```java
class Solution{
	public boolean exist(char[][] board, String word) {  
	    int m=board.length,n=board[0].length;  
	    for(int i=0;i<m;i++){  
	        for(int j=0;j<n;j++){  
	            if(check(board,word,i,j,m,n,0)){  
	                return true;  
	            }  
	        }  
	    }  
	    return false;  
	}  
	public boolean check(char[][] board,String word,int i,int j,int m,int n,int curr){  
	    if(curr>=word.length()){  
	        return true;  
	    }  
	    if(i<0 || j<0 || i>=m || j>=n){  
	        return false;  
	    }  
	    boolean exist=false;  
	    if(board[i][j]==word.charAt(curr)){  
	        board[i][j]+=100;  
	        exist=check(board,word,i+1,j,m,n,curr+1) || check(board,word,i-1,j,m,n,curr+1) || check(board,word,i,j+1,m,n,curr+1) || check(board,word,i,j-1,m,n,curr+1);  
	        board[i][j]-=100;  
	    }  
	    return exist;  
	}
}
```

**Explanation**
1. **Main Function `exist`:**

- **Input:**
    - `board`: A 2D array of characters representing the grid.
    - `word`: The word to be searched in the grid.
- **Output:**
    - A boolean value indicating whether the word can be found in the grid.
- **Steps:**
    - The dimensions of the grid are stored in `m` and `n`.
    - The function iterates over each cell in the grid, starting at `(i, j)`, and calls the `check` function to see if the word can be found starting from that cell.
    - If any call to `check` returns `true`, the word exists in the grid, and the function immediately returns `true`.
    - If no valid path is found after checking all cells, the function returns `false`.

2. **Recursive Function `check`:**

- **Parameters:**
    - `board`: The grid.
    - `word`: The word to search for.
    - `i`, `j`: The current position in the grid.
    - `m`, `n`: The dimensions of the grid.
    - `curr`: The current index in the word being matched with the grid.
- **Base Case:**
    - `if(curr >= word.length())`: If `curr` (the current index in the word) reaches the length of the word, it means the entire word has been matched, so the function returns `true`.
    - `if(i < 0 || j < 0 || i >= m || j >= n)`: If the current position `(i, j)` is out of bounds, the function returns `false`.
- **Main Logic:**
    - The function first checks if the current cell `board[i][j]` matches the current character in the word (`word.charAt(curr)`).
    - If there's a match, the function temporarily modifies the board to mark the cell as visited by adding `100` to the character's ASCII value (`board[i][j] += 100`). This ensures the cell cannot be reused in the current search path.
    - The function then makes recursive calls to `check` for the four possible directions: down, up, right, and left.
    - If any of these recursive calls returns `true`, the word can be constructed from the grid, and the function returns `true`.
    - If none of the directions work, the function backtracks by restoring the original character in `board[i][j]` (`board[i][j] -= 100`) and returns `false`.