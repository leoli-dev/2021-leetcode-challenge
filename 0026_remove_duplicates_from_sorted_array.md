# 26. Remove Duplicates from Sorted Array

- URL: https://leetcode.com/problems/remove-duplicates-from-sorted-array/
- Description:

    > Given a sorted array nums, remove the duplicates in-place such that each element appears only once and returns the new length.
    > Do not allocate extra space for another array, you must do this by modifying the input array in-place with O(1) extra memory.

- Tags: `Array`, `Two Pointers`
- Difficulty: __Easy__

## First try

```php
class Solution {
    function removeDuplicates(&$nums) {
        $nums = array_unique($nums);
        return count($nums);
    }    
}
```

Result:
- Runtime: 28 ms
- Memory: 18.2 MB

Problem:
- It's too slow and it took too much memory.
-  `array_unique()` will return a new array instead of modifying the original one, it doesn't meat the requirement.

## Final submit

```php
class Solution {
    function removeDuplicates(&$nums) {
        if (empty($nums)) {
           return 0; 
        }
        $length = count($nums);
        for ($i = 0; $i < $length; $i ++) {
            $current = current($nums);
            $next = next($nums);
            if ($current === $next) {
                unset($nums[$i]);
            }
        }
        
        return count($nums);
    }
}
```

Result:
- Runtime: 24 ms
- Memory: 17.6 MB

Improvements:
- All the operations stay in the original array
- Using [Two Pointers Technique](https://www.geeksforgeeks.org/two-pointers-technique/)
- less memory and faster
- Using `current()`, `next()` functions to manipulate the internal pointer of array
