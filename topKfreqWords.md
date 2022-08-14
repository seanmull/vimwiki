Given an array of strings words and an integer k, return the k most frequent strings.

Return the answer sorted by the frequency from highest to lowest. Sort the words with the same frequency by their lexicographical order.

 Example 1:

 Input: words = ["i","love","leetcode","i","love","coding"], k = 2
 Output: ["i","love"]
 Explanation: "i" and "love" are the two most frequent words.
 Note that "i" comes before "love" due to a lower alphabetical order.
 
Example 2:

Input: words = ["the","day","is","sunny","the","the","the","sunny","is","is"], k = 4
Output: ["the","is","sunny","day"]
Explanation: "the", "is", "sunny" and "day" are the four most frequent words, with the number of occurrence being 4, 3, 2 and 1 respectively.

We want to sort by two criteria:
1. Frequency
2. alphabetical order

["love", "i", "love", "i"], k = 2
Since both i and love have the same frequency the order doesnt matter for the first step but then then we need to sort by 2 which does matter
["i", "love"]

Plan of attack:
1. Create a frequency counter => {"i": 2, "love": 2}
2. Convert that to an array => [["i", 2], ["love", 2]]
3. Create a comparator function that gives you logic for how to compare values
4. Sort by passing the comparator
5. Slice the array to whats needed
6. Map to strip out the frequency

Note: You could pass this comparator into a heap for better performance
but ..javascript doesn't have it.  And when run through python seems to run slower.

Hard part first:
function compare(a , b)
  return a - b
  
In a simple comparision between numbers this work but for words you need a different implementation.  Javascript has a.localecompare(b) with will work for strings.


init map
loop word of words
	if(map has word)
		add 1 to map[word]
  else
		map[word] = 1

return ArrayfromMap.sort(
		if(frequency are equal)
			sort by word
		otherwise sort by freq
).slice to k.map to word
