The problem is given an array find if 3 numbers sum to 0

let nums = [-1,0,1,2,-1,-4]

Have three pointers arranged as such
[-1,0,1,2,-1,-4]
  i j         k
  
The idea behind this is to have binary search on j and k
If i + j + k are too high decrement k
If i + j + k are too low increment j
We have to constantly check if i, j or k have adjectent repeats if so move the letter accordingly

```
Sort the list (nlogn)
Loop i from 0 to length - 2
If i > 0 and a[i] === a[i + 1] skip this case since it will produce a repeat
Set j to one more the i and k to the last index
Loop until j crosses over k
If sum is greater then 0 k--
if sum is less then 0 j++
else
  push the numbers
  if j has repeats j++
  if k has repeats k--
  j++ k--
return the result

```
