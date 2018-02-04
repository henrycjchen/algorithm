### 问题描述
从给定的数组 nums 中，找到其中 2 个能相加和等于 target 的，并将这两个数的索引放到数组里并返回

### 方法一（runtime: 562 ms）
```
var twoSum = function(nums, target) {
    for (let i = 0; i < nums.length - 1; i++) {
        for (let j = i + 1; j < nums.length; j++) {
            if (nums[i] + nums[j] == target) {
                return [i, j];
            }
        }
    }
};
```

### 方法二：倒序循环（runtime: 229 ms）
```
var twoSum = function(nums, target) {
    for (let i = nums.length; i--;) { // 倒序循环减少计算步骤
        for (let j = i; j--;) {
            if (nums[i] + nums[j] == target) {
                return [i, j];
            }
        }
    }
};
```

### 方法三：记录“差”（95 ms）
```
var twoSum = function(nums, target) {  
    var maps = {}, // 记录差对应的减数的位置
        num, // 当前数
        p; // 当前数在 maps 中的位置
    for (var i = nums.length; i--;) {
        num = nums[i]
        p = maps[num]
        if (p > -1) {
            return [p, i]
        } else {      
            maps[target - num] = i    
        }
    }
}
```
