### 问题描述

给定字符串，返回这个字符串能拼接成回文串的最大长度

### 方法

```javascript
var longestPalindrome = function(s) {
    var len = s.length, maps={};
    for (let i=len; i--;) {
        var char = s[i]
        maps[char] = (maps[char]||0) +1
    }
    var result = len, hasOdd=0;
    for (char in maps) {
        var num = maps[char]
        if (num & 1) { // 听说用位运算求奇偶会比较快
            --result;
            hasOdd = 1
        }
    }
    return result+hasOdd
};
```

