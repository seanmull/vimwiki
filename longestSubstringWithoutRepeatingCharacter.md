Given a string s, find the length of the longest substring without repeating characters.

Example 1:

Input: s = "abcabcbb"
Output: 3
Explanation: The answer is "abc", with the length of 3.

This is a sliding window problem where we increment the right as long as it isn't in the cache.
If it increments left and remove the value from the cache.  This is all done while tracking the
max length.

Pseudocode

Init max, l, r to 0
Init cache to a new Set
while r is less then the length of the string
  if cache has r
    update max
    add r to cache
    increment r
  else
    delete l from cache
    increment l
return max
