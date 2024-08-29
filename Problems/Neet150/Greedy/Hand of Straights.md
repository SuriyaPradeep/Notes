#array 
### Question
Alice has some number of cards and she wants to rearrange the cards into groups so that each group is of size `groupSize`, and consists of `groupSize` consecutive cards.

Given an integer array `hand` where `hand[i]` is the value written on the `ith` card and an integer `groupSize`, return `true` if she can rearrange the cards, or `false` otherwise.

**Example 1:**

**Input:** hand = [1,2,3,6,2,3,4,7,8], groupSize = 3
**Output:** true
**Explanation:** Alice's hand can be rearranged as [1,2,3],[2,3,4],[6,7,8]

**Example 2:**

**Input:** hand = [1,2,3,4,5], groupSize = 4
**Output:** false
**Explanation:** Alice's hand can not be rearranged into groups of 4.

### Solution
```java
class Solution{
	public boolean isNStraightHand(int[] hand, int groupSize) {  
	    int n=hand.length;  
	    if(n%groupSize!=0){  
	        return false;  
	    }  
	    Arrays.sort(hand);  
	    for(int i=0;i<n;i++){  
	        if(hand[i]>=0){  
	            if(!findSuccesor(hand,groupSize,i,n)){  
	                return false;  
	            }  
	        }  
	    }  
	    return true;  
	}  
	public boolean findSuccesor(int[] hand,int groupSize,int i,int n){  
	    int suc=hand[i]+1,count=0;  
	    hand[i]=-1;  
	    i+=1;  
	    count++;  
	    while(i<n && count<groupSize){  
	        if(hand[i]==suc){  
	            suc=hand[i]+1;  
	            hand[i]=-1;  
	            count++;  
	        }  
	        i++;  
	    }  
	    if(count!=groupSize){  
	        return false;  
	    }else{  
	        return true;  
	    }  
	}
}
```

**Explanation**
1. **Check if Grouping is Possible**:
    
    - The first step is to determine if it's even possible to divide the hand into groups of the desired size. If the total number of cards (`n`) is not divisible by the `groupSize`, it's immediately impossible to form the groups, so the method returns `false`.
2. **Sorting the Hand**:
    
    - The hand is sorted in ascending order. Sorting is important because it allows us to easily find consecutive sequences. Once the hand is sorted, the algorithm can attempt to form consecutive sequences starting from the smallest number.
3. **Iterating Through the Hand**:
    
    - The algorithm iterates through the sorted hand. For each card, if the card hasn't been used in a group yet (i.e., it is non-negative), the algorithm attempts to start a new group with that card as the smallest card in the group.
4. **Forming a Group**:
    
    - The algorithm tries to form a group of the required size by finding the next `groupSize - 1` consecutive cards in the sorted hand.
    - For each consecutive card needed, the algorithm searches through the rest of the hand. If a suitable card is found, it's marked as used.
    - If at any point, the algorithm can't find the next consecutive card to complete the group, it returns `false` because it's impossible to form a group with the current setup.
5. **Final Check**:
    
    - If the algorithm successfully forms all the required groups without encountering any issues, it returns `true`, indicating that it's possible to rearrange the hand into the required consecutive groups.