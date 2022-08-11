You are given a string s. We want to partition the string into as many parts as possible so that each letter appears in at most one part.

Note that the partition is done so that after concatenating all the parts in order, the resultant string should be s.

Return a list of integers representing the size of these parts.

Example 1:

Input: s = "ababcbacadefegdehijhklij"
Output: [9,7,8]

Explanation:

The partition is "ababcbaca", "defegde", "hijhklij".
This is a partition so that each letter appears in at most one part.
A partition like "ababcbacadefegde", "hijhklij" is incorrect, because it splits s into less parts.

Look at a simple string

"abcba"
 01234

Clearly this cannot be partitioned since cutting if off at c
for instance would mean partioning the second b and a

Step one find the last index of each character:
map = {
  "a": 4,
  "b": 3,
  "c": 2
}

This can be done in linear time by updating the last index as you go.
We will keep update the end of the string by the highest index.  We would also
update the start of the string every time a partition is made

"abcba"
 01234
 ^       max = 4 so we know the last of the sequence is 4
  ^      max = 4
   ^      ....
    ^
     ^
     
"abcde"
 01234
 ^      max = 1 so we partition this
  ^     max = 1 so we partition this
  
  
Psedocode

// find the last index of each char
loop from 0 to length - 1 (i)
  set dict {a[i] : i}
  
// get the partitions
loop from 0 to length - 1 (end)
  // update the end of the string
  max = max(max, d[a[end]])
  // if we reach the end store the length and move the start position
  if(max === i)
    result.push(end + 1 - start)
    start = end + 1
  
