### 问题描述

给一个非空数字数组，求第三大的数字，如果没有第三大的，返回最大的数

#### 提示

- 一样大的数字排并列，比如 `[3,2,2,1]`，`2` 并列排第二大，第三大的就是 `1`
- 要求时间复杂度为 O(n)

### 解决方案

```javascript
var thirdMax = function (nums) {
    var len = nums.length - 1,
        first = nums[len],
        second = -Infinity,
        third = -Infinity;
    for (var i = len; i--;) {
        var temp = nums[i]
        if (temp == first || temp == second || temp == third) continue
        if (temp > first) {
            third = second
            second = first
            first = temp
        } else if (temp > second) {
            third = second
            second = temp
        } else if (temp > third) {
            third = temp
        }
    }
    if (third == -Infinity) return first
    return third
};
```

