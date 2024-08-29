#array #priority-queue #topK 
### Question
Design a class to find the `kth` largest element in a stream. Note that it is the `kth` largest element in the sorted order, not the `kth` distinct element.

Implement `KthLargest` class:

- `KthLargest(int k, int[] nums)` Initializes the object with the integer `k` and the stream of integers `nums`.
- `int add(int val)` Appends the integer `val` to the stream and returns the element representing the `kth` largest element in the stream.

**Example 1:**

**Input**
["KthLargest", "add", "add", "add", "add", "add"]
[[3, [4, 5, 8, 2]], [3], [5], [10], [9], [4]]
**Output**
[null, 4, 5, 5, 8, 8]

**Explanation**
KthLargest kthLargest = new KthLargest(3, [4, 5, 8, 2]);
kthLargest.add(3);   // return 4
kthLargest.add(5);   // return 5
kthLargest.add(10);  // return 5
kthLargest.add(9);   // return 8
kthLargest.add(4);   // return 8

### Solution
```java
class KthLargest{  
    int k;  
    Queue<Integer> pq;  
    public KthLargest(int k,int[] nums){  
        this.k=k;  
        pq=new PriorityQueue<>((a,b)->(a-b));  
        for(int num:nums){  
            add(num);  
        }  
    }  
    public int add(int val){  
        if(pq.size()<k){  
            pq.add(val);  
        }else if(pq.peek()<val){  
            pq.poll();  
            pq.add(val);  
        }  
        return pq.peek();  
    }  
}
```

**Explanation**
1. **Min-Heap (Priority Queue)**
    
    - The core of the implementation is a min-heap, which is a data structure where the smallest element is always at the top. In this case, the min-heap is implemented using a `PriorityQueue`.
    - By using a min-heap with a fixed size of `k`, the smallest element in the heap will always be the k-th largest element in the current stream of numbers.
2. **Initialization**
    
    - When an instance of `KthLargest` is created, it initializes the min-heap with the initial set of numbers. If there are fewer than `k` numbers initially, it simply adds all of them to the heap. If there are more than `k` numbers, it only keeps the `k` largest numbers in the heap.
3. **Adding New Elements**
    
    - Each time a new number is added, the class checks if the heap has fewer than `k` elements. If so, it adds the new number directly.
    - If the heap is already full (contains `k` elements), the class compares the new number to the smallest element in the heap. If the new number is larger than the smallest element, the smallest element is removed, and the new number is added. This ensures that the heap always contains the k largest elements.
4. **Tracking the k-th Largest Element**
    
    - After adding a new number, the smallest element in the heap (which is at the root of the min-heap) is the k-th largest element in the current set of numbers. This value is returned as the result.