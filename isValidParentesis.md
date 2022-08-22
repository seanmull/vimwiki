Given a string s containing just the characters '(', ')', '{', '}', '[' and ']', determine if the input string is valid.

An input string is valid if:

Open brackets must be closed by the same type of brackets.
Open brackets must be closed in the correct order.
 

Example 1:

Input: s = "()"
Output: true

The solution to this problem is using a stack.
We push to the stack any open parentesis and compare the closing parentesis as
we go.  If the stack isn't empty at the end we know its not valid

Make a map with parentesis.
Loop through the string
  if the element is an open bracket
    push to stack
  if the element does not have a matching closing bracket
    return false
  else
    pop the stack
return if length of stack is zero
