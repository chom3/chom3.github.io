---
layout: post
title:  "Finding First Unique Character in a String"
date:   2020-04-16
excerpt: "Use an array and understand the properties of a character to iterate and find the first unique character in a string."
algorithm: true
tag:
- strings
- algorithm
comments: true
---
# The problem:

Assuming a string in all lowercase.

Given a string, find the first non-repeating character in it and return the index (or character). If it doesn't exist, return -1.

~~~
given: abcdabc

Output: 3 or d

~~~

# Importance

I think the highlight here is to know your ASCII. With all lower case letters, 'a' to int is the value 97. 'z'  is 122. Subtracting any lowercase letter by 'a' will give 0-25 as a value. This can help you solve the problem with 0(1) constant space by using an array of size 26.


# The Thought Process
We need an array the size of all lower case letters (or adjusted if non-lowercase, we can set everything to lower case, etc.)

Iterate through the string and increment any letters in the array that are in the string.

iterate through the string again and any letter that returns the value 1 is our index/letter.

# The Solution
~~~
public int firstUniqChar(String s){
    int[] letters = new int[26];

    for (int i = 0; i < s.length(); i++){
        letters[s.charAt(i) - 'a']++;
    }

    for (int i = 0; i < s.length(); i++){
        if (letters[s.charAt(i) - 'a'] == 1){
            return i; // return letters[i];
        }
    }

    return -1;
}
~~~
