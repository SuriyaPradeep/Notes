#2DArray #intervals 
### Question
Given an array of meeting time interval objects consisting of start and end times `[[start_1,end_1],[start_2,end_2],...] (start_i < end_i)`, determine if a person could add all meetings to their schedule without any conflicts.

**Example 1:**

```java
Input: intervals = [(0,30),(5,10),(15,20)]

Output: false
```

Copy

Explanation:

- `(0,30)` and `(5,10)` will conflict
- `(0,30)` and `(15,20)` will conflict

**Example 2:**

```java
Input: intervals = [(5,8),(9,15)]

Output: true
```

