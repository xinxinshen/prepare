##  变量提升

JS引擎的工作方式是，先从上到下解析代码，然后将所有声明的变量提升到代码的头部，再逐行执行，这就叫做变量提升。

```javascript
console.log(a)
var a;
a = 1;
```

``` javascript
var a = undefined;
console.log(a);
a = 1;
```

## 一段JS代码是如何执行的

```javascript
setTimeout(function(){
    console.log('定时器开始啦')
});

new Promise(function(resolve){
    console.log('马上执行for循环啦');
    for(var i = 0; i < 10000; i++){
        i == 99 && resolve();
    }
}).then(function(){
    console.log('执行then函数啦')
});

console.log('代码执行结束');
/**
*
马上执行for循环啦

'代码执行结束'

执行then函数啦

定时器开始啦
*/
```

1. javascript是一门**单线程**语言

2. Javascript事件循环：js中的任务分为同步任务和异步任务：

   1. 同步和异步任务分别进入不同的执行"场所"，同步的进入主线程，异步的进入Event Table并注册函数。
   2. 当指定的事情完成时，Event Table会将这个函数移入Event Queue
   3. 主线程内的任务执行完毕为空，会去Event Queue读取对应的函数，进入主线程执行。
   4. 上述过程会不断重复，也就是常说的Event Loop(事件循环)。

   

3. 怎么知道主线程执行栈为空？
   1. js引擎存在monitoring process进程，会持续不断的检查主线程执行栈是否为空，一旦为空，就会去Event Queue那里检查是否有等待被调用的函数。

4. setInterval
   1. `setInterval`会每隔指定的时间将注册的函数置入Event Queue
   2. 一旦**`setInterval`的回调函数`fn`执行时间超过了延迟时间`ms`，那么就完全看不出来有时间间隔了**
5. 宏任务和微任务
   1. 宏任务：包括整体代码script，setTimeout，setInterval
   2. 微任务：Promise，process.nextTick

```javascript
// 做一下这道题，验证一下事件循环是否学会了
console.log('1');

setTimeout(function() {
    console.log('2');
    process.nextTick(function() {
        console.log('3');
    })
    new Promise(function(resolve) {
        console.log('4');
        resolve();
    }).then(function() {
        console.log('5')
    })
})
process.nextTick(function() {
    console.log('6');
})
new Promise(function(resolve) {
    console.log('7');
    resolve();
}).then(function() {
    console.log('8')
})

setTimeout(function() {
    console.log('9');
    process.nextTick(function() {
        console.log('10');
    })
    new Promise(function(resolve) {
        console.log('11');
        resolve();
    }).then(function() {
        console.log('12')
    })
})
```

写在最后：

1. 事件循环是js实现异步的一种方法，也是js的执行机制
2. javascript是一门单线程语言
3. Event Loop是javascript的执行机制



## 聊一下闭包（todo）

MDN：函数和对其周围状态（**lexical environment，词法环境**）的引用捆绑在一起构成**闭包**（**closure**）。也就是说，闭包可以让你从内部函数访问外部函数作用域。在 JavaScript 中，每当函数被创建，就会在函数生成时生成闭包。



## javascript的作用域链理解吗？

## ES6模块和CommonJS模块有什么区别？

## 谈谈你对原型链的理解？

## 谈谈你对this的理解？

​	箭头函数的this指向哪里

## async/await是什么？

​	其相对于Promise的优势？

JS的参数是按照什么方式传递的

## 如何在JS中实现不可变对象

## JS的基本类型和复杂类型是存储在哪里的？

## 讲讲JS的垃圾回收是怎么做的？

