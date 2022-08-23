Given an integer array nums, return an array answer such that answer[i] is equal to the product of all the elements of nums except nums[i].

The product of any prefix or suffix of nums is guaranteed to fit in a 32-bit integer.

You must write an algorithm that runs in O(n) time and without using the division operation.

Example 1:

Input: nums = [1,2,3,4]
Output: [24,12,8,6]

We want to create three arrays:
1. One to store all the numbers multiplied before a number
2. One to store all the numbers multiplied after a number
3. One to multiply list 1 and list 2 together

[1, 2, 3, 4]

before
[1, 1, 2, 6]

after
[24, 12, 4, 1]

before x after
[24, 12, 8, 6]

init pre
init seed = 1
loop for i to length
  add seed to pre 
  pre = pre * arr[i]
  
init post
seed = 1
loop for length to 0 
  add seed to post 
  post = post * arr[i]
  
init results
loop for i to length
  results = post * pre
  
return results
  


