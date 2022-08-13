Given an array of points where points[i] = [xi, yi] represents a point on the X-Y plane and an integer k, return the k closest points to the origin (0, 0).

The distance between two points on the X-Y plane is the Euclidean distance (i.e., √(x1 - x2)2 + (y1 - y2)2).

You may return the answer in any order. The answer is guaranteed to be unique (except for the order that it is in).
```
Input: points = [[1,3],[-2,2]], k = 1
Output: [[-2,2]]

Explanation:

The distance between (1, 3) and the origin is sqrt(10).
The distance between (-2, 2) and the origin is sqrt(8).
Since sqrt(8) < sqrt(10), (-2, 2) is closer to the origin.
We only want the closest k = 1 points from the origin, so the answer is just [[-2,2]].
```

The issue with javascript is it has no heap library.  When they ask for kclosest
of anything it usually implies some kind of comparision algo. Sorting is overkill and not worth the performance hit.

If javascript use sort since we don't have heap:

You can do a sort by a^2 + b^2 and then return the slice of that array.
Make note the sort doesn't actually change the values of the array just sort
by a function.

Its fast but technically nlogn since we sort

If python use the heapq library:
But be knowledgeable about how this library works since it does alot of work in
place.

a = [1,2,3]
heapq.heapify(a) # heaps it inplace
hespq.nsmallest(1, a, lambda a: <some function you want to compare>)
