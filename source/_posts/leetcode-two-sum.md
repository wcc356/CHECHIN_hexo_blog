---
title: leetcode/two_sum
date: 2021-05-30 20:53:48
tags:
---

[Two Sum](https://leetcode.com/problems/two-sum/)

[Objects vs. Maps](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Map)

helper func:

- map.has(key) = boolean
- map.get(key) = value

> <explicit>

```
function twoSum(nums: number[], target: number): number[] {
    let hash = new Map;
    for (let i = 0; i < nums.length; i++) {
        const secondNum: number = target - nums[i];
        if (hash.has(secondNum)) {
            return [hash.get(secondNum), i];
        }
        hash.set(nums[i], i);
    }

};
```

> </explicit>
