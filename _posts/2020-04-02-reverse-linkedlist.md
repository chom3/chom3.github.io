---
layout: post
title:  "Reverse a LinkedList"
date:   2020-04-05
excerpt: "Understanding how to reverse a singly linkedlist."
algorithm: true
tag:
- linkedlist
- algorithm
comments: true
---
# The problem:

Given a singly linked list, reverse it.

~~~
Given:

ListNode {
    int val;
    ListNode next;

    ListNode(int val){
        this.val = val;
    }
}

Sample LinkedList: 

1->2->3->4->5->NULL


Sample Output:

5->4->3->2->1->NULL
~~~

# Importance

I don't believe I've been asked to outright reverse a linkedlist during an interview process, but I've encountered questions where knowing the answer to this should relieve time if you knew how to do it off the top of your head. Questions can build on this by asking "reverse a sublist". Knowing the algorithm for this gives you some foundation for the solution.

# The Thought Process

The key is to use temporary nodes to hold the values!

We know we need to make our first node's next value point to NULL.

We need to be able still iterate forward.

~~~
Iterate would mean that we need to start a loop, from the start of the linkedlist until the end.

How to iterate:

while (start != null){
    start = start.next;
}


The algorithm:

//Starting point
start.val = 1

//Starting point
previous node = NULL

//Set our next to point backwards (NULL)
start.next = previous node

//Set our backwards point to move up to our current point (ListNode 1)
previous node = start

//Move our starting point forward because our dummy node held that value
start = dummy node (the value is 2)

What this has done is effectively changed the list to

1 -> NULL

As we've broken the link between 2->3->4->5, as we continue through each node reversing, we'll see

2 -> 1 -> NULL

and so on.

...

By the time we get ot the end, start will be null because we iterated all the way to the end.

Our previous ListNode which has been holding the values for us will be our starting point so we'll need to return that instead.
~~~


### The Solution (Java)

~~~
    public ListNode reverseList(ListNode head){
        ListNode start = head;
        ListNode previous = null;

        while (start != null){
            ListNode dummy = start.next;
            start.next = previous;
            previous = start;
            start = dummy;
        }

        return previous;
    }
~~~