# JS 函数的执行时机

## 解释如下代码为什么会打印出6个6

```
  let i = 0
  for(i = 0; i<6; i++){
    setTimeout(()=>{
      console.log(i)
    },0)
  }
```
解释这个就必须知道JS的执行机制 -- 事件循环，JS 每执行完一个宏任务，就会去微任务队列清空所有为任务，然后在执行下一个宏任务。
宏任务一般包括：整体Script代码，setTimeout，setInterval以及setImmediate。微任务一般包括：Promise，process.nextTick，MutationObserver

变量i是全局申明的，执行for循环绑定6个定时器，执行延时操作打印出i，整体代码（宏任务）执行完毕，这时for循环已经结束，i为6，此时微任务队列为空，
然后去找到下一个宏任务，执行第一次打印，然后第二次打印 ······ 所以打印出了6个6。
 
## 让上面代码打印 0、1、2、3、4、5 的方法

使用let申明局部变量i，通过闭包保留对i的引用。

```
  for(let i = 0; i<6; i++){
    setTimeout(()=>{
      console.log(i)
    },0)
  }
```

全局申明i，使用立即执行函数通过函数参数传递完成闭包来缓存每次循环之后i的值。

```
  let i = 0
  for(; i < 6; i++) {
    ((i) => {
      setTimeout(() => {
        console.log(i)
      }, 0)
    })(i)
  }
```

使用Promise对象的resolve()函数保存for循环的i的值，然后在 .then 的回调中获取reslove的结果并将其打印出来。

```
  for (var i = 0; i < 6; i++) {
    new Promise((res, rej) => {
      res(i);
    }).then((res) => {
      setTimeout(() => {
        console.log(res);
      }, 0);
    });
  }
```
