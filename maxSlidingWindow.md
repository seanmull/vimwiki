You are given an array of integers nums, there is a sliding window of size k which is moving from the very left of the array to the very right. You can only see the k numbers in the window. Each time the sliding window moves right by one position.

Return the max sliding window.

Example 1:

Input: nums = [1,3,-1,-3,5,3,6,7], k = 3

Output: [3,3,5,5,6,7]

Explanation: 

Window position                Max

---------------               -----

[1  3  -1] -3  5  3  6  7       3
 1 [3  -1  -3] 5  3  6  7       3
 1  3 [-1  -3  5] 3  6  7       5
 1  3  -1 [-3  5  3] 6  7       5
 1  3  -1  -3 [5  3  6] 7       6
 1  3  -1  -3  5 [3  6  7]      7

Loop 1 q = [1]
Loop 2 q = [3]
Loop 3 q = [3, -1] r = [3]

The tricky part of the problem is the design of queue.  We need to make it
so the maximum at every window is at the front of the queue.

Case 1 next number is higher then the end
  We remove the end since the next number is more recent and will be removed later
  We need to keep doing this if all the numbers are less then what are being added

Case 2 next number is lower then the end
  Just add it to the end of the queue since the maximum may get removed later
  
   1 
<--------
   remove 1 add 3 since 3 will be removed later in the window slide 
<--------
   add -1 since it may be the max after the 3 is removed
<--------

The next tricky part is when to shift the queue. One approach is to check if the front
of the window is equal to the top of the queue.  If it is removed it.

Psedocode

init result, queue and j // this is the left side of the window
Loop from i to length of array // this represents the right side of the window
  While length is not empty and num[i] > end of queue
    pop the queue
  push num[i]
  if i is at the end of the window
    push top of queue to result
    check if top of queue is equal to num[j] is so remove the top of the queue
    j++
return result
