### 问题描述

给定一组英文单词的根，再给定一句英文句子，将句子中包含根的单词替换为根

#### 例子

```
Input: dict = ["cat", "bat", "rat"]
sentence = "the cattle was rattled by the battery"
Output: "the cat was rat by the bat"
```

### 解决方案

#### 一：数组循环（696 ms）

```javascript
var replaceWords = function (dict, sentence) {
    var regs = [],
        words = sentence.split(' '),
        wordsLen = words.length
    for (var i = dict.length; i--;) {
        var root = dict[i]
        for (var j = wordsLen; j--;) {
            if (words[j].indexOf(root) == 0) {
                words[j] = root
            }
        }
    }
    return words.join(' ')
};
```

#### 二：处理标记 + 字符串截取

```javascript
var replaceWords = function (dict, sentence) {
    var regs = [],
        words = sentence.split(' '),
        wordsLen = words.length,
        maps = [], // 用于标记该单词是否被处理
        dictLen = dict.length
    for (var i = 0; i < dictLen; i++) {
        var root = dict[i],
            len = root.length
        for (var j = wordsLen; j--;) {
            if (!maps[j] && words[j].substr(0, len) == root) { 
              // 只判断字符串开头，所以用字符串截取后直接匹配比 indexOf 快
                words[j] = root
                maps[j] = true
            }
        }
    }
    return words.join(' ')
};
```

