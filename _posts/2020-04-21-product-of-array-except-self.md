---
layout: post
title:  "Find the product of each array's indice except for that indice"
date:   2020-04-21
categories: [software engineer interview, lists]
tags: [array]
---

# The Problem
Given an array nums of n integers where n > 1, return an array output such that output[i] is equal to the product of all the elements of nums[i].
*Without using division.
~~~
Input: [1,2,3,4]

Output: [24,12,8,6]
~~~

# Importance
I don't think this is that important of an algorithm to know off the top of your head. It's more for problem solving and being able to use constant time and space.

Doing these questions often usually help think about optimal solutions, but I think this is a pretty unique situation.

# The Thought Process
In this case, we can't use division, so we can break it down into 2 parts.

Imagine having a new array:
~~~
New: [1,1,1,1]
Given: [1,2,3,4]
~~~
We need to multiply each new indice, essentially, by everything to the right and left of the same indice in the given array.
~~~
new[0] = given[1] * given[2] * given[3]
new[1] = given[0] * given[2] * given[3]
new[2] = given[0] * given[1] * given[3]
new[3] = given[0] * given[1] * given[2]
~~~
So how about we set up two for loops and two arrays?
~~~
RIGHT:
new[0] = given[1] * given[2] * given[3]
new[1] = given[2] * given[3]
new[2] = given[3]
new[3] = 1

LEFT:
new[0] = 1
new[1] = given[0]
new[2] = given[0] * given[1]
new[3] = given[0] * given[1] * given[2]
~~~
One can handle all the multiplication to the left and one can handle all the multiplication to the right.

A final array that handles the multiplication of each indice of left and right should be equal to our answer!

# The Solution
~~~
public int[] productExceptSelf(int[] nums){
    int[] left = new int[nums.length];
    int[] right = new int[nums.length];
    int[] answer = new int[nums.length];

    left[0] = 1; // no elements to the left of index 0, so this should be set to 1
    right[nums.length - 1] = 1; // same deal

    for (int i = 1; i < nums.length; i++){
        left[i] = left[i-1] * nums[i-1];
    }

    for (int i = nums.length - 2; i >= 0; --i){
        right[i] = right[i+1] * nums[i+1];
    }

    for (int i = 0; i < nums.length; i++){
        answer[i] = left[i] * right[i];
    }

    return answer;
}
~~~

# Improvements
While I think the solution should be perfectly valid, O(N) space and time complexity. You're using arrays that are as large as the given array is and the time it takes to complete is as long as the given array is. 

We can also imagine what if we are only given an answer array and are not able to generate new arrays to help with the right/left multiplication.

We can just iterate through our initial array going from the left (or right).

We'll have, in our new array, just the lefts.
~~~
LEFT:
new[0] = 1
new[1] = given[0]
new[2] = given[0] * given[1]
new[3] = given[0] * given[1] * given[2]
~~~
Now for the right:
We can initialize a variable equal to 1.

As we go to the next index, we can just multiply our variable by that current index and build upon it to have the same value.
~~~
RIGHT:
new[0] = given[1] * given[2] * given[3]
new[1] = given[2] * given[3]
new[2] = given[3]
new[3] = 1
~~~
this is the same as:
~~~
int r = 1;
for (int i = nums.length - 1; i >= 0; --i){
    r *= nums[i];
}
~~~
Then we can multiply each of the answer array's indices by the number r to get the full product.

~~~
public int[] productExceptSelf(int[] nums){
    int[] answer = new int[nums.length];

    answer[0] = 1; // no elements to the left of index 0, so this should be set to 1

    for (int i = 1; i < nums.length; i++){
        answer[i] = answer[i-1] * nums[i-1];
    }

    int r = 1;
    for (int i = nums.length - 1; i >= 0; --i){
        answer[i] = answer[i] * R;
        r *= nums[i];
    }

    return answer;
}
~~~