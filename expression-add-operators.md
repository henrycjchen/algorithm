### 问题描述

给定数字字符串和目标结果，在数字字符串中添加 `[+, -, *]` 这三种符号形成式子，使式子的结果为目标结果

#### 例子

```
"123", 6 -> ["1+2+3", "1*2*3"] 
"232", 8 -> ["2*3+2", "2+3*2"]
"105", 5 -> ["1*0+5","10-5"]
"00", 0 -> ["0+0", "0-0", "0*0"]
"3456237490", 9191 -> []
```



### 解决方案

```javascript
var addOperators = function(num, target) {
    var res = [];
    helper(num, '', 0, 0);
    return res;
    
    function helper(num, temp, currRes, prevNum) {
        var len = num.length;
        if (len==0) {
            currRes==target && res.push(temp);
            return;
        }
        for (let i=1; i<=len; i++) { // 循环获取当前处理数 currNum 的各种可能性
            var currStr = num.substring(0,i);
            if (currStr.length>1 && currStr[0]=='0') { // 排除 0 开头的两位数
                return; // 直接废除这个式子
            }
            var currNum = +currStr;
            var nextStr = num.substring(i);
            if (temp.length == 0) {
                helper(nextStr, currStr, currNum, currNum)
            } else {
                // 乘法
                helper(nextStr, temp+"*"+currNum, (currRes - prevNum) + prevNum * currNum, prevNum * currNum);
                // 加法
                helper(nextStr, temp+"+"+currNum, currRes + currNum, currNum);
                // 减法
                helper(nextStr, temp+"-"+currNum, currRes - currNum, -currNum); 
            }
        }
    }
};
```

