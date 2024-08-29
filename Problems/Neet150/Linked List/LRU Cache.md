#linked-list #hashmap 
### Question
Design a data structure that follows the constraints of a **[Least Recently Used (LRU) cache](https://en.wikipedia.org/wiki/Cache_replacement_policies#LRU)**.

Implement the `LRUCache` class:

- `LRUCache(int capacity)` Initialize the LRU cache with **positive** size `capacity`.
- `int get(int key)` Return the value of the `key` if the key exists, otherwise return `-1`.
- `void put(int key, int value)` Update the value of the `key` if the `key` exists. Otherwise, add the `key-value` pair to the cache. If the number of keys exceeds the `capacity` from this operation, **evict** the least recently used key.

The functions `get` and `put` must each run in `O(1)` average time complexity.

**Example 1:**

**Input**
["LRUCache", "put", "put", "get", "put", "get", "put", "get", "get", "get"]
[[2], [1, 1], [2, 2], [1], [3, 3], [2], [4, 4], [1], [3], [4]]
**Output**
[null, null, null, 1, null, -1, null, -1, 3, 4]

**Explanation**
LRUCache lRUCache = new LRUCache(2);
lRUCache.put(1, 1); // cache is {1=1}
lRUCache.put(2, 2); // cache is {1=1, 2=2}
lRUCache.get(1);    // return 1
lRUCache.put(3, 3); // LRU key was 2, evicts key 2, cache is {1=1, 3=3}
lRUCache.get(2);    // returns -1 (not found)
lRUCache.put(4, 4); // LRU key was 1, evicts key 1, cache is {4=4, 3=3}
lRUCache.get(1);    // return -1 (not found)
lRUCache.get(3);    // return 3
lRUCache.get(4);    // return 4

### Solution
```java
class LRUCache{
	private class Node{  
	    int key;  
	    int val;  
	    Node pre;  
	    Node post;  
	    public Node(int key,int val){  
	        this.key=key;  
	        this.val=val;  
	        this.pre=null;  
	        this.post=null;  
	    }  
	    public Node(){}  
	}  
	int capacity;  
	int size;  
	HashMap<Integer,Node>hashMap;  
	Node head;  
	Node tail;  
	public LRUCache(int capacity) {  
	    this.capacity=capacity;  
	    size=0;  
	    hashMap=new HashMap<>();  
	    head=new Node();  
	    tail=new Node();  
	    head.pre=tail.post=null;  
	    head.post=tail;  
	    tail.pre=null;  
	}  
	  
	public void addNode(Node node){  
	    node.pre=head;  
	    node.post=head.post;  
	    head.post.pre=node;  
	    head.post=node;  
	}  
	public void removeNode(Node node){  
	    Node pre=node.pre;  
	    Node post=node.post;  
	    pre.post=post;  
	    post.pre=pre;  
	}  
	public void moveToHead(Node node){  
	    removeNode(node);  
	    addNode(node);  
	}  
	public Node popTail(){  
	    Node node=tail.pre;  
	    removeNode(node);  
	    return node;  
	}  
	public int get(int key) {  
	    if(!hashMap.containsKey(key)){  
	        return -1;  
	    }  
	    Node node=hashMap.get(key);  
	    moveToHead(node);  
	    return node.val;  
	}  
	  
	public void put(int key, int value) {  
	    if(hashMap.containsKey(key)){  
	        Node node=hashMap.get(key);  
	        node.val=value;  
	        moveToHead(node);  
	    }else{  
	        Node node=new Node(key,value);  
	        hashMap.put(key,node);  
	        addNode(node);  
	        size++;  
	        if(size>capacity){  
	            node=popTail();  
	            size--;  
	            hashMap.remove(node.key);  
	        }  
	    }  
	}
}
```
**Explanation**
1. **Node Class**:
    
    - The `Node` class represents a doubly linked list node.
    - Each node stores a `key` and `val` (value).
    - It has two pointers: `pre` (previous node) and `post` (next node).
    - The constructor initializes these properties.
2. **LRUCache Class**:
    
    - The `LRUCache` class contains the core functionality of the cache.
    - It has attributes for `capacity`, `size`, `hashMap`, `head`, and `tail`.
3. **Constructor**:
    
    - Initializes the cache with a given capacity.
    - Sets `size` to 0.
    - Initializes `hashMap` to store the nodes for quick access using keys.
    - Creates `head` and `tail` dummy nodes to help manage the doubly linked list.
    - Sets `head.post` to `tail` and `tail.pre` to `head`, effectively linking them.
4. **addNode Method**:
    
    - Adds a new node right after the `head` node.
    - Sets the new node's `pre` to `head` and `post` to `head.post`.
    - Updates `head.post` to point to the new node and the new node's `post.pre` to point to the new node.
5. **removeNode Method**:
    
    - Removes a given node from the doubly linked list.
    - Sets the `pre` node's `post` to the given node's `post`.
    - Sets the `post` node's `pre` to the given node's `pre`.
6. **moveToHead Method**:
    
    - Moves a given node to the head of the doubly linked list.
    - Calls `removeNode` to detach the node from its current position.
    - Calls `addNode` to add the node right after the `head`.
7. **popTail Method**:
    
    - Removes the least recently used (LRU) node, which is just before the `tail`.
    - Calls `removeNode` to detach the LRU node from the list.
    - Returns the LRU node.
8. **get Method**:
    
    - Retrieves the value of a node by its key.
    - If the key does not exist in `hashMap`, returns `-1`.
    - If the key exists, gets the node from `hashMap`.
    - Moves the node to the head of the list (indicating it was recently accessed).
    - Returns the node's value.
9. **put Method**:
    
    - Adds a new node or updates an existing node with a given key and value.
    - If the key exists in `hashMap`, updates the node's value and moves it to the head.
    - If the key does not exist, creates a new node and adds it to `hashMap` and the head of the list.
    - Increases the `size`.
    - If `size` exceeds `capacity`, calls `popTail` to remove the LRU node and decreases `size`.
    - Removes the LRU node from `hashMap`.
