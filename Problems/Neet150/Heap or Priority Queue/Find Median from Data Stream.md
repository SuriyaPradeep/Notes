#priority-queue 
### Question
The **median** is the middle value in an ordered integer list. If the size of the list is even, there is no middle value, and the median is the mean of the two middle values.

- For example, for `arr = [2,3,4]`, the median is `3`.
- For example, for `arr = [2,3]`, the median is `(2 + 3) / 2 = 2.5`.

Implement the MedianFinder class:

- `MedianFinder()` initializes the `MedianFinder` object.
- `void addNum(int num)` adds the integer `num` from the data stream to the data structure.
- `double findMedian()` returns the median of all elements so far. Answers within `10-5` of the actual answer will be accepted.

**Example 1:**

**Input**
["MedianFinder", "addNum", "addNum", "findMedian", "addNum", "findMedian"]
[[], [1], [2], [], [3], []]
**Output**
[null, null, null, 1.5, null, 2.0]

**Explanation**
MedianFinder medianFinder = new MedianFinder();
medianFinder.addNum(1);    // arr = [1]
medianFinder.addNum(2);    // arr = [1, 2]
medianFinder.findMedian(); // return 1.5 (i.e., (1 + 2) / 2)
medianFinder.addNum(3);    // arr[1, 2, 3]
medianFinder.findMedian(); // return 2.0

### Solution
```java
class MedianFinder {  
  
    PriorityQueue<Integer> smallHeap;  
    PriorityQueue<Integer> largeHeap;  
    boolean even;  
  
    public MedianFinder() {  
        smallHeap=new PriorityQueue<>((a,b)->Integer.compare(a,b));  
        largeHeap=new PriorityQueue<>((a,b)->Integer.compare(b,a));  
        even=true;  
    }  
  
    public void addNum(int num) {  
        if(even){  
            smallHeap.add(num);  
            largeHeap.add(smallHeap.poll());  
        }else{  
            largeHeap.add(num);  
            smallHeap.add(largeHeap.poll());  
        }  
        even=!even;  
    }  
  
    public double findMedian() {  
        if(even){  
            return (double)(smallHeap.peek()+largeHeap.peek())/2.0;  
        }else{  
            return (double)largeHeap.peek();  
        }  
    }  
}
```

**Explanation**
Fields:

- **`smallHeap`**: A min-heap that stores the larger half of the numbers. It keeps the smallest element at the top.
- **`largeHeap`**: A max-heap that stores the smaller half of the numbers. It keeps the largest element at the top.
- **`even`**: A boolean flag to track whether the current total number of elements is even or odd.

Constructor:

- **`MedianFinder()`**: Initializes the two heaps and sets `even` to `true` because the initial count of numbers is zero, which is even.

Methods:

1. **`addNum(int num)`**:
    
    - This method adds a new number to the data structure.
    - If the current number of elements is even:
        - The new number is added to `smallHeap` (min-heap), but immediately the smallest element from `smallHeap` is removed and added to `largeHeap` (max-heap). This ensures the balance between the two heaps.
    - If the current number of elements is odd:
        - The new number is added to `largeHeap` (max-heap), but immediately the largest element from `largeHeap` is removed and added to `smallHeap` (min-heap).
    - Finally, the `even` flag is toggled to reflect the new total count of numbers.
2. **`findMedian()`**:
    
    - This method returns the median of the current stream of numbers.
    - If the number of elements is even:
        - The median is the average of the two middle elements, which are the tops of `smallHeap` and `largeHeap`.
    - If the number of elements is odd:
        - The median is the top of `largeHeap`, which has one more element than `smallHeap`.