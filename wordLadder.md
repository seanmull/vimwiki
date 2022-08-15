A transformation sequence from word beginWord to word endWord using a dictionary wordList is a sequence of words beginWord -> s1 -> s2 -> ... -> sk such that:

Every adjacent pair of words differs by a single letter.
Every si for 1 <= i <= k is in wordList. Note that beginWord does not need to be in wordList.
sk == endWord
Given two words, beginWord and endWord, and a dictionary wordList, return the number of words in the shortest transformation sequence from beginWord to endWord, or 0 if no such sequence exists.

Example 1:

Input: beginWord = "hit", endWord = "cog", wordList = ["hot","dot","dog","lot","log","cog"]
Output: 5
Explanation: One shortest transformation sequence is "hit" -> "hot" -> "dot" -> "dog" -> cog", which is 5 words long.

The first issue is the problem description is terrible.  Two comparisions need made:
1. Compare current beginWord with word from wordlist
2. It passed when two conditions are met
    1. It hasn't already been visited
    2. It is only one off from the current beginning word
       For instance hot -> hit is one off
                    hon -> hit is two off
                    ...
3 Once that conditions is met check if its the endWord
4.If not cycle through all the possible matches for the current beginning word
5.Once this queue of all possible matches are empty we no we have gone though all
the possible transformations for that level.
                     hit 1
                     hot 2
                  dot lot 3
                  dog log 4
                  cog     5

Underneath the hood this is a problem where a BFS method works since it fits the pattern
of transformations. We also need to track which words we have vistited.

Psedocode:
add top element to queue
while queue is not empty
  nextState = []
  for q in queue
    for word in wordList
      if word == endword
        return level
      if(!isVisited(word) && isOneOff(q, word))
          isVisited(word) == true
          nextState.push(word)
  queue = nextState
  level++
return 0
