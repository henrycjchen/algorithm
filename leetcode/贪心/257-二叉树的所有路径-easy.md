- 深度优先搜索
- 广度优先搜索

## 方案一：深度优先搜索
深度优先，递归搜索
```js
var binaryTreePaths = function(root) {
    const path = new Path(root, '');
    return path.paths;
};

class Path {
    paths = []
    constructor(root, path) {
        if (!root) return;
        path += String(root.val);
        if (!root.left && !root.right) {
            this.paths.push(path);
        }
        path += '->';
        const pathLeft = new Path(root.left, path);
        this.paths.push(...pathLeft.paths);
        const pathRight = new Path(root.right, path);
        this.paths.push(...pathRight.paths);
    }
}
```

## 方案二：广度优先搜索
广度优先，循环遍历，缓存节点
```js
var binaryTreePaths = function(root) {
    const nodeStore = [root];
    const pathStore = [String(root.val)];
    const result = [];
    if (!root) return result;

    while (nodeStore.length) {
        const node = nodeStore.pop();
        const path = pathStore.pop();

        if (!node.left && !node.right) {
            result.push(path);
            continue;
        }


        if (node.left) {
            nodeStore.push(node.left);
            pathStore.push(path + '->' + String(node.left.val))
        }

        if (node.right) {
            nodeStore.push(node.right);
            pathStore.push(path + '->' + String(node.right.val))
        }
    }

    return result;
};

class Path {
    paths = []
    constructor(root, path) {
        if (!root) return;
        path += String(root.val);
        if (!root.left && !root.right) {
            this.paths.push(path);
        }
        path += '->';
        const pathLeft = new Path(root.left, path);
        this.paths.push(...pathLeft.paths);
        const pathRight = new Path(root.right, path);
        this.paths.push(...pathRight.paths);
    }
}
```
