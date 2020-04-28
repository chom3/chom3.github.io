---
layout: post
title:  "Generate Parentheses"
date:   2020-04-27
excerpt: "Generic backtracking algorithm that can be applied for many types of different \"combination or permutation problems.\""
algorithm: true
tag:
- backtracking
- algorithm
comments: true
---

# The Problem
note: from leetcode
Given n pairs of parentheses, write a function to generate all combinations of well-formed parentheses.

Given n = 3
~~~
Output:
[
  "((()))",
  "(()())",
  "(())()",
  "()(())",
  "()()()"
]
~~~

# Importance
The problem itself isn't that important to remember. The algorithm and understanding how to do the algorithm is more important. Backtracking can come up in diferent ways, usually you'll have to keep in mind that you start the function with some data structure to hold the different combinations. You'll then call a private function which will be used recursively to add a starting point and then branch off into different scenarios.

# Thought Process
The output example is most likely a list of strings so we can start there.

~~~
List<String> result = new ArrayList<String>();
// need to do something

return result;
~~~

Then like what was stated before, we'll need to call a function to get our recursion started.

In this case, we need to make sure we keep track of our "(" and ")". We can call these left "(" and right ")". If we initialize these values as integers, we can keep track of adding 1 to left or adding 1 to right. If left = n we stop adding left parenthesis, and if right = n we stop adding right ones.

As we recurse we'll pretty much be appending to our string, so we need to keep track of our string as we go on.

When will we know when to stop?

If we're given "n pairs" then when our length is 2 * n we'll know we're done.

We just need to know that the parentheses are well-formed, that each parentheses pair is closed properly.

I think that gives us enough info on what parameters we'll need for our recursive function.

~~~
parameters: 
need our List<String> result
int left
int right
string start
int n 

//base case - we have a well formed pair, add to our result and exit
if (2 * n == start.length()){
    result.add(start);
    return;
}

//our number of left parenthesis is less than n
//use recursion and add one to the left
if (left < n){
    backtrack(result, left + 1, right, n, start+"(");
}

//same for the right
if (right < n){
    backtrack(result, left, right+1, n, start+")");
}

How do we start the call? With all initial values of 0's and empty strings.
backtrack(result, 0, 0, n, "");
~~~

# Solution / Putting it all together
~~~
    public List<String> generateParenthesis(int n) {
        List<String> result = new ArrayList<String>();
                
        backtrack(result, 0,0, n, "");
        return result;
    }
    
    private void backtrack(List<String> result, int left, int right, int n, String start){
        if (start.length() == n*2){
            result.add(start);
            return;
        }
        if (left < n){
            backtrack(result, left+1, right, n, start+"(");
        }
        if (right < left){
            backtrack(result, left, right+1, n, start+")");
        }
    }
~~~