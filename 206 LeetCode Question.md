| Problem    | LeetCode Question 206. Reverse Linked List |
| ---------- | ------------------------------------------ |
| Time       | >80mins                                    |
| Difficulty | Easy                                       |
| Date       | 10/26/2021                                 |

**Question**

Given the `head` of a singly linked list, reverse the list, and return *the reversed list*.

1. **Listen**

I need to reverse this list. 

Singly linked list, meaning head node points to second node, second points to third, etc. And the linked list is only one direction.

Number of nodes range from [0 to 5000]

Value of the node itself is -5000 <= node.val <= 5000

2. **Example**

input: [1, 2, 3, 4, 5]

Output: [5, 4, 3, 2, 1]



Input: [1, 2]

Output:[2, 1]



Input head = []

output = []

3. **Brute Force**

Looking at this question, we know what the head is, we know what the tail is. We know next, we know values. We can put the nodes in a stack, then pop each one out in reverse. 

Time: O(n^2)

Space: O(n^2)

```
Stack stack = new Stack();
do{
	if(head = null){ end;}
	stack.push(head);
	
}while(node.next() != null);
```

Maybe use an array to rearrange. Does not work because the nodes are object. We dont need to make more space to implement this.



4. **Optimize**

Use Dynamics programming, or a recursive method, we can result in O(n) time. We can also use iterative method.

Making a recursive method, we first need a base case. 

```
if(head == null){
	return newHead;
}
ListNode next = head.next;
head.next = newHead;
return reverseListInt(next, head);
```



5. **Walk Through**

1. Using recursion to solve. 
2. Make a base case for when head == null, return it's new head.
3. We are then making a node called next, which is the second node. So, next = head.next. (At this moment, head is the current node, or the head node of the original linked list, and head.next is the second node of the original)
4. We set head.next to newHead, which is null, making it the tail. 
5. Then we recursively call the function, and set head to next, because we move onto the next node, and then set the second parameter, to head.
6. When the recursion reaches the end, it will return newHead, which is the tail, then previous node, then previous, then head.



**ESSENTIALLY**

1. Make new node, set this new node to next node
2. Make current node point to previous node, (if at start, point to null)
3. Make previous node to current node.
4. Make current node to next node. 



1. Using the iterative version.
2. Make a while loop. While head is not null
3. next = head.next
4. head.next = oldhead
5. oldhead = head.
6. head = next
7. return head.



6. **Implement**

   ```Java
   class Solution{
       public ListNode reverseList(ListNode head){
           return reverseListInt(head, null);	// First paramenter is head, second parameter is pointed to node
       }
       
       // Essentially, head is the current node, newHead will be the previous node
       private ListNode reverseListInt(ListNode head, ListNode newHead){
           if(head == null){
               return newHead;
           }
           ListNode next = head.next; 			// make the next as head.next to prepare for the next iteration.
           head.next = newHead;				// make head.next = newHead. Where newHead is current node.
           return reverseListInt(next, head);	// Perform the next iteration, first parameter is the head, and second paramenter 												is the pointed to node.
       } 
   }
   ```



```java
class Solution{
    public ListNode reverseList(ListNode head){
        ListNode next;
        ListNode oldHead = null;
        
        while(head!= null){
            next = head.next;
            head.next = oldHead;
            oldHead = head;
            head = next;
        }
        return oldHead;
    }
}
```



6. **Test**

Iterative

Runtime: 0 ms, faster than 100.00% of Java online submissions for Reverse Linked List.

Memory Usage: 39.1 MB, less than 43.05% of Java online submissions for Reverse Linked List.



**Solution**

Both the iterative and the recursive methods work. Both work in similar ways. Essentially making a next node and old node, changing the next, moving it over, but making sure its done in the right steps. 



**Ending Thoughts and What to Remember**

Two ways to solve this, Recursively or iteratively. Both get confusing, and are solved the same way. Keep track of whats next, whats current head, and head.next. 

Both methods essentially have a base case. It can be converted by just putting the base case in the while loop.

This just got confusing because you have to rearrange everything in the right order.

Essentially, you just make a new node, set that new node to the next, make the current node point to the previous node, set previous node (head.next) to current node, and set head to next node.

