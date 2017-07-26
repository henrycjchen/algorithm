### 问题描述
给定两个链结构，每个链有 3 个节点，对两个链求和，返回新的链
- 每个节点只保留 1 位，逢 10 进 1

### 方法一
```
var addTwoNumbers = function(l1, l2) {
    var l3 = new ListNode((l1.val+l2.val)%10);
    var temp = (l1.val+l2.val)/10>>0;
    var t3 = l3;
    while(l1.next||temp||l2.next) {
        l1 = l1.next||{};
        l2 = l2.next||{};
        t3.next = new ListNode(((l1.val||0)+(l2.val||0)+temp)%10);
        temp = ((l1.val||0)+(l2.val||0)+temp)/10>>0;
        t3 = t3.next;
    }
    
    return l3;
};
```
