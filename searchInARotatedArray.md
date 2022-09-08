There is an integer array nums sorted in ascending order (with distinct values).

Prior to being passed to your function, nums is possibly rotated at an unknown pivot index k (1 <= k < nums.length) such that the resulting array is [nums[k], nums[k+1], ..., nums[n-1], nums[0], nums[1], ..., nums[k-1]] (0-indexed). For example, [0,1,2,4,5,6,7] might be rotated at pivot index 3 and become [4,5,6,7,0,1,2].

Given the array nums after the possible rotation and an integer target, return the index of target if it is in nums, or -1 if it is not in nums.

You must write an algorithm with es an integer array nums sorted in ascending order ()(log n) runtime complexity.

Example 1:

Input: nums = [4,5,6,7,0,1,2], target = 0
Output: 4

We need to use binary search for this problem.  We need to split the searches into partitions. One thing to notice is no matter where you split one side will be sorted while the other will not.  

Case 1 Left side is sorted and target is between l and m
  Shrink down r to m 
Case 2 Left side is sorted and target is not between l and m
  Shrink down l to m + 1
Case 3 Right side is sorted and target is between m + 1 and h
  Shrink down l to m + 1
Case 4 Right side is sorted and target is not between m + 1 and h
  Shrink down r to m
  
  
  4, 5, 6, 7, 0, 1, 2  our target = 0
  l        m        r
              l  m  r
              l  r
              lr
  
Steps
init l to 0 r to end
while l and r are not equal
  set m to mid of l and r
  if left side is sorted 
    if target is between l and m
      set r to m // look left
    else
      set l to m + 1 // look right
  else // right is sorted
    if target is between m and r
      set l to m + 1
    else
      set to m
if arr[r] is equal to target return r else -1
