| Problem    | LeetCode Question 70 |
| ---------- | -------------------- |
| Time       | 60                   |
| Difficulty | Easy                 |
| Date       | 10/27/2021           |

**Question**

Climbing Stairs

You are climbing a staircase. It takes `n` steps to reach the top.

Each time you can either climb `1` or `2` steps. In how many distinct ways can you climb to the top?

1. **Listen**

You have two options to get to the top. Climb one stair, or two. 

1 <= n <= 45

we want to find how many distinct ways to get to the top.

2. **Example**

climbing 1 stair.

1

Takes 1 distinct way to climb. 1 step.



Climbing 2 stairs

1, 1

2

Takes 2 distinct ways to climb. 1, 1 or 2.



Climbing 3 stairs.

1, 1, 1
1, 2
2, 1
Takes 3 distinct ways to climb 3 stairs.

1 + 2 = 3

Climbing 4 stairs.

1, 1, 1, 1
1, 1, 2
1, 2, 1
2, 1, 1
2, 2

There are 5 distinct ways to climb 4 stairs.

2 + 3 = 5



Climbing 5 stairs

1, 1, 1, 1, 1
1, 1, 1, 2
1, 1, 2, 1
1, 2, 1, 1
1, 2, 2
2, 1, 1, 1
2, 1, 2
2, 2, 1

There are 8 distinct ways to climb 5 stairs.

3+5 = 8



Climbing 6 stairs

1, 1, 1, 1, 1, 1
1, 1, 1, 1, 2
1, 1, 1, 2, 1
1, 1, 2, 1, 1
1, 1, 2, 2
1, 2, 1, 1, 1
1, 2, 2, 1
1, 2, 1, 2
2, 1, 1, 1, 1
2, 1, 1, 2
2, 1, 2, 1
2, 2, 1, 1
2, 2, 2

There are 13 distinct ways to climb 6 stairs.

5+8 = 13

I was trying to find a pattern between the number of stairs, and the like.. sequences of the ways to climb stairs. But because I saw the category of what this question is in, aka dynamic programming, I realized that it is a fib sequence.



3. **Brute Force**

How do you brute force something that is dynamic. Maybe theres a way to program the sequences and count them like how i was doing above. This seems like a problem that would take way too long to code, and I wont waste too much time on this section.

4. **Optimize**

Theres two ways I can go about this question. First is the most obvious way, which is the recursive implementation. This is probably the most common way and the usual way fib sequences is coded. Another way could be through iteratively going through with a while loop. 

From what I can recall, questions like these require a lot of calculations for each fib sequence, and the further you go, the more calculations will be made. These calculations are usually the same calculations over and over again, which can be minimized by storing these values in something like a HashMap for fast lookup times. Lookup for a HashMap is O(1). We will be storing the values so it will increase the space complexity, but not by much. The trade-off for an increase in time complexity outweighs the space.

5. **Walk Through**



Lets say we have n = 6

find n-1 and n-2 (n = 5, n = 4)

to find n = 5, we need n-1 and n-2 (n = 4, n = 3)

to find n = 4, we need n = 3 and n = 2

to find n = 3, we need n = 2, and n = 1

n = 2 is 2, and n = 1 is 1.

return 2 and 1 to n = 3, which will return 3.

n = 3 will return 3 to n = 4, and n=2 will return 2, this n = 4 will return 5 to the n = 5.

n = 5 will get 5 and 3, to equal 8. return 8

n = 6 will get 8 and 5, to output 13.



We need a base case

if n = 2, return 2.

if n = 1, return 1.



6. **Implement**

   Recursive without storing values in HashMap.

   ```Java
   public int climbStairs(int n){
       if(n == 2){
           return 2;
       }
       if(n == 1){
           return 1;
       }
       
       return climbStairs(n-1) + climbStairs(n-2);
   }
   ```

   

   Recursive Method with HashMap.

   ```Java
   public int climbStairs(int n){
       HashMap<Integer, Integer> map = new HashMap<>();
       
       map.put(1, 1);
       map.put(2, 2);
       return climbStairs(n, map);
   }
   
   public int climbStairs(int n, HashMap<Integer, Integer> map){
       if(map.containsKey(n)){
           return map.get(n);
       }
       
       map.put(n, climbStairs(n-1, map) + climbStairs(n-2, map));
       return map.get(n);
   }
   ```

   Runtime: 0 ms, faster than 100.00% of Java online submissions for Climbing Stairs.

   Memory Usage: 36.2 MB, less than 51.90% of Java online submissions for Climbing Stairs.

   This should result in a O(n) time, and O(n) space. 

   

   Implementation without Recursion.
   Bottom Up Approach

   This implementation, we do the calculations from the bottom to the top. For this, we calculate each one, same as the recursive way, but instead, we dont need to save any of the values because we just want the last two values. We work from the bottom, replacing temp1 with temp2, then temp2 with newVal. 

   ```java
   public int climbStairs(int n){
       if(n < 3){
           return n;
       }
       
       int temp1 = 1;
       int temp2 = 2;
       
       for(int i = 3; i <= n; i++){
           int newVal = temp1+temp2;
           temp1 = temp2;
           temp2 = newVal; 
       }
       return temp2;
       
   }
   ```

   I believe this is O(n) time, and O(1) space.

   Runtime: 0 ms, faster than 100.00% of Java online submissions for Climbing Stairs.

   Memory Usage: 35.6 MB, less than 80.58% of Java online submissions for Climbing Stairs.



**Ending Thoughts and What to Remember**

Very interesting problem with different types of solutions I would not have thought about. The obvious recursive fib method was correct but took too long. Using a HashMap to store the values was a good way of doing things. The bottom up approach without recursion was also the same runtime and used less memory. 

Remember to include edge cases, like n < 3.

Realize that it is a fib sequence sooner. Wasted about 15 minutes trying to figure it out.



