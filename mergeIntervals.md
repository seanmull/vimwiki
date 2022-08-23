Given an array of intervals where intervals[i] = [starti, endi], merge all overlapping intervals, and return an array of the non-overlapping intervals that cover all the intervals in the input.

Example 1:

Input: intervals = [[1,3],[2,6],[8,10],[15,18]]
Output: [[1,6],[8,10],[15,18]]
Explanation: Since intervals [1,3] and [2,6] overlap, merge them into [1,6].

1----3
 2----------6
              8---10
                      15------18
                      
1-----3                             add it but then it gets overwritten
1----------6                        overwriting from 1-3 then add
              8---10                add
                      15------18    add
                      
We want to sort intervals so we have in order start times.  We will compare two intervals a
left and a right.  When we merge the two intervals we replace the end with one of them with whichever is higher.  If we do not merge add it to the new list and move up right. 

Pseudocode
sort intervals by start time
init mergeIntervals by the first element of intervals
init j to 0 (this is the left interval)
  loop from i = 1 to end (this is the right interval)
    if(interval(i)(start) <= interval(j)(end))
      set interval(j)(end) to the max of the end of i or j interval
    else
      push interval(i) to the end of mergedIntervals
      increment j
return mergedIntervals
