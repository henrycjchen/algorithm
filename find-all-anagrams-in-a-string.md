### 问题描述

给定字符 s 和 p，记录 s 中 乱序 p 的位置

#### 例子一

```
Input:
s: "cbaebabacd" p: "abc"

Output:
[0, 6]

Explanation:
0 为起始位置是 cba，是 abc 的乱序字符串
6 为起始位置是 bac，是 abc 的乱序字符串
```

#### 例子二

```
Input:
s: "abab" p: "ab"

Output:
[0, 1, 2]

Explanation:
0 为起始位置的是 ab
1 为起始位置的是 ba
2 为起始位置的是 ab
以上都是 ab 的乱序字符串
```

### 解决方案

#### 一、记录每个字母的个数是否相同（O(n*m), 306 ms）

```javascript
var findAnagrams = function(s, p) {
    var pObj = {},sObj={},pLen = p.length,sLen=s.length,res=[]
    for (let i=pLen;i--;) {
        pObj[p[i]] = (pObj[p[i]]||0)+1
    }
    for (let i=pLen;i--;) {
        sObj[s[i]] = (sObj[s[i]]||0)+1
    }
    for (let i=0;i<sLen-pLen+1;i++) {
        var valid = true
        for (let char in pObj) {
            if (sObj[char]!=pObj[char]) {
                valid = false
                break
            }
        }
        if (valid) {
            res.push(i)
        }
        --sObj[s[i]];
        sObj[s[i+pLen]] = (sObj[s[i+pLen]]||0)+1
    }
    return res
}
```

#### 二、检察临界字符（O(n)，178 ms）

```javascript
var findAnagrams = function(s, p) {
    var map = {},
        pLen = p.length,
        sLen=s.length,
        res=[],
        left=0,
        right=0,
        count = pLen
    for (let i=pLen;i--;) {
        map[p[i]] = (map[p[i]]||0)+1
    }
    while(right<sLen) {
        if (map[s[right++]]--) count--
        if (count==0) res.push(left)
        if (right-left==pLen && map[s[left++]]++>=0) count++
    }
    return res
}
```

