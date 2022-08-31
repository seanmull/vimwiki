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
  

let search = function(nums, target) {
    if (!nums.length) return -1;
    let [l, r] = [0, nums.length-1];
    while (l !== r) {
        let m = Math.trunc((l + r) / 2);
        if (nums[l] < nums[m]) {
            // target contained on left?
            if (nums[l] <= target && target <= nums[m]) r = m;
            else l = m + 1;
        }
        else {
            // target contained on right?
            if (nums[m+1] <= target && target <= nums[r]) l = m +1;
            else r = m;
        }
    }
    return (nums[r] == target)? r: -1;
}


