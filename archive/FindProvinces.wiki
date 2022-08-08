There are n cities. Some of them are connected, while some are not. 
If city a is connected directly with city b, and city b is connected directly with city c, then city a is connected indirectly with city c.
A province is a group of directly or indirectly connected cities and no other cities 
outside of the group.
You are given an n x n matrix isConnected where isConnected[i][j] = 1 
if the ith city and the jth city are directly connected, and isConnected[i][j] = 0 otherwise.
Return the total number of provinces.

Input: isConnected = [[1,1,0],[1,1,0],[0,0,1]]
Output: 2

[1, 1, 0], [1, 1, 0], [0, 0, 1]
    0          1          2
    
City 0 is connected to itself and City 1
City 1 is connected to itself and City 0
City 2 is connected to itself

City 0 and City 1 form a province
City 2 is an alone province

Create an array that indicates the cities we have visited

Create a function that
Passed in the array
  Mark current city as visited
  if its not already been visited and there isConnnected == 1
  function(city)
  
Loop through each city
  if city hasn't been visited
    call function
    add to provinces


