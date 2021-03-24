# 1. Two Sum

- URL: https://leetcode.com/problems/two-sum/
- Description:

    > Given an array of integers `nums` and an integer `target`, return indices of the two numbers such that they add up to `target`.
    > You may assume that each input would have exactly one solution, and you may not use the same element twice.
    > You can return the answer in any order.

- Tag: `Array`, `Hash Table`
- Difficulty: __Easy__

## First try

Using a brute-force approche with double for loops.

```php
class Solution {

    /**
     * @param Integer[] $nums
     * @param Integer $target
     * @return Integer[]
     */
    function twoSum($nums, $target) {
        if (!is_array($nums) || 2 > count($nums)) {
            throw new \Exception('Invalid input');
        }
        $length = count($nums);
        for ($i = 0;  $i < $length - 1; $i ++) {
            for ($j = $i+1; $j < $length; $j++) {
                if ($nums[$i] + $nums[$j] === $target) {
                    return [$i, $j];
                }
            }
        }
        throw new \Exception('No result');
    }
}
```

Result:
- Runtime: 16 ms
- Memory: 15.6 MB

Problem:
- It's too slow (only beats 29.15% of php submissions)

## Final submit

Using a hash table to create a difference's table, here's the process:

1. create an empty table
2. loop all the elements of the integer array
3. in each loop, first of all try to look up the current element from the table
    - if current element doesn't exist in the keys of table, calculate the difference of (target - current element), use the difference as the key and the current index as the value, and add this new key-value pair into the table
    - if current element do exist in the keys, return the current index and the related value of that key.

```php
class Solution {

    /**
     * @param Integer[] $nums
     * @param Integer $target
     * @return Integer[]
     */
    function twoSum($nums, $target) {
        $hashTable = [];
        for ($i = 0; $i < count($nums); $i ++) {
            $num = $nums[$i];
            if (isset($hashTable[$num])) {
                return [$hashTable[$num], $i];
            }
            $hashTable[(string) ($target - $num)] = $i;
        }
    }
}
```

Result:
- Runtime: 8 ms
- Memory: 15.6 MB

Here's the js version

```js
var twoSum = function(nums, target) {
    const hashTable = {}
    for (let i = 0; i < nums.length; i++) {
        const num = nums[i]
        if (hashTable[num] !== undefined) {
            return [hashTable[num], i];
        }
        hashTable[target - num] = i
    }
};
```
