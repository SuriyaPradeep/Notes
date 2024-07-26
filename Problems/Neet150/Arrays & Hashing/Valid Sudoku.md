#set 
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
	    int rows=board.length,cols=board[0].length;  
	    for(int i=0;i<rows;i++){  
	        for(int j=0;j<cols;j++){  
	            char c=board[i][j];  
	            if(c!='.'){  
	                String row=c+" in row "+i;  
	                String col=c+" in cols "+j;  
	                String box=c+" in box "+i/3+" "+j/3;  
	                if(!set.add(row) || !set.add(col) || !set.add(box)){  
	                    return false;  
	                }  
	            }  
	        }  
	    }  
	    return true;  
	}
}
```

### Explanation
1. **Initialize HashSet**:
    
    - Create a `HashSet<String>` called `set` to store unique strings representing the presence of digits in rows, columns, and sub-boxes.
2. **Iterate Over the Board**:
    
    - Use nested loops to iterate through each cell in the `board`. The outer loop iterates over rows, and the inner loop iterates over columns.
3. **Check Each Cell**:
    
    - For each cell, check if the cell contains a digit (`c != '.'`).
4. **Create Unique Identifiers**:
    
    - Create three unique strings for the current digit:
        - `row`: A string representing the digit in the current row.
        - `col`: A string representing the digit in the current column.
        - `box`: A string representing the digit in the current 3x3 sub-box.
5. **Check for Duplicates**:
    
    - Try to add each of these strings to the `set`. If any of the `add` operations return `false`, it means the digit is already present in the respective row, column, or sub-box, and the board is not valid. Return `false` immediately.
6. **Return True if No Duplicates Found**:
    
    - If the loops complete without finding any duplicates, return `true`.

