## 【题目】

剑指 Offer 09. 用两个栈实现队列

## 【破题】

 用两个栈实现队列，想到的首先就是栈的特性和队列的特性，那么栈的特性就是先进后出，队列的特性是先进先出。它们有一个共同特性，就是后进的，在“排列”上市在前面的，但是出的顺序不一样，所以队列“先进”的特性可以直接用栈，而“先出”的特性跟栈是相反的，那么就让栈先出去（顺序是后进的先出去），再进栈，这时候顺序就是后进的在前面，先进的在后面，根据栈后进先出的特性，后面的（先进队列的）先出栈

## 【分析】

栈和队列都属于线性表的结构，对于JavaScript来说，只有数组是最为贴近的，实际上js里也没有真正的栈和队列，都只能用数组来进行模拟。上面我们分析需要先全部出栈一次，再入栈一次，那么就需要两个栈。由于有进栈和出栈两个动作，我们就对应着一个用来模拟队列入队，一个用来模拟队列出队。模拟入队的栈要全部出栈，模拟出队的栈要全部接收到然后入栈。那么时机呢？入队是可以不受影响的，需要考虑的是什么时候入队的栈全部出栈反向入队到出队的栈呢？那当然是出栈的队列中没有元素的时候了。

## 【代码】

```javascript
var CQueue = function() {
    this.enqueue = [];
    this.dequeue = [];
};

/** 
 * 入队
 * @param {number} value
 * @return {void}
 */
CQueue.prototype.appendTail = function(value) {
    this.enqueue.push(value);
};

/**
 * 出队
 * @return {number}
 */
CQueue.prototype.deleteHead = function() {
    if(this.dequeue.length) return this.dequeue.pop();
    if(!this.enqueue.length) return -1;
    let len = this.enqueue.length;
    // 出队的栈全部出栈，反向进入到入队的栈
    while(--len >= 0){        
        this.dequeue.push(this.enqueue.pop())
    }
    return this.dequeue.pop();
};
```
## 【leetcode地址】
[超级简单易懂，说清楚用栈实现队列](https://leetcode-cn.com/problems/yong-liang-ge-zhan-shi-xian-dui-lie-lcof/solution/chao-ji-jian-dan-yi-dong-shuo-qing-chu-y-wkzz/)