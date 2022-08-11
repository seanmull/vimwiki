Design a data structure that follows the constraints of a Least Recently Used (LRU) cache.
Implement the LRUCache class:

LRUCache(int capacity) Initialize the LRU cache with positive size capacity.

int get(int key) Return the value of the key if the key exists, otherwise return -1.

void put(int key, int value) Update the value of the key if the key exists. Otherwise, add the key-value pair to the cache. If the number of keys exceeds the capacity from this operation, evict the least recently used key.

The functions get and put must each run in O(1) average time complexity.

Example 1:

Input

["LRUCache", "put", "put", "get", "put", "get", "put", "get", "get", "get"]
[[2], [1, 1], [2, 2], [1], [3, 3], [2], [4, 4], [1], [3], [4]]

Output

[null, null, null, 1, null, -1, null, -1, 3, 4]

Explanation

LRUCache lRUCache = new LRUCache(2);
lRUCache.put(1, 1); // cache is {1=1}
lRUCache.put(2, 2); // cache is {1=1, 2=2}
lRUCache.get(1);    // return 1
lRUCache.put(3, 3); // LRU key was 2, evicts key 2, cache is {1=1, 3=3}
lRUCache.get(2);    // returns -1 (not found)
lRUCache.put(4, 4); // LRU key was 1, evicts key 1, cache is {4=4, 3=3}
lRUCache.get(1);    // return -1 (not found)
lRUCache.get(3);    // return 3
lRUCache.get(4);    // return 4

The trick with this problem has to do with how maps are implemented.  If you 
use a map you can get an ordering of the key value pair base on the order they are
added for instance:

init map
map.set("a": 1)
map.set("b": 2)
print(map.entries()) => "a": 1 , "b": 2

The "get" method must track when a "get" request for any key was made recently

The "put" method must do two things
1. Check if it would overflow if we added one more element
	1. If so remove the least recently used element
	2. Then add the element either way

First return -1 if its not in the map.  Don't do anything to the map if its not there.
The "get" method can track the update elements by adding and removing the same
element.  This pushes the element to the end of the map

"a" : 1, "b" : 2
 ------------->
   most recently used
<----------------
   least recently used

First with the put method remove any keys it wants to add so the key value is moved
to the end of the map.
The "put" method would set the value to what is passed into it.
It would check to see if it overflowing, if it is remove from the top of the map.

/**
 * @param {number} capacity
 */
var LRUCache = function(capacity) {
   this.map = new Map()
   this.capacity = capacity
};

/** 
 * @param {number} key
 * @return {number}
 */
LRUCache.prototype.get = function(key) {
  if(!this.map.has(key)){
    return -1
  }
  let value = this.map.get(key)
  // this resets the value to end of the map
  this.map.delete(key)
  this.map.set(key, value)
  return value
};

/** 
 * @param {number} key 
 * @param {number} value
 * @return {void}
 */
LRUCache.prototype.put = function(key, value) {
  if(this.map.has(key)){
    this.map.delete(key)
  }
  this.map.set(key, value)
  if(this.map.size > this.capacity){
    // remove the oldest record of the map
    this.map.delete(this.map.keys().next().value)
  }
};

/** 
 * Your LRUCache object will be instantiated and called as such:
 * var obj = new LRUCache(capacity)
 * var param_1 = obj.get(key)
 * obj.put(key,value)
 */
