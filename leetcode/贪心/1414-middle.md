# 和为 K 的最少斐波那契数字数目
经过推演可以知道，为了达到和为 k，必须采用不小于 k 的最大斐波那契数。因此，
k = maxFib(k) + maxFib(k - maxFib(k)) ... 

## 解决方案：贪心算法
```js
/**
 * @param {number} k
 * @return {number}
 */
var findMinFibonacciNumbers = function(k) {
    const fibArr = [1,1]
    let max = 2;
    while (max <= k) {
        fibArr.push(max)
        max = fibArr[fibArr.length - 2] + fibArr[fibArr.length - 1]
    }

    let result = 0;
    for (let i=fibArr.length; i--;) {
        if (k <= 0) break;
        if (fibArr[i] <= k) {
            k -= fibArr[i];
            result += 1;
        }
    }

    return result;
};
```