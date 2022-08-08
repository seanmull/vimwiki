You are given an array prices where prices[i] is the 
price of a given stock on the ith day.

You want to maximize your profit by choosing a single day 
to buy one stock and choosing a different day in the future to sell that stock.

Return the maximum profit you can achieve from this transaction. If you cannot achieve any profit, return 0.

Input: prices = [7,1,5,3,6,4]
Output: 5

Explanation: Buy on day 2 (price = 1) and sell on day 5 (price = 6), profit = 6-1 = 5.
Note that buying on day 2 and selling on day 1 is not 
allowed because you must buy before you sell.

We need to find the best combo of buy and sell times and the only constraint is
that buy must be before sell

The best combo is one that yields the largest difference between buy and sell times

[7, 1, 5, 3, 6, 4]
 <------  s    
    min
    
s = sell date
min = the minimum value to left of s

The trick of the problem is to make sure buy must always be before sell in a one
pass algorthm.  We loop through all dates from n = 1 the end.
While this is happening track the difference between the minimum from that value
and that value.

max = 0
b = a[0]
loop s -> end
  update max to max of max and a[s] - a[b]
  update buy to be min between a[b], a[s]
return buy

[7, 1, 5, 3, 6, 4]
 b  s                  max = 0 buy = 1 
    b  s               max = 4 buy = 1
    b     s            max = 4 buy = 1
    b        s         max = 5 buy = 1
    b           s      max = 5 buy = 1
    
returns 5
