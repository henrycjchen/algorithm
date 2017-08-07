### 问题描述

```javascript
/**
 * @param {number[]} price
 * @param {number[][]} special
 * @param {number[]} needs
 * @return {number}
 */
```

#### example

```
Input: [2,5], [[3,0,5],[1,2,10]], [3,2]
Output: 14
Explanation: 
第一个参数表示有两个商品 A 和 B，价格分别是 2 元 和 5 元 
第二个参数表示有两种优惠方案
	优惠方案 1，3 个 A 和 0 个 B 的价格是 5 元
    优惠方案 2，1 个 A 和 2 个 B 的价格是 10 元
第三个参数表示需要的购买量，需要买 3 个 A 和 2 个 B，求能购买到规定商品的最优惠的价格
```

#### tips

1. 最多有 6 种商品，100 种优惠方案
2. 每样商品，最多只会买 6 件
3. 不允许购买超过指定数量的商品，即时这样可能会更优惠（很无奈）

### 方案一：递归（522 ms）

```javascript
var shoppingOffers = function(price, special, needs) {
  	var len = needs.length;
  	return shopping(needs)
    function shopping(needs) {
      	var res = noSpecial(needs)
        for (s of special) {
          	var _needs = Array.from(needs) // 克隆，防止修改到原数据
            for (var i=len;i--;) {
              	var diff = _needs[i]-s[i]
                if (diff < 0) break
                _needs[i]=diff
            }
          	if (i == -1) {
              	res = Math.min(res, s[len]+shopping(_needs))
          	}
        }
      	return res
    }
  	function noSpecial(needs) { // 计算直接购买所需费用
      	var res = 0;
      	for (var i=len;i--;) {
          	res += price[i] * needs[i]
      	}
      	return res
  	}
};
```



### 方案二：递归 + maps（349 ms）

```javascript
var shoppingOffers = function(price, special, needs) {
  	var len = needs.length, maps={};
  	return shopping(needs)
    function shopping(needs) {
      	var res = maps[needs]
      	if (res) return res
      	res = noSpecial(needs)
        for (s of special) {
          	var _needs = Array.from(needs) // 克隆，防止修改到原数据
            for (var i=len;i--;) {
              	var diff = _needs[i]-s[i]
                if (diff < 0) break
                _needs[i]=diff
            }
          	if (i == -1) {
              	res = Math.min(res, s[len]+shopping(_needs))
          	}
        }
      	return maps[needs]=res
    }
  	function noSpecial(needs) { // 计算直接购买所需费用
      	var res = 0;
      	for (var i=len;i--;) {
          	res += price[i] * needs[i]
      	}
      	return res
  	}
};
```

### 方案三：？

```javascript
var shoppingOffers = function (price, special, needs) {
 	var min = 0, specialLen = special.length, needsLen = needs.length;
  	for (var i=needsLen;i--;) {
      	min += needs[i]*price[i]; // 计算直接购买所需费用
  	}
  	for (var i=specialLen;i--;) {
      	var valid = true // 优惠方案是否有效
        for (var j=needsLen;j--;) {
          	if (special[i][j] > needs[j]) {
              	valid = false;
                break;
          	}
        }
      	if (!valid) continue; // 无效则进行下一个优惠方案的判断
        var _needs = Array.from(needs),
          	curPrice = special[i][needsLen];
        for (var j=needsLen;j--;) {
          	_needs[j] -= special[i][j];
        }
      	curPrice += shoppingOffers(price, special, _needs);
        if (curPrice < min) min = curPrice;
  	}
  	return min
}
```

