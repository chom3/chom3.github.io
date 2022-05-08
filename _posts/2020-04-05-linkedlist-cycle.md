---
title:  "Find a Cycle in a LinkedList"
date:   2020-04-05
categories: [software engineer interview, linkedlist]
tags: [linkedlist]
---
# The problem:
Given a linked list, determine if it has a cycle in it.

~~~
Given:

ListNode {
    int val;
    ListNode next;

    ListNode(int val){
        this.val = val;
    }
}

1->2->3
   ^--v
 
 Should be a cycle because after node with value 3, you'll go back to node with value 2.
~~~
# Importance
Opening your mind to the slow/fast (Tortoise and the Hare) method is a great approach to solving many different problems.

You might be asked to find a cycle in a tree, determine if it is a tree, etc.

# The Thought Process

The key is to use two pointers at the start of the list. One goes forward one node, the other two nodes.

If there is a cycle, both pointers will eventually be equal.

If not, then you will eventually hit the null end.
~~~
1 -> 2 -> 3
     ^----v
~~~
Both pointers start at 1.

Turtle -> 1 -> 2 -> 3

Hare -> 1 -> 3 -> 3


1 -> 2-> 3

Turtle -> 1 -> 2 -> 3 -> NULL

Hare -> 1 -> 3 -> NULL

Since our hare pointer is going to be going two at a time, it should check if it's currently null or it's next value will be null.

We have to remember to be careful of not letting the pointers going two at a time to be caught looking for the next value of an already null object! 

# The Solution
~~~
    public boolean hasCycle(ListNode head) {
        //Some basic check for the extreme cases. 
        //Everything is null? No cycle.
        //There is no next value after the starting node? No cycle.
        if (head == null || head.next == null){
            return false;
        }
        
        ListNode turtle = head;
        ListNode hare = head;
        
        while (hare != null && hare.next != null){
            turtle = turtle.next;
            hare = hare.next.next;
            if (turtle == hare){
                return true;
            }
        }
        
        return false;
    }
~~~