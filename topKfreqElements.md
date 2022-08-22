Given an integer array nums and an integer k, return the k most frequent elements. You may return the answer in any order.

Example 1:

Input: nums = [1,1,1,2,2,3], k = 2
Output: [1,2]

Steps
1. Create a frequency counter
2. Build a sorted list returning a map of the most frequent elements

Frequency counter 
Good example below [1,1,2] => {1: 2, 2: 1}
```
let freqCounter = (nums) => {
    let cache = new Map()
    for(let num of nums){
        if(cache.has(num)) {
            let n = cache.get(num)
            cache.set(num, n + 1)
        }else {
            cache.set(num, 1)
        }
    }
    return cache
}
```

Build a sorted lists (by freq) and return a slice of the numbers
with the frequencies striped out
```
var topKFrequent = function(nums, k) {
    //.entries() => [[1,2], [2, 1]]
    return [...freqCounter(nums)
            .entries()]
            // sort by frequency
            .sort((a, b) => b[1] - a[1])
            // take the first k elements
            .slice(0, k)
            // strip frequencies
            .map(ele => ele[0])
};
```


