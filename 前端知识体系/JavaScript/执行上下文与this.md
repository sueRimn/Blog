
`this`，即当前执行代码的环境对象。

换句话说，执行的每个`JavaScript`函数都有对其当前执行上下文的引用，称为`this`。

### 一、执行上下文

执行上下文代表函数的调用方式，大多数情况下，函数的调用方式决定了`this`的值。即，执行上下文决定了`this`的值。

要理解这个关键字`this`，**只需要`this`取决于函数的调用方式，跟函数声明以及声明位置没关系**。

比如看下面这段代码：

```javascript
function person() {
    console.log(this.name);
}

let name = "sueRimn";
let one = {name: "八至", age: 22};
let two = {name: "小九", age: 22};

person();     // "sueRimn"
one.person(); // "八至"
two.person(); // "小九"
```

代码中函数`person()`的执行任务是打印出`this.name`，即打印当前执行上下文的`name`属性的值。

当函数`person()`没有被调用时，执行上下文也没有指定，默认为当前全局下，`this.name`就是全局变量的值`"sueRimn"`。

而`one.person()`是代表函数`person()`被`one`调用，此时函数的执行上下文是`one`，即执行上下文`this.name`的值就是`one.name`的值，`two.person()`也是相同道理。

> **注意**：
>
> * `this`不能在函数执行期间被赋值
> * 函数每次被调用时`this`的值不同

### 二、`this`关键字的绑定规则

`this`的绑定分为：

* 默认绑定与隐式绑定
* 显示绑定与固定绑定

#### 1、默认绑定和隐式绑定

* 严格模式下：`this`的默认值是`undefined`
* 非严格模式下：`this`默认指向全局对象
* 在函数内部，`this`的值取决于函数被调用的方式
* 当有一个作为方法调用的对象属性时，该对象是该方法的`this`对象或执行上下文对象，这是`this`关键字的隐式绑定

**只要记住，在函数内部，`this`的值取决于函数被调用的方式，与函数声明时间、地点无关**。

```javascript
//在浏览器中， window对象同时也是全局对象
// this的默认绑定
console.log(this === window);//true
const AGE = 22;
console.log(window.AGE); // 22

this.b = "sueRimn";
console.log(window.b); // "sueRimn"
console.log(b); // "sueRimn"

// this的隐式绑定
let obj_1 = {
    name: "sueRimn",
    person: function () {
        console.log(this.name);
    }
}

let obj_2 = {name: "八至", person: obj_1.person};
let name = "小九";
let person = obj_1.person;

person(); // "小九"
obj_1.person(); // "sueRimn"
obj_2.person(); // "八至"
```

#### 2、显示绑定和固定绑定

要想把 `this` 的值从一个环境传到另一个，就要用 `call` 或者`apply` 方法。

**call()**

**call()**`方法使用一个指定的 `this` 值和单独给出的一个或多个参数来调用一个函数

```javascript
fun.call(thisArg, arg1, arg2, ...)
```

**apply()**

**apply()** 方法调用一个具有给定`this`值的函数，以及作为一个数组（或[类似数组对象](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Guide/Indexed_collections#Working_with_array-like_objects)）提供的参数

```javascript
func.apply(thisArg, [argsArray])
```

**区别**

* `call()` 方法接受的是**一个参数列表**
*  `apply()` 方法接受的是**一个包含多个参数的数组**

```java
let obj = {a: 'sue'};
let a = 'suerimn';
function whatThis(arg) {
    return this.a;//this的值取决于函数的调用方式
}

whatThis();// 'suerimn'
whatThis.call(obj);//'sue'
whatThis.apply(obj);//'sue'
```

如果我们使用`call()`和`apply()`方法调用函数，需要把自己的第一个参数作为执行上下文。这就是`this`关键字的绑定。

> 注意：在显示绑定或固定绑定中，无论在哪里调用，可以强制`this`对象始终相同

```javascript
function add(c, d) {
    return this.a + this.b + c + d;
}

let o = {a: 1, b: 3};
//第一个参数作为this使用的对象
//后续参数作为参数传递给函数调用
add.call(o, 2, 3);//1 + 3 + 2 + 3 = 9

//第一个参数作为this使用的对象
//第二个参数是一个数组，数组里的元素用作函数调用时的参数
add.apply(o, [10, 20]);//1 + 3 + 10 + 20 = 34
```

上面代码中，`add`使用`call()`方法调用将执行上下文对象`o`作为第一个参数传递，将`o`分配给`this`对象并返回。这称为`this`关键字的显示绑定。

### 三、设置`this`值的方式

#### （1）`call()`或`apply()`

上文中已经提及。

#### （2）`bind`方法

ES5引入了[bind](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Function/bind)方法来设置函数的`this`值，而不用考虑函数如何被调用的，调用`f.bind(someObject)`会创建一个与`f`具有相同函数体和作用域的函数，但是在这个新函数中，`this`将永久地被绑定到了`bind`的第一个参数，无论这个函数是如何被调用的。

```javascript
function f() {
    return this.a;
}

let g = f.bind({a: 'sueRimn'});
console.log(g()); // sueRimn

let h = g.bind({a: 'sueRimn'}); // bind只生效一次
console.log(h()); // sueRimn

let z = {a: 37, f: f, g: g, h: h};
console.log(z.f(), z.g(), z.h()); // 37 'sueRimn' 'sueRimn'
```

#### （3）箭头函数

这是`ES6`新引入的，在箭头函数中，`this`与封闭词法环境的`this`保持一致。在全局代码中，它将被设置为全局对象。

```javascript
let person = (name, age) => {
    console.log(name, age);
}
```



#### （4）`new`关键字

当函数作为对象里的方法被调用时，它们的`this`是调用该函数的对象。

任何函数前面的`new`关键字都会将函数调用转换为构造函数调用，并且当`new`关键字放在函数前面时会发生这些事情：

* 创建一个全新的空对象
* 新的空对象链接到该函数的`prototype`属性
* 将相同的新空对象绑定为该函数调用的执行上下文
* 如果该函数没有返回任何内容，则隐式返回此对象

```javascript
function person() {
    let name = "sueRimn";
    this.age = 22;
    console.log(this.name + "" + age); // undefined 23
}

let name = "八至";
let age = 23;

obj = new person();
console.log(obj.age); // 22
```

在上面的代码中，使用`new`关键字调用`person`函数，它创建了一个新对象链接到函数原型链上，并绑定到该对象函数返回的对象上。

`this.name`的

```javascript
let fn = {
    prop: 37,
    f: function () {
        return this.prop;
    }
};

console.log(fn.f());//37
```

### 四、`this`关键字绑定的顺序

1. 检查函数是否使用`new`关键字调用
2. 检查函数是否使用`call()`或者`apply()`调用，因为这意味着显示绑定
3. 检查函数是否通过上下文对象调用（隐式绑定）
4. 默认全局对象（在严格模式下未定义）

