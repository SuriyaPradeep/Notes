#slidingWindow
### Question
You are given an array `prices` where `prices[i]` is the price of a given stock on the `ith` day.

You want to maximize your profit by choosing a **single day** to buy one stock and choosing a **different day in the future** to sell that stock.

Return _the maximum profit you can achieve from this transaction_. If you cannot achieve any profit, return `0`.

**Example 1:**

**Input:** prices = [7,1,5,3,6,4]
**Output:** 5
**Explanation:** Buy on day 2 (price = 1) and sell on day 5 (price = 6), profit = 6-1 = 5.
Note that buying on day 2 and selling on day 1 is not allowed because you must buy before you sell.

**Example 2:**

**Input:** prices = [7,6,4,3,1]
**Output:** 0
**Explanation:** In this case, no transactions are done and the max profit = 0.

### Solution
```java
class Solution{
	public int maxProfit(int[] prices) {  
	    int min=prices[0];  
	    int maxProfit=0;  
	    for(int i=1;i<prices.length;i++){  
	        if(min>prices[i]){  
	            min=prices[i];  
	        }else{  
	            maxProfit=Math.max(maxProfit,(prices[i]-min));  
	        }  
	    }  
	    return maxProfit;  
	}
}
```

**Explanation**
1. **Initialize Variables**:
    
    - `min` is initialized to the first element of the `prices` array. This variable keeps track of the minimum price seen so far.
    - `maxProfit` is initialized to 0. This variable stores the maximum profit that can be achieved.
2. **Iterate Through Prices**:
    
    - The loop starts from the second day (`i = 1`) and goes through each price in the `prices` array.
3. **Update Minimum Price**:
    
    - If the current price (`prices[i]`) is less than the current `min`, update `min` to the current price. This ensures `min` always contains the lowest price seen so far.
4. **Calculate and Update Maximum Profit**:
    
    - If the current price (`prices[i]`) is greater than `min`, calculate the potential profit by subtracting `min` from the current price.
    - Update `maxProfit` with the maximum value between the current `maxProfit` and the potential profit. This ensures `maxProfit` always contains the highest profit seen so far.
5. **Return Maximum Profit**:
    
    - After the loop finishes, return the value of `maxProfit`.

