# 定时器
`JavaScript` 提供定时执行代码的功能，叫做定时器（`timer`），主要由`setTimeout()`和`setInterval()`这两个函数来完成。它们向任务队列添加定时任务。
## setTimeout()
`setTimeout`函数用来指定某个函数或某段代码，在多少毫秒之后执行。它返回一个整数，表示定时器的编号，以后可以用来取消这个定时器。
* 第一个参数`func|code`是将要推迟执行的函数名或者一段代码，如果推迟执行的是函数，就直接将函数名，作为`setTimeout`的参数
* 第二个参数`delay`是推迟执行的毫秒数，如果省略，则默认为`0`

```javascript
var timerId = setTimeout(func|code, delay);
```
* 除了前两个参数，`setTimeout`还允许更多的参数。它们将依次传入推迟执行的函数（回调函数）
```javascript
setTimeout(function (a,b) {
  console.log(a + b);
}, 1000, 1, 1);
```
上面代码中，`setTimeout`共有4个参数。最后那两个参数，将在1000毫秒之后回调函数执行时，作为回调函数的参数。

还有一个需要注意的地方，如果回调函数是对象的方法，那么`setTimeout`使得方法内部的`this`关键字指向全局环境，而不是定义时所在的那个对象。
## setInterval()

`setInterval`函数的用法与`setTimeout`完全一致，区别仅仅在于`setInterval`指定某个任务每隔一段时间就执行一次，也就是无限次的定时执行。

```javascript
var i = 1
var timer = setInterval(function() {
  console.log(2);
}, 1000)
```
与`setTimeout`一样，除了前两个参数，`setInterval`方法还可以接受更多的参数，它们会传入回调函数。

`setInterval`指定的是“开始执行”之间的间隔，并不考虑每次任务执行本身所消耗的时间。因此实际上，两次执行之间的间隔会小于指定的时间。

为了确保两次执行之间有固定的间隔，可以不用`setInterval`，而是每次执行结束后，使用`setTimeout`指定下一次执行的具体时间。

```javascript
var i = 1;
var timer = setTimeout(function f() {
  // ...
  timer = setTimeout(f, 2000);
}, 2000);
```
## clearTimeout()，clearInterval()

`setTimeout`和`setInterval`函数，都返回一个整数值，表示计数器编号。将该整数传入`clearTimeout`和`clearInterval`函数，就可以取消对应的定时器。

```javascript
var id1 = setTimeout(f, 1000);
var id2 = setInterval(f, 1000);

clearTimeout(id1);
clearInterval(id2);
```
# Promise 对象
## 概述

Promise 对象是 JavaScript 的异步操作解决方案，为异步操作提供统一接口。它起到代理作用（proxy），充当异步操作与回调函数之间的中介，使得异步操作具备同步操作的接口。Promise 可以让异步操作写起来，就像在写同步操作的流程，而不必一层层地嵌套回调函数。

首先，Promise 是一个对象，也是一个构造函数。

```javascript
function f1(resolve, reject) {
  // 异步代码...
}

var p1 = new Promise(f1);
```

上面代码中，`Promise`构造函数接受一个回调函数`f1`作为参数，`f1`里面是异步操作的代码。然后，返回的`p1`就是一个 Promise 实例。

Promise 的设计思想是，所有异步任务都返回一个 Promise 实例。Promise 实例有一个`then`方法，用来指定下一步的回调函数。

```javascript
var p1 = new Promise(f1);
p1.then(f2);
```

上面代码中，`f1`的异步操作执行完成，就会执行`f2`。
## Promise 对象的状态
`Promise` 实例具有三种状态：

- `pending`：异步操作未完成，正在执行
- `fulfilled`：异步操作成功
- `rejected`：异步操作失败
- `settled`：`Promise`处于 `fulfilled` 或 `rejected `二者中的任意一个状态, 不会是 `pending`

上面状态里面，`fulfilled`和`rejected`合在一起称为`resolved`（已定型）。

状态的变化途径只有两种。

- 从“未完成”到“成功”
- 从“未完成”到“失败”

一旦状态发生变化，就凝固了，不会再有新的状态变化。这也是 Promise 这个名字的由来，它的英语意思是“承诺”，一旦承诺成效，就不得再改变了。这也意味着，Promise 实例的状态变化只可能发生一次。

因此，Promise 的最终结果只有两种。

- 异步操作成功，Promise 实例传回一个值（value），状态变为`fulfilled`。
- 异步操作失败，Promise 实例抛出一个错误（error），状态变为`rejected`。
## Promise 属性
* `Promise.length`：其值总是1（构造器参数的数目）
* `Promise.prototype`:表示`Promise`构造器的原型
## Promise 方法
### Promise.all(iterable)
* 返回一个新的`promise`对象，该对象在`iterable`参数对象里所有的`promise`对象都成功的时候才会触发成功
* 触发成功状态以后，会把一个包含`iterable`里所有`promise`返回值的数组作为成功回调的返回值，顺序跟`iterable`的顺序保持一致
* 触发了失败状态，它会把`iterable`里第一个触发失败的`promise`对象的错误信息作为它的失败错误信息
### Promise.race(iterable)
当iterable参数里的任意一个子promise被成功或失败后，父promise马上也会用子promise的成功返回值或失败详情作为参数调用父promise绑定的相应句柄，并返回该promise对象
### Promise.reject(reason)
返回一个状态为失败的Promise对象，并将给定的失败信息传递给对应的处理方法
### Promise.resolve(value)
* 返回一个状态由给定value决定的Promise对象
* 如果该值是thenable(即，带有then方法的对象)，返回的Promise对象的最终状态由then方法执行决定
* 否则(该value为空，基本类型或者不带then方法的对象),返回的Promise对象状态为fulfilled，并且将该value传递给对应的then方法
## Promise 原型
### 属性
Promise.prototype.constructor：返回被创建的实例函数，默认为`Promise`函数
### 方法
#### Promise.prototype.catch(onRejected)
添加一个拒绝(`rejection`) 回调到当前 `promise`, 返回一个新的`promise`。

当这个回调函数被调用，新 promise 将以它的返回值来resolve，否则如果当前promise 进入fulfilled状态，则以当前promise的完成结果作为新promise的完成结果。
#### Promise.prototype.then(onFulfilled, omRejected)
添加解决(`fulfillment`)和拒绝(`rejection`)回调到当前 `promise`, 返回一个新的 `promise`, 将以回调的返回值来`resolve`。
#### Promise.prototype.finally(onFinally)
添加一个事件处理回调于当前`promise`对象，并且在原`promise`对象解析完毕后，返回一个新的`promise`对象。

回调会在当前`promise`运行完毕后被调用，无论当前`promise`的状态是完成(`fulfilled`)还是失败(`rejected`)。
## Promise 构造函数

JavaScript 提供原生的`Promise`构造函数，用来生成 Promise 实例。

异步任务顺利完成且返回结果值时，会调用 resolve 函数；而当异步任务失败且返回失败原因（通常是一个错误对象）时，会调用reject 函数。
```javascript
var promise = new Promise((resolve, reject) => {
  // ...

  if (/* 异步操作成功 */){
    resolve(value);
  } else { /* 异步操作失败 */
    reject(new Error());
  }
});
```
`resolve`函数的作用是，将`Promise`实例的状态从“未完成”变为“成功”（即从`pending`变为`fulfilled`），在异步操作成功时调用，并将异步操作的结果，作为参数传递出去。

`reject`函数的作用是，将`Promise`实例的状态从“未完成”变为“失败”（即从`pending`变为`rejected`），在异步操作失败时调用，并将异步操作报出的错误，作为参数传递出去。
## Promise.prototype.then()
Promise 实例的`then`方法，用来添加回调函数。

`then`方法可以接受两个回调函数，第一个是异步操作成功时（变为`fulfilled`状态）的回调函数，第二个是异步操作失败（变为`rejected`）时的回调函数（该参数可以省略）。一旦状态改变，就调用相应的回调函数。

```javascript
var p1 = new Promise(function (resolve, reject) {
  resolve('成功');
});
p1.then(console.log, console.error);
// "成功"

var p2 = new Promise(function (resolve, reject) {
  reject(new Error('失败'));
});
p2.then(console.log, console.error);
// Error: 失败
```

上面代码中，`p1`和`p2`都是Promise 实例，它们的`then`方法绑定两个回调函数：成功时的回调函数`console.log`，失败时的回调函数`console.error`（可以省略）。`p1`的状态变为成功，`p2`的状态变为失败，对应的回调函数会收到异步操作传回的值，然后在控制台输出。

`then`方法可以链式使用。

```javascript
p1
  .then(step1)
  .then(step2)
  .then(step3)
  .then(
    console.log,
    console.error
  );
```

上面代码中，`p1`后面有四个`then`，意味依次有四个回调函数。只要前一步的状态变为`fulfilled`，就会依次执行紧跟在后面的回调函数。

最后一个`then`方法，回调函数是`console.log`和`console.error`，用法上有一点重要的区别。`console.log`只显示`step3`的返回值，而`console.error`可以显示`p1`、`step1`、`step2`、`step3`之中任意一个发生的错误。举例来说，如果`step1`的状态变为`rejected`，那么`step2`和`step3`都不会执行了（因为它们是`resolved`的回调函数）。Promise 开始寻找，接下来第一个为`rejected`的回调函数，在上面代码中是`console.error`。这就是说，Promise 对象的报错具有传递性。

## then() 用法辨析

Promise 的用法，简单说就是一句话：使用`then`方法添加回调函数。但是，不同的写法有一些细微的差别，请看下面四种写法，它们的差别在哪里？

```javascript
// 写法一
f1().then(function () {
  return f2();
});

// 写法二
f1().then(function () {
  f2();
});

// 写法三
f1().then(f2());

// 写法四
f1().then(f2);
```

为了便于讲解，下面这四种写法都再用`then`方法接一个回调函数`f3`。写法一的`f3`回调函数的参数，是`f2`函数的运行结果。

```javascript
f1().then(function () {
  return f2();
}).then(f3);
```

写法二的`f3`回调函数的参数是`undefined`。

```javascript
f1().then(function () {
  f2();
  return;
}).then(f3);
```

写法三的`f3`回调函数的参数，是`f2`函数返回的函数的运行结果。

```javascript
f1().then(f2())
  .then(f3);
```

写法四与写法一只有一个差别，那就是`f2`会接收到`f1()`返回的结果。

```javascript
f1().then(f2)
  .then(f3);
```

## 实例：图片加载

下面是使用 Promise 完成图片的加载。

```javascript
var preloadImage = function (path) {
  return new Promise(function (resolve, reject) {
    var image = new Image();
    image.onload  = resolve;
    image.onerror = reject;
    image.src = path;
  });
};
```

上面的`preloadImage`函数用法如下。

```javascript
preloadImage('https://example.com/my.jpg')
  .then(function (e) { document.body.append(e.target) })
  .then(function () { console.log('加载成功') })
```

## 小结

Promise 的优点在于，让回调函数变成了规范的链式写法，程序流程可以看得很清楚。它有一整套接口，可以实现许多强大的功能，比如同时执行多个异步操作，等到它们的状态都改变以后，再执行一个回调函数；再比如，为多个回调函数中抛出的错误，统一指定处理方法等等。

而且，Promise 还有一个传统写法没有的好处：它的状态一旦改变，无论何时查询，都能得到这个状态。这意味着，无论何时为 Promise 实例添加回调函数，该函数都能正确执行。所以，你不用担心是否错过了某个事件或信号。如果是传统写法，通过监听事件来执行回调函数，一旦错过了事件，再添加回调函数是不会执行的。

Promise 的缺点是，编写的难度比传统写法高，而且阅读代码也不是一眼可以看懂。你只会看到一堆`then`，必须自己在`then`的回调函数里面理清逻辑。
