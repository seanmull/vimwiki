Given a string s and a dictionary of strings wordDict, return true if s can be segmented into a space-separated sequence of one or more dictionary words.

Note that the same word in the dictionary may be reused multiple times in the segmentation.

Example 1:

Input: s = "leetcode", wordDict = ["leet","code"]
Output: true
Explanation: Return true because "leetcode" can be segmented as "leet code".

This is a DP problem since involves solving subproblems.  

Here the optimal substructure. Build an array where we assume if we have an empty string in wordDict. This will be the seed value.  We would look through all letters in both s and wordDict.
But if the seed array is false we just skip it since word in the wordbank cannot be formed at that location.

 0 1 2 3 4 5 6 7 8
 T F F F F F F F F
   l e e t c o d e
   
we add leet

 0 1 2 3 4 5 6 7 8
 T F F F T F F F F
   l e e t c o d e
         ^
        end of word
   
we add code and once it get "t on leetcode ...   

 0 1 2 3 4 5 6 7 8
 T F F F T F F F T
   l e e t c o d e
                 ^
                 end of word
   
Psuedocode

init seed array with falses and +1 the size of s
set first value to true since we can have empty string
loop from 0 to s.length
  if seed at this loc is false skip since it s cannot be formed here
  create prefix of s starting a i 
  loop the wordDict
    if the prefix starts with the current word in dictionary and is true from the seed
    you can assign true to the end of word in the seed table
    seed[i + wordDict[j].length] = true //i is from s, j is from word in the dictionary
return the end of seed table
