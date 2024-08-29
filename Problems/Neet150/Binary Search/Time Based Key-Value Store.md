#binary-search #hashmap 
### Question
Design a time-based key-value data structure that can store multiple values for the same key at different time stamps and retrieve the key's value at a certain timestamp.

Implement the `TimeMap` class:

- `TimeMap()` Initializes the object of the data structure.
- `void set(String key, String value, int timestamp)` Stores the key `key` with the value `value` at the given time `timestamp`.
- `String get(String key, int timestamp)` Returns a value such that `set` was called previously, with `timestamp_prev <= timestamp`. If there are multiple such values, it returns the value associated with the largest `timestamp_prev`. If there are no values, it returns `""`.

**Example 1:**

**Input**
["TimeMap", "set", "get", "get", "set", "get", "get"]
[[], ["foo", "bar", 1], ["foo", 1], ["foo", 3], ["foo", "bar2", 4], ["foo", 4], ["foo", 5]]
**Output**
[null, null, "bar", "bar", null, "bar2", "bar2"]

**Explanation**
TimeMap timeMap = new TimeMap();
timeMap.set("foo", "bar", 1);  // store the key "foo" and value "bar" along with timestamp = 1.
timeMap.get("foo", 1);         // return "bar"
timeMap.get("foo", 3);         // return "bar", since there is no value corresponding to foo at timestamp 3 and timestamp 2, then the only value is at timestamp 1 is "bar".
timeMap.set("foo", "bar2", 4); // store the key "foo" and value "bar2" along with timestamp = 4.
timeMap.get("foo", 4);         // return "bar2"
timeMap.get("foo", 5);         // return "bar2"

### Solution
```java
class TimeMap {  
    class Pair{  
        int timeStamp;  
        String val;  
        public Pair(int timeStamp,String val){  
            this.timeStamp=timeStamp;  
            this.val=val;  
        }  
        public int getTimeStamp() {  
            return timeStamp;  
        }  
        public String getVal() {  
            return val;  
        }  
    }  
    HashMap<String, ArrayList<Pair>> hashMap;  
    public TimeMap() {  
        hashMap=new HashMap<>();  
    }  
  
    public void set(String key, String value, int timestamp) {  
        if(!hashMap.containsKey(key)){  
            hashMap.put(key,new ArrayList<>());  
        }  
        hashMap.get(key).add(new Pair(timestamp,value));  
    }  
    public String get(String key, int timestamp) {  
        if(!hashMap.containsKey(key)){  
            return "";  
        }  
        Pair pair=binarySearch(hashMap.get(key),timestamp);  
        return pair==null?"":pair.getVal();  
    }  
    public Pair binarySearch(List<Pair> pairs,int timestamp){  
        if(pairs==null){  
            return null;  
        }  
        int left=0,right=pairs.size()-1;  
        Pair res=null;  
        while(left<=right){  
            int mid=(left+right)/2;  
            if(pairs.get(mid).getTimeStamp()==timestamp){  
                return pairs.get(mid);  
            }else if(pairs.get(mid).getTimeStamp()>timestamp){  
                right=mid-1;  
            }else{  
                left=mid+1;  
                res=pairs.get(mid);  
            }  
        }  
        return res;  
    }  
}
```

**Explanation**
**Class Structure and Purpose**

- **Class Name**: `TimeMap`
- **Purpose**: To allow setting values for a key with a timestamp and retrieving values based on the timestamp for a key.

**Inner Class: `Pair`**

- **Fields**:
    - `timeStamp`: An integer representing the timestamp.
    - `val`: A string representing the value associated with the timestamp.
- **Constructor**: Initializes the `timeStamp` and `val` fields.
- **Methods**:
    - `getTimeStamp()`: Returns the timestamp.
    - `getVal()`: Returns the value.

**Main Class: `TimeMap`**

- **Fields**:
    - `hashMap`: A HashMap where each key maps to a list of `Pair` objects, representing timestamp-value pairs.

**Methods**

**Constructor: `TimeMap()`**

- Initializes the `hashMap`.

 `set(String key, String value, int timestamp)`

- **Purpose**: To set the value for a key with a specific timestamp.
- **Logic**:
    - If the key does not exist in `hashMap`, add the key with a new ArrayList of `Pair` objects.
    - Add the new `Pair` (timestamp, value) to the list associated with the key.

`get(String key, int timestamp)`

- **Purpose**: To get the value for a key that has the closest timestamp less than or equal to the given timestamp.
- **Logic**:
    - If the key does not exist in `hashMap`, return an empty string.
    - Perform a binary search on the list of `Pair` objects to find the closest timestamp less than or equal to the given timestamp using the `binarySearch` method.
    - Return the value of the found `Pair`. If no such `Pair` exists, return an empty string.

`binarySearch(List<Pair> pairs, int timestamp)`

- **Purpose**: To perform a binary search on the list of `Pair` objects to find the closest timestamp less than or equal to the given timestamp.
- **Logic**:
    - Initialize `left` and `right` pointers for the binary search.
    - Initialize `res` to null to keep track of the result.
    - While `left` is less than or equal to `right`:
        - Calculate the `mid` index.
        - If the timestamp at `mid` is equal to the given timestamp, return the `Pair` at `mid`.
        - If the timestamp at `mid` is greater than the given timestamp, adjust the `right` pointer to `mid - 1`.
        - If the timestamp at `mid` is less than the given timestamp, adjust the `left` pointer to `mid + 1` and update `res` to the `Pair` at `mid`.
    - Return `res`, which will be the `Pair` with the closest timestamp less than or equal to the given timestamp, or null if no such `Pair` exists.