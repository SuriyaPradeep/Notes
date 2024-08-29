### Question
The **n-queens** puzzle is the problem of placing `n` queens on an `n x n` chessboard such that no two queens attack each other.

Given an integer `n`, return _all distinct solutions to the **n-queens puzzle**_. You may return the answer in **any order**.

Each solution contains a distinct board configuration of the n-queens' placement, where `'Q'` and `'.'` both indicate a queen and an empty space, respectively.

**Example 1:**

![](https://assets.leetcode.com/uploads/2020/11/13/queens.jpg)

**Input:** n = 4
**Output:** [[".Q..","...Q","Q...","..Q."],["..Q.","Q...","...Q",".Q.."]]
**Explanation:** There exist two distinct solutions to the 4-queens puzzle as shown above

**Example 2:**

**Input:** n = 1
**Output:** [["Q"]]

### Solution
```java
class Solution{
	public List<List<String>> solveNQueens(int n) {  
	    List<List<String>> ans=new ArrayList<>();  
	    if(n<=0){  
	        return ans;  
	    }  
	    List<String> curr=new ArrayList<>();  
	    HashSet<Integer> cols=new HashSet<>();  
	    HashSet<Integer> posDiagonal=new HashSet<>();  
	    HashSet<Integer> negDiagonal=new HashSet<>();  
	    helper(ans,curr,cols,posDiagonal,negDiagonal,n);  
	    return ans;  
	}  
	public void helper(List<List<String>> ans,List<String> curr,HashSet<Integer> cols,HashSet<Integer> posDiagonal,HashSet<Integer> negDiagonal,int n){  
	    if(curr.size()==n){  
	        ans.add(new ArrayList<>(curr));  
	        return;  
	    }  
	    int row=curr.size();  
	    for(int i=0;i<n;i++){  
	        if(cols.contains(i) || posDiagonal.contains(row+i) || negDiagonal.contains(row-i)){  
	            continue;  
	        }  
	        curr.add(addQueen(n,i));  
	        cols.add(i);  
	        posDiagonal.add(row+i);  
	        negDiagonal.add(row-i);  
	        helper(ans,curr,cols,posDiagonal,negDiagonal,n);  
	        curr.remove(curr.size()-1);  
	        cols.remove(i);  
	        posDiagonal.remove(row+i);  
	        negDiagonal.remove(row-i);  
	    }  
	}  
	public String addQueen(int n,int col){  
	    String str="";  
	    for(int i=0;i<n;i++){  
	        if(i==col){  
	            str+="Q";  
	        }else{  
	            str+=".";  
	        }  
	    }  
	    return str;  
	}
}
```

**Explanation**
Key Concepts:

1. **Queens and Threats**:
    
    - A queen can attack any other queen that is on the same row, column, or diagonal. Therefore, the challenge is to place `n` queens on an `n x n` board so that no two queens share the same row, column, or diagonal.
2. **Backtracking**:
    
    - The problem is solved using backtracking, a recursive algorithm that builds a solution incrementally and abandons solutions (backtracks) as soon as it determines that the solution cannot possibly be completed.

Components of the Code:

1. **Data Structures**:
    
    - **`List<List<String>> ans`**: Stores all the valid board configurations.
    - **`List<String> curr`**: Represents the current state of the board as a list of strings.
    - **`HashSet<Integer> cols`**: Tracks which columns have queens placed.
    - **`HashSet<Integer> posDiagonal`**: Tracks the positive diagonals (`row + col`).
    - **`HashSet<Integer> negDiagonal`**: Tracks the negative diagonals (`row - col`).
2. **`solveNQueens(int n)` Method**:
    
    - Initializes the required data structures and calls the helper method to start the backtracking process.
    - Returns a list of all valid board configurations.
3. **`helper` Method**:
    
    - **Base Case**: When the current list `curr` contains `n` strings, it means a valid configuration is found, so it is added to `ans`.
    - **Loop through Columns**: For each row, the algorithm tries placing a queen in each column.
    - **Checks for Conflicts**: Before placing a queen in a column, it checks if the column or diagonals are already occupied by another queen.
    - **Place Queen**: If no conflicts, it places the queen, updates the sets, and recurses to the next row.
    - **Backtracking**: After exploring a configuration, the queen is removed, and the sets are updated to backtrack.
4. **`addQueen(int n, int col)` Method**:
    
    - Creates a string representing a row on the board with a queen placed at the specified column (`col`).
    - The row is constructed with `.` (empty spaces) and a `Q` for the queen's position.

How It Works:

1. **Initialization**: The `solveNQueens` method starts with an empty board and calls the helper function to begin placing queens row by row.
    
2. **Recursive Exploration**:
    
    - At each row, the helper method tries to place a queen in each column.
    - If placing a queen in a column doesn't result in any conflict (based on the current state of the `cols`, `posDiagonal`, and `negDiagonal` sets), the method adds that placement and moves to the next row.
3. **Backtracking**:
    
    - If a placement leads to a dead end (no valid positions for the next queen), the method backtracks by removing the last placed queen and trying the next possible position.
4. **Completion**:
    
    - When all queens are successfully placed on the board (`curr.size() == n`), the configuration is saved.
    - The method eventually returns all possible solutions stored in `ans`.