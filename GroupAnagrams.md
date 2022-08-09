Given an array of strings strs, group the anagrams together. You can return the answer in any order.

An Anagram is a word or phrase formed by rearranging the letters of a different word or phrase, typically using all the original letters exactly once.

Example 1:

Input: strs = ["eat","tea","tan","ate","nat","bat"]
Output: [["bat"],["nat","tan"],["ate","eat","tea"]]

One way we can easily find if word is an anagram with another is to count
the letters for each word

A hash can be made by using an array and joining them
eat =>  [1, 0, 0, 0, 1, ....]
         a  b  c  d  e
         
We can then make a map of each hash and each word
If there is nothing we set the hash to <hash> : [element]
Otherwise we get the array append the element to it and set it

map = {
        "1#0#0#0#1..." : ["ate", "eat", "tea"]
      }
      
Then we can unpack it and return the values
