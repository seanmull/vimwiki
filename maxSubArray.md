Given an integer array nums, find the contiguous subarray (containing at least one number) which has the largest sum and return its sum.

A subarray is a contiguous part of an array.
Example 1:
Input: nums = [-2,1,-3,4,-1,2,1,-5,4]

Output: 6

Explanation: [4,-1,2,1] has the largest sum = 6     

Use kadanes algorithm

Example = [1,-3, 4, 1]
           ^            largest sum = 1 or -Infinity = 1 sumendinghere = 1
              ^         largest sum = 1 or -2 = 1 sumendinghere = 0
                        the sum now starts at 4 since we have negative sum
                 ^      largest sum = 4  sumendinghere = 4
                    ^   largest sum = 4 or 5 sumendinghere = 5
                    
Steps
1. Loop through array
2. Added current elements to maxEndingHere (even if negative)
3. set max to max of maxEnding here or max
4. reset maxending here if it is negative (we just assume we start after the element since its better not to include the negative value)


Code

```
var maxSubArray = function(nums) {
    let maxSoFar = -Infinity   
    let maxEndingHere = 0
    for(let i = 0; i < nums.length; i++){
      // this adds the number even if its negative
      maxEndingHere += nums[i]
      maxSoFar = Math.max(maxEndingHere, maxSoFar)
      // reset the ending number to 0 if negative
      // if we start with a bunch of negatives we just
      // move were the array started to the right
      // this makes sense since you either add -1 or not which one is maximum
      maxEndingHere = Math.max(maxEndingHere, 0)
    }
    return maxSoFar
    
};
```
