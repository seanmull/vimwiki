Given a string paragraph and a string array of the banned words banned, return the most frequent word that is not banned. It is guaranteed there is at least one word that is not banned, and that the answer is unique.
The words in paragraph are case-insensitive and the answer should be returned in lowercase.

Example 1:

Input: paragraph = "Bob hit a ball, the hit BALL flew far after it was hit.", banned = ["hit"]
Output: "ball"
Explanation: 
"hit" occurs 3 times, but it is a banned word.
"ball" occurs twice (and no other word does), so it is the most frequent non-banned word in the paragraph. 
Note that words in the paragraph are not case sensitive,
that punctuation is ignored (even if adjacent to words, such as "ball,"), 
and that "hit" isn't the answer even though it occurs more because it is banned.

Steps to solve
1. Filter out symbols that are not part of the word
2. Lowercase all the words in the paragraph
3. Create a frequency counter hash
4. Iterate through the hash to get the highest frequency value

paragraph = paragraph.match.regExp(/\w+/)
paragraph = paragraph.toLowerCase

create frequencycounter = {"word": 1, "hello": 2}
max = 0
word = ""
loop word from frequency counter
  if max < hash[key]
    max = hash[key]
    word = key
return key
Alternatively this could be done with reduce
.reduce((a, b) => a[1] > b[1] ? a : b)[0]
