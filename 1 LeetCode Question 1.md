| Problem    | LeetCode Question 1. Two Sum |
| ---------- | ---------------------------- |
| Time       | 77 minutes                   |
| Difficulty | Easy                         |
| Date       | 10/22/2021                   |



Given an array of integers `nums` and an integer `target`, return *indices of the two numbers such that they add up to `target`*.

You may assume that each input would have ***exactly\* one solution**, and you may not use the *same* element twice.

You can return the answer in any order.

1. **Listen**

array of numbers

an integer target

we wanna find two numbers that add up to this target number.

only one solution, and cannot use the same element twice.

we dont want just the numbers, we want the indices of these numbers in the array.

2. **Example**

Array
2 4 9 3 8 10 32 28

Target
17

two numbers would be 9 and 8. (9 + 8 = 17)

Answer would be: (3, 4)



Array
10 4 23 32 59 2 12 2 5

Target 
22

Two numbers would be 10 and 12. (10+12= 22)

Answer would be: (0, 6)



3. **Brute Force**

two for loops, adding every number with the first index, seeing if anything adds up to the target, if not, move to second index, etc etc.
Essentially nested for loops.

Time: O(n^2)

Space: O(n)



4. **Optimize**

When I see a question like this, with an array and searching for another value, I like to think of hashmaps. 

something else to think about, the value we're getting, if the numbers in the array are larger than the target, we can ignore, small things like this can be implemented to skip steps. A way we can mitigate this is by sorting first. Fastest sorting algorithm would be merge sort, or quick sort (O(nlogn)).

If we implement a hashmap, we can get time down to O(n).

5. Walk Through

Array
3 5 2 9 7

Target
14

1. Look at the first index in the array
2. Get Target, subtract Index value, (14 - 3 = 11). Check if 11 is in hashmap, if not, store value (11) into hashmap. (index 0 -> 11).
3. Move onto next index. Check if 5 index value is in hashmap, if not, do step 2 again. (14 - 5 = 9). Store value 9 in hashmap. (index 1 -> 9)
4. move onto next index. Check if 2 is in hashmap. if not do step 2. (14 - 2 = 12). Store value 12 in hashmap. (index 2 -> 12)
5. Move onto next index. Check if 9 is in hashmap. We can see that it is, meaning that this index, (index 3) and index where it is found in the hashmap, (index 1), is the answer.
6. Therefore we get answer [1, 3].



6. Implement

```
class Solution {

	public int[] twoSum(int [] nums, int target) {

		HashMap<Integer, Integer> map = new HashMap<>();



		int hashsub;

		for(int i = 0; i < nums.length; i++){

			if(map.containsValue(num[i])){

				return (map.get(hashsub), i);

			}

		hashsub = target - num[i]; 

		map.put(hashsub, i);


		}

	return null;

	}

}
```





Hashmap what we need (storing target - value)

Key			Value

index 0	11

index 1	9

index 2	12

hashmap of what we have (storing value)

index 0	3

index 1	5

index 3	2



7. **Test**

What I was doing wrong and what I was stuck on.

I forgot to change the put, key, and values around. So when i was searching for Value, it wasnt giving me the value. It was mapping the KEY to 11, and value to 0.

Because **get returns the value**, and we cannot return the key, we want to **set the index to value**, and the **key as the actual number**. Unless theres a way to get value, we will have to use hashmaps of what we have.





Solution
      

    class Solution {
        public int[] twoSum(int[] nums, int target) {
            HashMap<Integer, Integer> map = new HashMap<>();    
        	for(int i = 0; i < nums.length; i++){
            	if(map.containsKey(target - nums[i])){
            	    return (new int[]{map.get(target - nums[i]), i});
            	}
           		else{
            		map.put(nums[i], i);
            	}
       		}
        return null;
    	}
    }




**Ending Thoughts and What to Remember**

Using hashmap to keep track of the value we need, and the index of where that value is. 

We have to map the number of the array to the KEY, and the index of the array to the VALUE, because the getter for hashmaps returns the VALUE, which would be the index, which is what we want.



Took too long finding what went wrong. Took too long realizing that get returns the value and that things were mixed up.