#array #2DArray #set 
### Question
Determine if a `9 x 9` Sudoku board is valid. Only the filled cells need to be validated **according to the following rules**:

1. Each row must contain the digits `1-9` without repetition.
2. Each column must contain the digits `1-9` without repetition.
3. Each of the nine `3 x 3` sub-boxes of the grid must contain the digits `1-9` without repetition.

**Note:**

- A Sudoku board (partially filled) could be valid but is not necessarily solvable.
- Only the filled cells need to be validated according to the mentioned rules.

**Example 1:**

![](https://upload.wikimedia.org/wikipedia/commons/thumb/f/ff/Sudoku-by-L2G-20050714.svg/250px-Sudoku-by-L2G-20050714.svg.png)

**Input:** board = 
[["5","3",".",".","7",".",".",".","."]
,["6",".",".","1","9","5",".",".","."]
,[".","9","8",".",".",".",".","6","."]
,["8",".",".",".","6",".",".",".","3"]
,["4",".",".","8",".","3",".",".","1"]
,["7",".",".",".","2",".",".",".","6"]
,[".","6",".",".",".",".","2","8","."]
,[".",".",".","4","1","9",".",".","5"]
,[".",".",".",".","8",".",".","7","9"]]
**Output:** true

**Example 2:**

**Input:** board = 
[["8","3",".",".","7",".",".",".","."]
,["6",".",".","1","9","5",".",".","."]
,[".","9","8",".",".",".",".","6","."]
,["8",".",".",".","6",".",".",".","3"]
,["4",".",".","8",".","3",".",".","1"]
,["7",".",".",".","2",".",".",".","6"]
,[".","6",".",".",".",".","2","8","."]
,[".",".",".","4","1","9",".",".","5"]
,[".",".",".",".","8",".",".","7","9"]]
**Output:** false
**Explanation:** Same as Example 1, except with the **5** in the top left corner being modified to **8**. Since there are two 8's in the top left 3x3 sub-box, it is invalid.


### Solution
```java
class Solution{
	public boolean isValidSudoku(char[][] board) {  
	    HashSet<String> set=new HashSet<>();  
	    for(int i=0;i<9;i++){  
	        for(int j=0;j<9;j++){  
	            char c=board[i][j];  
	            if(c!='.'){  
	                String row=c+" in row "+i;  
	                String col=c+" in col "+j;  
	                String block=c+" in block "+i/3+" "+j/3;  
	                if(!set.add(row) || !set.add(col) || !set.add(block)){  
	                    return false;  
	                }  
	            }  
	  
	        }  
	    }  
	    return true;  
	}
}
```

**Explanation**
1. **Initialization**:
    
    - You initialize a `HashSet` to store unique strings that represent the presence of each number in its respective row, column, and 3x3 block.
2. **Iteration**:
    
    - You iterate through each cell in the 9x9 Sudoku board using nested loops.
3. **Check and Add to Set**:
    
    - For each non-empty cell (`c != '.'`), you generate three strings:
        - One for the row: `"c in row i"`
        - One for the column: `"c in col j"`
        - One for the 3x3 block: `"c in block i/3 j/3"`
    - You attempt to add each of these strings to the `HashSet`.
    - If any of these strings already exist in the set (i.e., `set.add()` returns `false`), it means there is a duplicate number in the respective row, column, or block, and the board is invalid.
4. **Return Result**:
    
    - If no duplicates are found during the iteration, the board is valid, and the method returns `true`.