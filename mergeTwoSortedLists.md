
You are given the heads of two sorted linked lists list1 and list2.

Merge the two lists in a one sorted list. The list should be made by splicing together the nodes of the first two lists.

Return the head of the merged linked list.

Input: list1 = [1,2,4], list2 = [1,3,4]

Output: [1,1,2,3,4,4]

We need to perform merge sort on this list.

[1,2,4] , [1,3,4] => [1] pick 1
 ^         ^
[1,2,4] , [1,3,4] => [1,1] pick 1
   ^       ^
[1,2,4] , [1,3,4] => [1,1,2] pick 2
   ^         ^
.....

But we need to do this while splicing together the linked list.
Steps:
1. Create dummy node that will be the head of the new linked list
2. Add pointer p1 and p2 to the head of each list we want to splice
3. Compare values of p1 and p2 being careful to look out for the case either is null
4. Guard against null case then do the comparision
5. Point the tail of the new list to the lower of the two
6. Increment pointers of the new list and picked element
7. Disconnect the pointer of the new list by pointing to null.  This overrides the pointer that was pointing to the next value in p1 or p2.
8. Return the dummy.next

make new node dummy
point to dummy
p1 and p2 point to list1 and list2
while either p1 or p2 is not null
	if p1 is null
		newlist point to p2
		increment p2
	else if p2 is null
		newlist point to p1
		increment p1
	else if p1 < p2
		newlist point to p1
		increment p1
	else
		newlist point to p2
		increment p2
	newlist point to null
return dummy.next
