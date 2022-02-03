### 问题描述
数字反转，将数字镜像反转，并保留正负符号
- 入参是 32 位的数字，如果出参数字大于 32 位，直接返回 0

### 方法一：字符串处理（166 ms）
```
var reverse = function (x) {
    var flag = x > 0,
        str = x + '',
        num = 0;
    if (flag) {
        num = +(str.split('').reverse().join(''));
    } else {
        num = -(str.split('').splice(1).reverse().join(''));
    }
    if (num >> 0 == num) {
        return num;
    } else {
        return 0;
    }
};
```

### 方法二：数学处理（146 ms）
```
var reverse = function (x) {
    var temp = 0,
        res = 0,
        sign = x < 0;

    sign && (x *= -1);
    while (x > 0) {
        temp = x % 10
        res = res * 10 + temp;
        x = (x - temp) / 10
    }
    if (res >> 0 != res) {
        return 0
    }
    return sign ? -res : res
};
```
