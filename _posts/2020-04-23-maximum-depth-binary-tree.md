---
layout: post
title:  "Find the max depth of a binary tree"
date:   2020-04-22
categories: [software engineer interview, binary tree]
tags: [recursion]
---

# The Problem
Given a binary tree, find the maximum depth.

~~~
/**
 * Definition for a binary tree node. (From Leetcode)
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */

        1
       / \
      2   3
     /\
    4  5
   /
  6

Max depth is 4 1->2->4->6
~~~

# Importance
You can use recursion here which is a good idea to keep in mind for future problems, like backtracking.

# The Thought Process
Set the base case. What if the root/input is null to start with? It'd be depth 0.
~~~
if (root == null){
    return 0;
}
~~~
We know we need to call the function within the function again.. but we also need to traverse left and right nodes.

So we'll need
~~~
root.left

root.right
~~~
But since we made it past the base case, we need to add 1 for the extra level. We don't know if the left or right is the one with the extra level but we just need to know if there is one or not. So we can take the max between the two.
~~~
Math.max(root.left, root.right) + 1
~~~
As it recurses back up we'll just keep adding 1 per level.

# Solution
~~~
    public int maxDepth(TreeNode root) {
        if (root == null){
            return 0;
        }
        
        return Math.max(maxDepth(root.left), maxDepth(root.right))+1;
    }
~~~
