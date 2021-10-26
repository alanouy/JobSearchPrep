| Problem    | LeetCode Question 121 |
| ---------- | --------------------- |
| Time       | 46 minutes            |
| Difficulty | Easy                  |
| Date       | 10/26/2021            |

**Question**

You are given an array `prices` where `prices[i]` is the price of a given stock on the `ith` day.

You want to maximize your profit by choosing a **single day** to buy one stock and choosing a **different day in the future** to sell that stock.

Return *the maximum profit you can achieve from this transaction*. If you cannot achieve any profit, return `0`.

1. **Listen**

An array is given, buy one stock, sell one stock in the future. Cannot sell in the past, doesnt make sense. If all values in the array `prices` is in descending order, return 0 because you cannot return a profit. 

We want to find the **maximum** profit. So if there is a profit to be made earlier, but a better choice is found later on, then we need to use the later one.

2. **Example**

prices = [7, 1, 5, 3, 6, 4]

Output will be 5

Buy on day 2, sell on day 5.

buy for 1, sell for 6, return 5 profit.



prices = [7, 6, 4, 3, 1]

Output is 0

There is no optimal day to make money because all values are in descending order.

3. **Brute Force**

The obvious brute force method would be to take the first number, check with all the next numbers, find the best profit. Then move to the next number, find the highest profit, move to the next, etc etc.

Nested for loop.

```java
maxProfit = 0;
for(int i = 0; i < prices.length; i++){
    for(int j = i+1 = 1; j < prices.length; j++){
        if(prices[j] - prices[i] > maxProfit)
        	maxProfit = prices[j] - prices[i];
    }
}
return maxProfit; 
```

Time: O(n^2)

Space: O(1) i think (review space complexity)



4. **Optimize**

Every time you want to use or save something, I think of Hashmap. We can make the hashmap represent previous values. Does not need to be in a particular order, because we are just finding maximum profit from the past to present. We know that the hashmap has a lookup time of O(1), meaning we can store the values in the hashmap, look up if there is a value less than our current value. O(1) + O(1) + O(1)... = O(1). I think worst case would be O(n). 



Revelation

Because a hashmap needs to look up a certain key or value, we cannot use it for this question. A better data structure would be a stack, where we take the lowest value, put it in a stack, and subtract. O(n) time. O(n) space.

5. **Walk Through**

1. Create Stack
2. Create forloop
3. check first value, if stack empty, add to stack. 
4. If stack not empty, compare value with top of stack 
5. if less than top, add it to the stack.
6. If not less than top, subtract from the top of stack and save value. 
7. iterate through entire array.

6. **Implement**

   ```java
   class Solution{
       public int maxProfit(int[] prices){
           Stack stack = new Stack(); // push, pop, peek, remove.
           int maximumProfit = 0;
           
           for(int i = 0; i < prices.length; i++){
               if(stack.isEmpty() || prices[i] < (int)stack.peek()){
                   stack.push(prices[i]);
               }
               else {
                   if(prices[i] - (int)stack.peek() > maximumProfit){
                       maximumProfit = prices[i] - (int)stack.peek();
                   }
                   
               }
           }
           return maximumProfit;
       }
   }
   ```

   

7. **Test**

Everything worked out, other than initializing Stack stack = new Stack(); and remembering the data type of stack.peek(). Peek and pop return object, and we have to make sure it is int to do arithmetic on it. 

Runtime: 14 ms, faster than 5.17% of Java online submissions for Best Time to Buy and Sell Stock.

Memory Usage: 54.2 MB, less than 52.72% of Java online submissions for Best Time to Buy and Sell Stock.

**Solution**

Solution can be faster. Faster than only 5.17% of other submissions and 52.72% faster for memory. Meaning most people are faster.



**Ending Thoughts and What to Remember**

Revisit this problem. Improve on time and finding the pattern. Comparing prices uses a stack to keep track of the lowest value. Hashmap can only look up keys and values, so specific values. Stack can be used to keep track of lowest values. Remember the data types for pop and peek, which is object and not int. 

