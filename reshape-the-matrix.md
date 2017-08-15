### 问题描述

这个问题很简单啦，把一个矩阵重新排列成新的长宽，顺序不变。

#### 注意

如果给定的大小与原来的大小不一致，直接返回原来的矩阵

### 代码

```javascript
var matrixReshape = function(nums, r, c) {
    var width = nums[0].length,
        height = nums.length,
        _r = r;
    if (width*height!=r*c) return nums // 给定的大小与原来的大小不一致，直接返回原来的矩阵
    var newArr = [].concat(...nums), // 将原来的数组平铺到一个新的数组里
    	res=[]
    for (var i=r;i--;) {
        res[i]=[]
    }
    for (var i=r;i--;) {
        for (var j=c;j--;) {
            res[i].unshift(newArr.pop())
        }
    }
    return res
}
```

