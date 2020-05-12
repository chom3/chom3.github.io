---
layout: post
title:  "Letter Combinations of Phone Number"
date:   2020-05-11
excerpt: "More backtracking problems."
algorithm: true
tag:
- backtracking
- algorithm
comments: true
---

# The Problem:
Given a string containing digits from 2-9 inclusive, return all possible letter combinations that the number could represent.

# Importance
I've encountered this exact problem in a different interview so I'm certain that backtracking is a favorite for some interviewers. 

# Thought Process
It's easy to make a mistake but you'll generally have to know that you'll have a base function that starts the combinations and then a private function that will be recursive and build the strings for you. Stick to that and you should be able to work it out. Luckily when we're not actively in an interview we can take our time, look over solutions, and help internalize what the thought process is for these solutions. It's not about memorizing the problems but understanding the thought process!

First we'll need to make it easy to access these different letter combinations. A hash map would be easiest way, when you're given a number we should return the string that's associated with it.

~~~
        HashMap<String, String> map = new HashMap<String, String>();
        map.put("2","abc");
        map.put("3","def");
        map.put("4","ghi");
        map.put("5","jkl");
        map.put("6","mno");
        map.put("7","pqrs");
        map.put("8","tuv");
        map.put("9","wxyz");
~~~

We need to initialize an arraylist to return the combinations.

~~~
List<String> combinations = new ArrayList<String>();
~~~

We'll call our private function that will do all the work. We need to pass the arraylist to add to, the hash map, a starting string to build on, and the given string of digits.

~~~
findCombinations(combinations, map, "", digits);
~~~

Finally we return the combinations.

~~~
return combinations;
~~~

Altogether, we know what the solution will look like, we just need to fill in the rest.

~~~
    public List<String> letterCombinations(String digits) {
        HashMap<String, String> map = new HashMap<String, String>();
        map.put("2","abc");
        map.put("3","def");
        map.put("4","ghi");
        map.put("5","jkl");
        map.put("6","mno");
        map.put("7","pqrs");
        map.put("8","tuv");
        map.put("9","wxyz");
        List<String> combinations = new ArrayList<String>();
        if (digits.length() != 0){
            findCombinations(combinations, map, "", digits);    
        }        
        return combinations;
    }
~~~

Backtracking, I went wrong here and I thought it would be best to get the starting string, start a for loop, add to it, and do another loop... but we can make it much easier. We can get the first digit and retrieve the letters associated with that digit.

~~~
    String digit = digits.substring(0,1);
    String letters = map.get(digit);
~~~

Then we'll iterate through all the letters. My issue was that I was using charAt (java) when substring(i, i+1) will work just as well in our iteration. We can shave off the first character in the digits string but using substring as well. We pass on the current string with the letter appended, and the next digit. We'll create different combinations by passing on each letter represented by a digit this way (findCombinations("a"), findCombinations("b"), findCombinations("c")... etc) are basically being done here. 

~~~
    for (int j = 0; j < letters.length(); j++){
        String letter = map.get(digit).substring(j, j + 1);
        findCombinations(combinations, map, curr+letter, digits.substring(1));
    }
~~~

Our end point is when we have no more digits to find.

~~~
    if (digits.length() == 0){
        combinations.add(curr);
    }
~~~

# Solution / Putting it all together

~~~
class Solution {
    public List<String> letterCombinations(String digits) {
        HashMap<String, String> map = new HashMap<String, String>();
        map.put("2","abc");
        map.put("3","def");
        map.put("4","ghi");
        map.put("5","jkl");
        map.put("6","mno");
        map.put("7","pqrs");
        map.put("8","tuv");
        map.put("9","wxyz");
        List<String> combinations = new ArrayList<String>();
        if (digits.length() != 0){
            findCombinations(combinations, map, "", digits);    
        }        
        return combinations;
    }
    
    private void findCombinations(List<String> combinations, HashMap<String, String> map, String curr, String digits){
        if (digits.length() == 0){
            combinations.add(curr);
        }
        else {
            String digit = digits.substring(0,1);
            String letters = map.get(digit);


            for (int j = 0; j < letters.length(); j++){
                String letter = map.get(digit).substring(j, j + 1);
                findCombinations(combinations, map, curr+letter, digits.substring(1));
            }
        }
    }
}
~~~

Definitely easy to go wrong, but once you have the base down it's about filling in the rest and thinking it through! As a refresher, I definitely took a look at the solutions page. I'm writing down the solutions and thought process to help me for the next time I'm faced with these problems.