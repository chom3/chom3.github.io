---
layout: post
title:  "Find index of a substring in a string"
date:   2020-04-22
categories: [software engineer interview, strings]
tags: [substring]
---
# The Problem
Return the index of the first occurrence of a substring in a string.

If the length of the string is 0 return 0.

If there is no match return -1.
~~~
Given: abcdefde
Find "de"

Output: 3
~~~

# Importance
String manipulation questions are asked often in interview processes. I think these are necessary to be prepared especially if strings are a weakpoint. 

Another note is that I solved this my way, looks ike it's O(1) space and O(N) (iterates as long as the given string) time. It could be cleaned up and optimized more.

In a given interview, as long as you can explain your thought process as you write your code I believe it will be good enough.

# The Thought Process
An easy way would be to start iterating through the string and if you hit a possible match for the substring, start iterating through the substring.

Then we can start setting some flags.


Once we start iterating, we need to see if there's a possible start to an answer... We can set this by using a boolean flag.
~~~
Given: string s, string sub

//Start
int i = 0;
int j = 0;
int possibleAnswer = -1;
boolean firstOccurrence = true;

//iterate through the string
while( i < s.length()){
}

//how to figure out there's a possible start
if (s.charAt(i) == sub.charAt(j)){
    possibleAnswer = i; //possible index
}

We can use a flag here to set to false so we won't overwrite our possibleAnswer flag

if (firstOccurrence){
    possibleAnswer = i;
    firstOccurrence = false;
}

Iterate through both the string and substring:
i++;
j++;


What happens if we don't match:
We need to just move forward with i

i++;

But what if our j was already moving forward? We need to reset that. 

Also consider if we went past the answer while iterating through our i/j's - so we'll need to reset back to where we were as well. We saved our place with possibleAnswer! So we can increment 1 past that.

And we need to reset our flag.

if (j > 0){
    j = 0;
    i = possibleAnswer + 1;
    firstOccurrence = true;
}

In the end - if j is equal to the length of the substring then we made it to the end and can just return possibleAnswer.

If we did not, we return -1.
~~~

# Working Solution
~~~
class Solution {
    public int strStr(String s, String sub) {
        //Quick checks
        if (sub.length() == 0){
            return 0;
        }
        
        //Sub can't b e greater than the main string
        if (sub.length() > s.length()){
            return -1;
        }
        
        int i = 0;
        int j = 0;
        int possibleAnswer = -1;
        boolean firstOccurrence = true;
        while(i < s.length()){
            //Possible start
            if (s.charAt(i) == sub.charAt(j)){
                if (firstOccurrence){
                    possibleAnswer = i;
                    firstOccurrence = false;
                }
                i++;
                j++;
            } else {
                //Reset or keep going
                if (j > 0){
                    i = possibleAnswer + 1;
                    firstOccurrence = true;
                    j = 0;
                } else {
                    i++;
                }
            }
            //At the end
            if (j == sub.length()){
                return possibleAnswer;
            }
        }
        
        //No match
        return -1;
    }
}
~~~
