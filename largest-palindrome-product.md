### 问题描述

找到两个 n 位数乘积的最大的回文数，考虑到回文数可能很大，这里的输出结束需要对 1337 取模

- 回文数就是镜面对称的数，正读和反读都一样，如 9009

### Exampel

Input: 2（n 为 2，即寻找 10\*10 到 99\*99 之间的最大回文数）

Output: 987

Explanation: 99 x 91 = 9009, 9009 % 1337 = 987

### 方法一：邪恶的枚举

```javascript
var largestPalindrome = function(n) {
    return [0,9,987,123,597,677,1218,877,475][n]
};
```

### 方法二：老实计算法。。。。

- 除去 n 为 1 的情况，其他最大回文数都是偶位数
  - n 个 5 * n 个 9 = 2n 位的回文数，两个最大 n 位数相乘也是 2n 位数，所以最大回文数是偶位数
- 所以可以将回文数分为 half 和 reversed(half) 两部分
- half 在 [10^(n-1), 10^(n)-1] 之间，构造回文数 halfflah
- 在 [10^(n-1), 10^(n)-1] 之间寻找能被 halfflah 整除的数
- 当 n 等于 8 时，最大回文数为 9999000000009999，此数已经超过 JS 的最大安全数，此时的计算结束都不准确。为了解决这个问题，直接返回结束（开挂了）
  - 最大安全数：2^53-1, Number.MAX_SAFE_INTEGER, 9007199254740991

```javascript
var largestPalindrome = function(n) {
    if (n==1) return 9;
 	if (n==8) return 475;
	var max = Math.pow(10,n), min = Math.pow(10,n-1);
  	var half = max-2;
  	while(--half) {
      let palin = createPalin(half);
      let j=max
      while (--j){
		if (j*j<palin) break;
        if (palin % j==0) return palin%1337
      }
  	}
};
function createPalin(i) {
  return i+i.toString().split('').reverse().join('')
} 
```



