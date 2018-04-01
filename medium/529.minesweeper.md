### 问题描述

这个就是个扫雷游戏判定系统啦，给定当前雷区的状态二维数组，再给一个点击的坐标数组，求点击之后的状态二维数组

#### 例子

```javascript
Input: 
[['E', 'E', 'E', 'E', 'E'],
 ['E', 'E', 'M', 'E', 'E'],
 ['E', 'E', 'E', 'E', 'E'],
 ['E', 'E', 'E', 'E', 'E']]

Click : [3,0]

Output: 
[['B', '1', 'E', '1', 'B'],
 ['B', '1', 'M', '1', 'B'],
 ['B', '1', '1', '1', 'B'],
 ['B', 'B', 'B', 'B', 'B']]
```

#### 提示

 - 雷区的长和宽的范围都是 [1, 50]
 - 点击只会点在 `M` 和 `E` 上，所以不会点在数字上，也表示至少有一个可点击的小方块
 - 给定的雷区不会是一个游戏结束的状态，就是说没有雷被点到
 - 简单起见，你不需要标记出所有雷，即时你踩到雷或你赢了这个游戏

### 解决方案（深度搜索）

- 如果点到一个雷 `M`，标记为 `X` 并返回 
- 如果点到的是空 `E`，则要开始搜索周围的雷区
  - 如果周围有雷，标记周围雷的个数并返回
  - 如果周围没有雷，则标记为 `B` ，并搜索更新这个点周围 8 个点的状态

```javascript
var updateBoard = function(board, click) {
    var width = board[0].length,
        height = board.length
    return helper(click)
    
    function helper(click) {
      	var y = click[0], 
            x = click[1], 
            maps = [] // 用于存储需要搜索的位置
        if (board[y][x]=='M') {
            board[y][x]='X'
        } else {
            var count = 0
            for (var i=-1;i<2;i++) {
                for (var j=-1;j<2;j++) {
                    if (i==0 && j==0) continue // i 和 j 为 0 时表示当前点击位置
                    
                    var _x = x + i, _y=y+j
                    if (_x==-1 || _x==width || _y==-1 || _y==height) continue 
                    // 越界，本来是用 board[_y][_x] 来判断的，但检索速度不如数值比较来得快
                    
                    var temp = board[_y][_x]
                    if (temp=='M') {
                        count++
                    } else if (temp == 'E') { // 如果这个位置为 E，表示未搜索过，则放入搜索数组 maps
                        maps.push([_y, _x])
                    }
                }
            }
            if (count) { // count>0, 
                board[y][x] = count+''
            } else {
                board[y][x] = 'B'
                while(maps[0]) {
                    updateBoard(board, maps.pop())
                }
            }
        }
        return board
    }    
};
```

