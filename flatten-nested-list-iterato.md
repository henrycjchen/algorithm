### 问题描述

给定一个特定结构数据组成的数组，将这个数组做扁平化

#### 例子一

```
[[1,1],2,[1,1]] -> [1,1,2,1,1]
```

#### 例子二

```
[1,[4,[6]]] -> [1,4,6]
```

### 解决方案

```javascript
/**
 * // 给定数据的数据结构
 * function NestedInteger() {
 *
 *     判断该数据是否为纯数字
 *     @return {boolean}
 *     this.isInteger = function() {
 *         ...
 *     };
 *
 *     获取当前数据数组
 *     @return {NestedInteger[]}
 *     this.getList = function() {
 *         ...
 *     };
 * };
 */

var NestedIterator = function(nestedList) {
    this.arr = nestedList
};

NestedIterator.prototype.hasNext = function() {
    if (this.arr[0]==undefined) return false
    while (this.arr[0]!=undefined) {
        if(this.arr[0].isInteger()) {
            return true;
        }
        var item = this.arr.shift().getList()
        for(let i = item.length;i--;) {
            this.arr.unshift(item[i])
        }
    }
};

NestedIterator.prototype.next = function() {
    return this.arr.shift()
};

/**
 * 以上代码给被判断系统如下执行
 * var i = new NestedIterator(nestedList), a = [];
 * while (i.hasNext()) a.push(i.next());
*/
```

