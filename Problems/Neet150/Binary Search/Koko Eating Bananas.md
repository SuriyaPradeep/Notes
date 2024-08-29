#binary-search 
### Question
Koko loves to eat bananas. There are `n` piles of bananas, the `ith` pile has `piles[i]` bananas. The guards have gone and will come back in `h` hours.

Koko can decide her bananas-per-hour eating speed of `k`. Each hour, she chooses some pile of bananas and eats `k` bananas from that pile. If the pile has less than `k` bananas, she eats all of them instead and will not eat any more bananas during this hour.

Koko likes to eat slowly but still wants to finish eating all the bananas before the guards return.

Return _the minimum integer_ `k` _such that she can eat all the bananas within_ `h` _hours_.

**Example 1:**

**Input:** piles = [3,6,7,11], h = 8
**Output:** 4

**Example 2:**

**Input:** piles = [30,11,23,4,20], h = 5
**Output:** 30

**Example 3:**

**Input:** piles = [30,11,23,4,20], h = 6
**Output:** 23

### Solution
```java
class Solution{
	public int minEatingSpeed(int[] piles, int h) {  
	    int max=piles[0];  
	    for(int pile:piles){  
	        max=Math.max(pile,max);  
	    }  
	    int left=1,right=max;  
	    while(left<right){  
	        int mid=(left+right)/2;  
	        if(!canEat(piles,mid,h)){  
	            left=mid+1;  
	        }else{  
	            right=mid;  
	        }  
	    }  
	    return right;  
	}  
	public boolean canEat(int[] piles,int k,int h){  
	    int time=0;  
	    for(int pile:piles){  
	        time+=(pile/k);  
	        if(pile%k!=0){  
	            time++;  
	        }  
	        if(time>h){  
	            return false;  
	        }  
	    }  
	    return true;  
	}
}
```

**Explanation**
1. **Initialization**:
    
    - Find the maximum number of bananas in any pile (`max`). This represents the upper bound for `K` since, in the worst case, we would need to eat an entire pile within an hour.
    - Initialize two pointers: `left` set to 1 (the minimum possible speed) and `right` set to `max` (the maximum possible speed).
2. **Binary Search Loop**:
    
    - Continue the loop as long as `left` is less than `right`.
3. **Mid Calculation**:
    
    - Calculate the middle point `mid` by taking the average of `left` and `right`.
4. **Check Eating Feasibility**:
    
    - Use the helper method `canEat` to determine if it's possible to eat all the piles within `H` hours at the speed `mid`.
5. **Adjust Search Range**:
    
    - If it's not possible to eat all the bananas at speed `mid`, adjust the search range by setting `left` to `mid + 1`.
    - If it is possible, adjust the search range by setting `right` to `mid`.
6. **Return Result**:
    
    - When the loop ends, `right` will be the minimum eating speed `K` that allows all piles to be eaten within `H` hours.

**Helper Method: `canEat`**

1. **Initialization**:
    
    - Initialize `time` to 0. This will keep track of the total hours needed to eat all piles at speed `K`.
2. **Calculate Eating Time**:
    
    - Iterate over each pile in `piles`.
    - Calculate the hours required to eat the current pile at speed `K` and add it to `time`.
        - `time += pile / k` gives the full hours required.
        - If there are any leftover bananas (`pile % k != 0`), increment `time` by 1 to account for the additional hour needed.
    - If at any point `time` exceeds `H`, return `false` indicating that it's not possible to eat all bananas at speed `K`.
3. **Return Result**:
    
    - If the total `time` is less than or equal to `H`, return `true` indicating that it's possible to eat all bananas at speed `K`.