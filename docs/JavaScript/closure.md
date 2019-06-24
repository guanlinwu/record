一 代码片段：
```javascript
for (var i = 0; i < 5; i++) {
    setTimeout(function() {
        console.log(i);
    }, 1000);
}

console.log(i);
```

(1) 以下代码会输出
A. 0,1,2,3,4,5
B. 5,0,1,2,3,4
C. 5,5,5,5,5,5 (正确答案)

(2.1) 利用闭包改造，输出 5 -> 0,1,2,3,4
```javascript
// 声明即执行的函数表达式
for (var i = 0; i < 5; i++) {
  (function(j) {  // j = i
      setTimeout(function() {
          console.log(j);
      }, 1000);
  })(i);
}

console.log(i);
```
(2.2) 不用利用闭包改造，输出 5 -> 0,1,2,3,4
```javascript
// setTimeout的传参
for (var i = 0; i < 5; i++) {
    setTimeout(function(i) {
        console.log(i);
    }, 1000, i);
}

console.log(i);
```

```javascript
// 按值传递
var output = function (i) {
    setTimeout(function() {
        console.log(i);
    }, 1000);
};

for (var i = 0; i < 5; i++) {
    output(i); // 这里传过去的 i 值被复制了
}

console.log(i);
```
(3) 如果要满足以下条件，（加分题）
a 输出0 -> 1 -> 2 -> 3 -> 4 -> 5，
b 代码执行时，立即输出 0，之后每隔 1 秒依次输出 1,2,3,4，循环结束后在大概第 5 秒的时候输出 5
c 利用Promise解决，或者ES7async await 特性


```javascript
//【利用Promise解决】
let tasks = [] // 存放异步操作的primose
const output = (i) => new Promise((resolve) => {
    setTimeout(() => {
        console.log(i);
        resolve();
    }, 1000 * i);
});

// 生成全部的异步操作
for (var i = 0; i < 5; i++) {
    tasks.push(output(i));
}

// 异步操作完成之后，输出最后的 i
Promise.all(tasks).then(() => {
    setTimeout(() => {
        console.log(i);
    }, 1000);
});
```

```javascript
//【ES7async await 特性】
const sleep = (time) => new Promise((resolve) => {
    setTimeout(resolve, time);
});

(async () => {  // 声明即执行的 async 函数表达式
    for (var i = 0; i < 5; i++) {
		console.log(i);
        await sleep(1000);

    }
    console.log(i);
})();
```

二 用闭包实现一个计数器，要求
（1）计数器有私有变量(命名自定，假设私有变量命名为count)，初始值为0
（2）计数器有加，减，清零，取值4个功能函数
其中
加函数（increment）： 私有变量count加1，并返回执行后的count
减函数（decrement）：私有变量count减1，并返回执行后的count
清零（reset）: 私有变量count重置为0，并返回执行后的count
取值 (getValue): 获取私有变量count的值
（3）依次执行实现的计数器的加函数，取值函数。

```javascript
var counterObj = (function() {
  var count = 0

  return {
    increment: function() {
		return ++count
    },
    decrement: function() {
		return --count
    },
	reset: function () {
		count = 0
		return count
	},
    getValue: function() {
      return count
    }
  }
})();

counterObj.increment() // 加函数
counterObj.getValue() // 取值函数
```

三 用es6的class对上述计数器进行改造
```javascript
const Counter = (() => {
    const _count = Symbol('count') // 保护私有变量
    class Counter {
        constructor () {
            this[_count] = 0
        }
        increment () {
            return ++this[_count]
        }
        decrement () {
            return --this[_count]
        }
        reset  () {
            this[_count] = 0
            return this[_count]
        }
        getValue () {
          return this[_count]
        }
    }

    return Counter
})()

let counterObj = new Counter()
counterObj.increment() // 加函数
counterObj.getValue() // 取值函数
```

四 用闭包实现一个四则计数器
（1）计数器有私有变量初始值为0
（2）计数器有加，减，乘，除，赋值，取值 这几个功能函数
加函数 (increment)
减函数 (decrement)
乘函数 (multiplication)
除函数 (division)
赋值 (setValue)
取值 (getValue)
（3）可以做到链式调用，类似JQuery的$('selector').eq(0).addClass('className')的链式调用
（4）依次执行加 赋值(1).加(1).乘(2).减(3).除(4).取值()

```javascript
/* 加函数
 * @method increment
 * @param {Number} num 加数
 * @return {Object} 示例本身
*/
/* 减函数
 * @method decrement
 * @param {Number} num 减数
 * @return {Object} 示例本身
*/
/* 乘函数
 * @method multiplication
 * @param {Number} num 乘数
 * @return {Object} 示例本身
*/
/* 除函数
 * @method division
 * @param {Number} num 除数
 * @return {Object} 示例本身
*/
```