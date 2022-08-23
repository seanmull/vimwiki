Given a string containing digits from 2-9 inclusive, return all possible letter combinations that the number could represent. Return the answer in any order.

A mapping of digits to letters (just like on the telephone buttons) is given below. Note that 1 does not map to any letters.

Example 1:

Input: digits = "23"
Output: ["ad","ae","af","bd","be","bf","cd","ce","cf"]

We can use recursion to get all the combinations possible for each number.
             
             
               ""
               
            a   b   c
            
          d e f .....
          
Steps
1. Build a map for all the buttons { 2: [a,b,c], ...}
2. Init results
3. Create a recursive function that loops through all the combinations for the string
4. If the combo is the same length as the string add it to results

Notice: make sure you pass variable rather then store them as state since we want to keep the state
of i and combo in the stack.  All changes should be passed.

Pseudocode
init results
make map of numbers to letters
function getCombos
  if i is the length of digits
    push combo to results
  get the table for the current digits
  loop table from 0 to length
    call getCombos (i + 1, combo + table[j]) //this insures the state doesn't change as we loop
call getCombos
return results

