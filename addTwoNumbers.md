You are given two non-empty linked lists representing two non-negative integers. The digits are stored in reverse order, and each of their nodes contains a single digit. Add the two numbers and return the sum as a linked list.

You may assume the two numbers do not contain any leading zero, except the number 0 itself.

Input: l1 = [2,4,3], l2 = [5,6,4]
Output: [7,0,8]
Explanation: 342 + 465 = 807.

2 -> 4 -> 3
5 -> 6 -> 4
          
5 + 2 < 10 so just add them 7
4 + 6 < 10 we have to carry over and minus 10 so 0
3 + 4 + 1 (carry over) < 10 ok just add them 8

The trick to this problem is handling the event we have a carryover.  Especially at the end
of the loop.  We also need to do a fair amount of pointer management with 3 lists.

Steps
1. Create to pointers at the head of the lists
2. Make a dummy element to be the head of the new list
3. Init the carry_over = 0
4. Loop checking two conditions
5.  Are we not at the end of both lists
6.  Do we have no carry over
7. Guard against the case pointer are pointers are null (default to zero)
8. Gather the sum as a + b + carry over
9. Assign carry over if we sum to more then 9
10. If we are over 10
11.  Get the remainder of the value
11.Else
     Get the sum
12. Link this to list
13. Increment both lists if they are not null

Init p1 and p2 pointers to be head of lists
Create dummy node to be the new list
init co and head of new list
while both p1 and p2 are not null or carry over is not 0
  Note: this insures that we are not at the end of both lists and we have no carry over
  get values from p1 and p2 (guarding against null)
  add v1 + v2 + co
  assign co if sum > 9  
  get remainder of sum
  create node new sum if theres no co new rm if there is
  attach new node to new list
  increment all three lists
return dummy.next
