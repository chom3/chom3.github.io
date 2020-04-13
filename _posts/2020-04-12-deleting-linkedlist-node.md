---
layout: post
title:  "Deleting a LinkedList Node"
date:   2020-04-12
excerpt: "Something that you can use to skip steps in more complicated problems, like designing a least recently used cache."
algorithm: true
tag:
- linkedlist
- algorithm
comments: true
---
# The problem:
Given a node, remove it from the linked list.

~~~

public class ListNode{
    int val;
    ListNode next;
    ListNode(int x){
        val = x;
    }
}

1->2->3

Given node with value 2

Output:

1 -> 3
~~~

# Importance
Knowing this off the top of my head was huge for designing a least recently used cache. I was able to do a delete this node and create a new node to place at the top fairly easily by having this in mind.

It's a relatively simple question with a simple solution, so having the instant solution for this in your back pocket will help you not waste time during any interview questions.

# The Thought Process
You can be a little hacky and not totally delete, but replace this node's value with the next value, and skip over the next node.

You've effectively written over your current node with the next node and changed the pointer to next to the node after.

# The Solution
~~~
public void deleteNode(ListNode node){
    node.val = node.next.val;
    node.next = node.next.next;
}
~~~