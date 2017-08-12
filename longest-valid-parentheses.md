### 问题描述

给定一串括号字符串，求合法连续括号的最长字符串

```javascript
var longestValidParentheses = function (s) {
    if (s.length < 2) return 0
    var lens = [], // 存储所有合法括号字符串的长度
        max = 0,
        lastIndex = s.length - 1
    lens[lastIndex] = 0 // 初始化，
    lens[lastIndex + 1] = 0 // 处理超界状态下的长度
    for (var i = lastIndex; i--;) { // 倒序排序减少操作次数，能小副提升性能
        lens[i]=0
        if (s[i] == '(') {
            if (s[i + 1] == ')') {
                lens[i] = lens[i + 2] + 2 // 继承【相邻合法串的长度】+2
            } else if (s[i + lens[i + 1] + 1] == ')') {
                lens[i] = lens[i + 1] + lens[i + lens[i + 1] + 2] + 2 
                // 继承【包含合法串的长度】和【相邻合法串的长度】+2
            }
            max = Math.max(max, lens[i])
        }
    }
    return max
};
```

