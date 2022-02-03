### 问题描述

寻找二叉树的最大深度



### 方法：递归

```javascript
var maxDepth = function(root) {
    if (root == null) return 0
    if (root.left==null && root.right==null) return 1
    return Math.max(maxDepth(root.left), maxDepth(root.right))+1
};
```



