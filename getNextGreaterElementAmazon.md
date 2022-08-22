Given an array return an array the provide the next highest element at every position.
If there is no greater element return -1

[1,3,6,2,5,10] => [3,6,10,5,10,-1]

Use a stack to solve this and store the index for all values equal or less the one
you are comparing.


Fill an array with -1 (Results)
Initialize 0 to be top of stack
Loop from 1 to end
  While arr[i] > top of stack value
    results[poped index from stack] = arr[i] 
  push i to stack
return stack
