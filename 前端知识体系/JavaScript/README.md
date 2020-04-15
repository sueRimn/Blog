```JavaScript

```

## 语言特性

* 运行在客户端浏览器上
* 不用预编译，直接解析执行代码
* 弱类型语言，较为灵活
* 跨平台语言、脚本语言、解释性语言

## 数据类型
一共有七种数据类型，主要为两大类：值类型（基本类型）、引用类型
### 基本类型（原始值）

基本数据类型是按值访问的，可以操作保存在变量中的实际值

* 数值`number`：用于任何类型的数字，包括整数或浮点数
* 字符串`string`：字符串
* 布尔值`boolean`：逻辑类型，`true`和`false`
* 空值`null`：未知的值
* 无定义`undefined`：未定义的值
* `symbol`：创建对象的唯一标识符（`ES6`新增）
### 引用类型（对象值）
* 对象`object`：复杂的数据结构
* 数组
* 函数
### 基本数据类型和引用类型的区别

* 基本数据类型的变量的值是不可变的，当变量重新赋值后并不是变量的值改变了，变量名只是指向变量的一个指针，所以只是指针的指向改变了，该变量是不变的，但是引用类型可以改变
* 基本数据类型不可以添加属性和方法，引用类型可以
* 基本数据类型的赋值是简单赋值，引用类型的赋值是对象引用
* 基本数据类型的比较是值的比较，引用类型的比较是对象内存地址的比较
* 基本数据类型的值存放在栈区，引用类型的值保存在栈区和堆区

## NaN的理解

`NaN`是JS的特殊值，表示非数字（`Not a Number`），`NaN`不是数字，但是数据类型是数字，它不等于任何值，包括自身，在布尔运算时被当做`false`，`NaN`与任何数运算得到的结果都是`NaN`

## JS的作用域类型

JS采用的是词法作用域，也就是静态作用域，所以函数的作用域在函数定义的时候就决定了

* 词法作用域
* 函数作用域
* 块级作用域

## undefined与null的区别

`null`表示没有对象，`undefined`表示缺少值，就是此处应该有一个值但是还没有定义

```javascript
undefined == null // true
undefined === null // false
!undefined == !null // true
!undefined === !null // true
```

> 在做==比较时，不同类型的数据会先转换成一致后在做比较，===中如果类型不一致就直接返回false，一致的才会比较

## instance操作符
用来比较两个操作数的构造函数。

## 类型判断

首先判断是否为`null`，之后用`typeof`判断类型，如果是`object`的话，再用`Array.isArray`判断是否为数组，如果是数字的话用`isNaN`判断是否是`NaN`即可

`typeof()、instanceof、Object.prototype.toString.call()`

## 隐式转换
显示转换主要涉及三种转换：
* 值->原始值：`ToPrimitive()`
* 值->数字：`ToNumber()`
* 值->字符串：`ToString()`

**内置类型的构造函数隐式转换**

* 转换为字符串：`''+10==='10'//true` 将一个值加上空字符串可以转换为字符串类型
* 转化为数字：`+'10' === 10//true` 使用一元的加号操作符，把字符串转换为数字
* 转换为布尔值：使用否操作符两次
```JavaScript
!!'foo';   // true
!!'';      // false
!!'0';     // true
!!'1';     // true
!!'-1'     // true
!!{};      // true
!!true;    // true
```
## 运算符
* 算术运算符：加减乘除（`+-*/`）、指数（`**`）、余数（`%`）、自增(`++`)、自减（`--`）、数值、负数值
* 比较运算符：大于(`>`)、小于(`<`)、大于或等于(`>=`)、小于或等于(`<=`)、相等(`==`)、严格相等(`===`)、不相等(`!=`)、严格不相等(`!==`)
* 布尔运算符：取反(`!`)、且(`&&`)、或(`||`)、三元(`? :`)
* 二进制位运算符
## 数组`Array`
> 对象允许存储键值化的集合,可以存储任何类型的元素
### 方法
#### 添加/移除元素 `pop/push`、`shift/unshift`（改变原数组）
* `unshift`：在数组首部添加一个元素
* `shift`：取出并返回第一个元素
* `push`：在末尾添加一个元素
* `pop`:取出并返回最后一个元素
#### 添加/删除/插入元素`splice()`（改变原数组）/`slice()`
`arr.splice(index[], deleteCount, elem1, ..., elemN])`
* 从索引位置删除几个元素，并用另外的元素替换它们。
* 将 `deleteCoun`t 设置为 0，`splice` 方法就能够插入元素而不用删除
`arr.slice(start, end)`
* 从所有元素的开始索引 "start" 复制到 "end" (不包括 "end") 返回一个新的数组
#### 合并数组`concat()`
`arr.concat(arg1, arg2...)`，浅拷贝

#### 查询数组 
* 1.`indexOf/lastIndexOf` 和 `includes`
  * `arr.indexOf(item, from)` 从索引 `from` 查询 `item`，如果找到返回索引，否则返回 `-1`
  * `arr.lastIndexOf(item, from)` 和上面相同，只是从尾部开始查询
  * `arr.includes(item, from)` 从索引 `from` 查询 `item`，如果找到则返回 `true`
* 2.`find` 和 `findIndex`
  
  ```javascript
  let result = arr.find(function(item, index, array) {
  // 如果查询到返回 true
  });
  ```
  * `item`是元素
  * `index`是它的索引
  * `array`是数组本身
  

返回`true`停止查询，返回`item`，没有查询到结果则返回`undefined`。

`arr.findIndex`与之一样，不过返回的是元素索引而不是元素本身。

* 3.`some`和`every`
  * `some`：查到一项`true`全为`true`
  * `every`：查到一项`false`全为`false`

#### 过滤数组`filter()`
> 返回所有匹配元素组成的数组
```javascript
let results = arr.filter(function(item, index, array) {
  // 在元素通过过滤器时返回 true
});
```
#### 转换数组
* `map()`
> 迭代并返回数组中每个元素调用函数并返回符合结果的数组
```javascript
let result = arr.map(function(item, index, array) {
  // 返回新值而不是当前元素
})
```
* `sort()`:数组排序，会改变原数组
* `reverse()`:颠倒数组，然后返回它
#### 迭代`forEach`
> 允许为数组的每个元素运行一个函数
```javascript
arr.forEach(function(item, index, array) {
  // ... do something with item
});
```
#### 遍历数组
* 老方法for循环：`for(let i=0; i<arr.length; i++)`
* `for...of`：不能获取当前元素的索引,只能访问 `items`
* `for...in`（不推荐）
* `forEach`
* `map`：遍历数组返回新数组
### 数组去重

* `indexOf`循环去重

```javascript
// 方法1：
function unique(arr) {
    if (!Array.isArray(arr)) {
        return
    }
    let res = []
    for (let i = 0; i < arr.length; i++) {
        if (res.indexOf(arr[i] === -1)) {
            res.push(arr[i])
        }
    }
    return res
}

// 方法2：
function unique(arr) {
    if (!Array.isArray(arr)) {
        return
    }
    return Array.prototype.filter.call(arr, (item, index) => {
        return arr.indexOf(item) === index
    })
}
```

* `set`与解构赋值去重（推荐）：Set函数可以接受一个数组（或类数组对象）作为参数来初始化，利用该特性能做到给数组去重

```javascript
function unique(arr) {
    if (!Array.isArray(arr)) {
        return
    }
    return [...new Set[arr]]
}
```

* `Array.from`与`Set`去重

```javascript
function unique(arr) {
    if (!Array.isArray(arr)) {
        return
    }
    return Array.from(new Set(arr))
}
```

* 相邻元素去重：根据排序后的结果进行遍历及相邻元素比对，如果相等则跳过改元素，直到遍历结束

```javascript
function unique(arr) {
    if (!Array.isArray(arr)) {
        return
    }
    arr = arr.sort()
    let res = []
    for (let i = 0; i < arr.length; i++) {
        if (arr[i] !== arr[i-1]) {
            res.push(arr[i])
        }
    }
    return res
}
```

* 双循环去重（不推荐）

```javascript
function unique(arr) {
    if (!Array.isArray(arr)) {
        console.log('type error!')
        return
    }
    let res = [arr[0]]
    for (let i = 1; i < arr.length; i++) {
        let flag = true
        for (let j = 0; j < res.length; j++) {
            if (arr[i] === res[j]) {
                flag = false;
                break
            }
        }
        if (flag) {
            res.push(arr[i])
        }
    }
    return res
}
```

* 对象属性去重：创建空对象，遍历数组，将数组中的值设为对象的属性，并给该属性赋初始值1，每出现一次，对应的属性值增加1，这样，属性值对应的就是该元素出现的次数了

```javascript
function unique(arr) {
    if (!Array.isArray(arr)) {
        console.log('type error!')
        return
    }
    let res = [], obj = {}
    for (let i = 0; i < arr.length; i++) {
        if (!obj[arr[i]]) {
            res.push(arr[i])
            obj[arr[i]] = 1
        } else {
            obj[arr[i]]++
        }
    }
    return res
}
```

### 判断是否为数组

*  Array.isArray(arg)：需要考虑兼容

```javascript
if (!Array.isArray) {
    Array.isArray = function(arg) {
        return Object.prototype.toString.call(arg) = '[object Array]'
    }
}
```

* instanceof

```javascript
let ary = [1, 2, 3]
console.log(arr instanceof Array) // true
```

* 原型链方法

  ```javascript
  let ary = [1, 2, 3]
  console.log(ary._prototype_.constructor === Array) // true
  console.log(ary.constructor === Array)
  ```

## 对象(`Object`)
* 对象是用来存储键值对和属性的实体
* 对象是单个实物的抽象
### 属性的`getter`和`setter`
属性分为两种：数据属性和访问器属性。

当读取属性值时，用`getter`，当设置属性值时，使用`setter`。

### 对象操作
* 访问属性的方法
  * 点符号：`obj.property`
  * 方括号：`obj["property]`
* 删除属性：`delete obj.property`
* 检查属性是否存在：`key in obj`
* 遍历对象：`for(let key in obj)`
* 对象根据引用来复制或者赋值：变量存储的不是对象的“值”，而是值的“引用”（内存地址）。所以复制变量或者传递变量到方法中只是复制了对象的引用。 所有的引用操作（像增加，删除属性）都作用于同一个对象
* 深拷贝使用`Object.assign`或者[_.cloneDeep(obj)](https://lodash.com/docs#cloneDeep)
### new 操作符原理

* 创建一个类的实例：创建一个空对象obj，然后把这个空对象的__proto__设置为构造函数的`prototype`
* 初始化实例：构造函数被传入参数并调用，关键字`this`被设定指向该实例`obj`
* 返回实例`obj`

### 继承的实现方式

* 原型链继承：将父类的实例作为子类的原型，子类能够访问父类的原型属性和方法，不能多继承
* 构造继承：复制子类实例属性给子类（子类不能继承原型属性和方法），能实现多继承
* 实例继承：为父类实例添加新特性，作为子类实例返回，不能多继承
* 拷贝继承：支持多继承，但效率低
* 组合继承：调用父类构造继承父类的属性并保留传参优点，通过将父类实例作为子类原型，实现函数复用
* 寄生组合继承：通过寄生方式，砍掉父类实例属性

### 原型与原型链
#### 原型`prototype`
每个函数都有一个`prototype`属性，指向对象。
```JavaScript
function foo()
typeof foo.prototype; //Object
```
对于构造函数来说，生成实例的时候，该`prototype`属性会自动成为实例对象的原型

**作用**

 对象的属性和方法定义在原型上，那么所有实例对象都能共享，节省内存。
```javascript
function Person(name){
  this.name = name;
}
person.prototype.sex = 'male';

let jack = new Person('jack');
let mark = new Person('mark');

jack.sex;//'male'
mark.sex;//'male'
```
构造函数`Person`的`prototype`属性，就是实例对象`jack`和`mark`的原型对象，它俩都共享了该属性。

原型对象的属性不是实例对象自身的属性。修改原型对象时，会体现在所有实例对象上，因为原型对象是共享的。

如果实例对象自身有某个属性或方法，实例对象不会取原型对象上获取。
如果
#### 原型链
形成一个原型链：对象到原型，原型到原型...
* 所有对象都有自己的原型对象`prototype`
  * 对象可以充当其他对象的原型
  * 原型对象本身也是对象，所有它也有自己的原型
* 所有对象的原型最终上溯到`Object.prototype`，继承它的属性
* `Obejct.prototype`的原型是`null`，也就是没有自己的原型，原型链的尽头就是`null`
```JavaScript
Object.getPrototypeOf(Object.prototype)
// null
```
* 读取对象的某个属性时，`JavaScript` 引擎先寻找对象本身的属性，如果找不到，就到它的原型去找，如果还是找不到，就到原型的原型去找。如果直到最顶层的`Object.prototype`还是找不到，则返回`undefined`。
* 如果对象自身和它的原型，都定义了一个同名属性，那么优先读取对象自身的属性，这叫做“覆盖”（`overriding`）
#### 原型方法
* `Object.create()`:j接受一个对象作为参数，然后以它的原型返回一个实例对象，完全继承原型对象的属性
* `Object.setPrototypeOf`：为参数对象设置原型，返回该参数对象。接受两次参数，第一个为现有对象，第二个为原型对象
* `Object.getPrototypeOf`：返回参数对象的原型
* `Object.prototype.isPrototypeOf()`：判断该对象是否为参数对象的原型
* `Object.prototype._proto_`：返回该对象的原型。`_proto_`属性指向当前对象的原型对象，即构造函数的`prototypr`属性
```JavaScript
let Person = function(){};
let people = new Person();
Object.getPrototypeOf(people);//Person.prototype
```
* 获取实例对象`obj`的原型对象有三种方法：
  * `obj._proto_`
  * `obj.constructor.prototype`
  * `Objct.getPrototyprOf(obj)`
* `Object.getOwnPropertyNames`：返回一个数组，元素是参数对象本身所有属性的键名
* `Object.prototype.hasOwnProperty()`：返回布尔值，判断某个属性在对象自身还是在原型链上

#### `hasOwnPrototype`属性(推荐用于遍历对象属性)
* 判断一个对象是否包含自定义属性而不是原型链上的属性
* `hasOwnProperty` 是 `JavaScript` 中唯一一个处理属性但是不查找原型链的函数
#### `constructor`属性
* `prototype`对象有一个`constructor`属性，默认指向`prototype`对象所在的构造函数
```javascript
function Person(){};
Person.prototype.constructor;//Person
```
* `constructor`属性定义在`prototype`对象上面，意味着可以被所有实例对象继承
* 修改了原型对象，一般会同时修改`constructor`属性
#### `instanceof`运算符
* 返回一个实例，检验对象是否为某个构造函数的实例
* `instanceof`运算符只能用于对象，不适用原始类型的值
* 对于`undefined`和`null`，`instanceOf`运算符总是返回`false`
#### 对象拷贝
* 确保拷贝后的对象与元对象具有相同原型
* 确保拷贝后的对象与原对象具有相同的实例属性
```JavaScript
let copyObj = origin => {
 return Obejct.create(
  Object.getPrototypeOf(origin),
  Obejct.getOwnPropertyDescriptors(origin)
 );
}
```
#### `this`关键字

> this总是指向函数的直接调用者

**1.涵义**

* `this`在构造函数中，表示实例对象
* 不管在什么场合，它总是返回一个对象
* `this`就是属性或方法“当前”所在的对象
* `this`的指向是可变的，因为属性所在的当前对象可变
* `this`的实质就是在函数体内部，指代函数当前运行环境
 * 在全局环境执行，`this`指向全局环境
 * 在`obj`环境执行，指向`obj`
```JavaScript
function Person(){
 return "我是" + this.name;
}
let jack = {
 name:"jack",
 resume:Person
};
let mark = {
  name:"mark",
  resume:Person
 };
 jack.resume();//"我是jack"
 mark.resume();//"我是mark"
```
**2.使用场合**
* (1)全局环境：只要全局环境下使用`this`，它指向的是顶层对象`window`
* (2)构造函数：指向实例对象
* (3)对象的方法：指向方法运行时所在的对象
* (4)显示设置`this`：当使用`Function.prototype`的`call`/`apply`方法时，函数内的`ths`·会被显示设置为函数调用的第一个参数

**3.绑定this的方法**
* `call()`：可以指定函数内部`this`的指向（即函数执行时所在的作用域），函数在指定作用域中调用该函数，
  * 其参数是一个对象，为空时，`null`和`undefined`传入全局对象
  * 其参数是一个原始值，会自动转为对应的包装对象，然后传入`call`方法
```JavaScript
let obj = {};
let person = function (){
 return this;
}
person();//window
person.call(obj);//obj
```
全局环境运行函数`person`时，`this`指向全局环境（`window`），`call`方法改变`this`指向对象`obj`
* `apply`：与`call`类型，唯一不同就是它接收一个数组作为函数执行时的参数
```JavaScript
function.apply(thisValue, [...arr]);
```
第一个参数是`this`指向的对象，为`null`或`undefined`时，传入全局对象。

第二个参数是数组，其元素依次作为参数传入原函数。
* ` bind()`：将函数体内的`this`绑定到某个对象，然后返回一个新函数
```JavaScript
let person = function(name, sex){
 return "我叫" + name + "," + sex;
}
let obj = {
 name:"jack"，
 sex:21
}
let new = person.bind(obj);
new();//我叫jack，21
```
**4.this使用注意点**
* 避免多层套用`this`
* 避免数组处理方法中使用`this`
* 避免回调函数中使用`this`
* 函数声明时的`this`只有等到调用时才会有值
* 箭头函数没有`this`，在箭头函数内部访问的都是来自外部的`this`值
## 函数
### 作用域与闭包
#### 作用域
JavaScript语言的作用域仅存在于函数范围中，作用域分为全局作用域和函数作用域。

作用域有上下级关系，嵌套的函数存在层层的上下级关系。

**作用域用处**

隔离变量，不同作用域下的同名变量不会有冲突。

**作用域链**

当函数创建变量，变量在函数作用域中取值时，查不到值就会向上级作用域去查找，直到全局作用域，这么一个过程形成的链条就叫作用域链。

### 闭包

闭包就是能够读取其他函数内部变量的函数。函数即闭包。

```javascript
function one () {
    let a = 1;
    function two () {
        console.log(a)
    }
    return two()
}
// 函数two就形成闭包
```

**闭包的特征**

* 函数内嵌套函数
* 内部函数可以引用外层的参数和变量
* 参数和变量不会受制于垃圾回收机制

**闭包的优缺点**

* 封装对象的私有的变量和方法
  * 优点：避免全局污染
  * 缺点：内存常驻，增加内存开销，使用不当造成内存泄漏
* 读取函数内部的变量，让变量始终保持在内存中，模仿块级作用域
* 保存外部函数的变量

**闭包的用处**

实现封装和缓存

## 模块化

### 优点

* 避免变量污染和命名冲突
* 提高代码复用性
* 提供可维护性
* 便于依赖关系管理

### 模块化方法

#### 函数封装

* 避免变量污染
* 但是外部可以随意修改内部成员，产生安全问题

```javascript
let module = {
	one: 1,
    two: 2,
    fn1 () {
        
    },
    fn2 () {
        
    }
}
```

#### 立即执行函数

* 模块外部无法修改内部没有暴露的变量、函数
* 但是会增加开销

```javascript
let myModule = (function(){
    let var1 = 1;
    let var2 = 2;
    
    function fn1(){
    
    } 
    
    function fn2(){
    
    }

return {
    fn1: fn1,
    fn2: fn2
};
})();

```

## 异步回调地狱

#### 解决方法

* promise
* generator：利用`Generator`函数的暂停执行的效果，可以把异步操作写在`yield`语句里面，等到调用`next`方法时再往后执行。
  * 分段执行，可以暂停
  * 可以控制阶段和每个阶段的返回值
  * 可以知道是否执行到结尾
* async/awit
  * `async `表示这是一个async函数，`await`只能用在这个函数里面
  * `await `表示在这里等待异步操作返回结果，再继续执行
  * `await `后一般是一个`promise`对象

## 事件流（事件模型）

事件流描述的是从页面中接收事件的顺序

DOM2级事件流包括下面几个阶段：

* 事件捕获阶段

* 处于目标阶段

* 事件冒泡阶段

在DOM标准事件模型中，是先捕获后冒泡：点击`DOM`节点时，事件传播顺序是事件捕获阶段，从上往下传播，然后到达事件目标节点，最后是冒泡阶段，从下往上传播。

DOM节点添加事件监听方法`addEventListener`，参数`capture`可以指定该监听是添加在事件捕获阶段还是事件冒泡阶段，为`false`是事件冒泡，为`true`是事件捕获，并非所有的事件都支持冒泡，比如`focus`、`blur`等等，我们可以通过`event.bubbles`来判断

但是如果要实现先冒泡后捕获的效果，对于同一个事件，监听捕获和冒泡，分别对应相应的处理函数，监听到捕获事件，先暂缓执行，直到冒泡事件被捕获后再执行捕获事件。

事件模型常用方法：

* `event.stopPropagation`：阻止捕获和冒泡阶段中当前事件的进一步传播
* `event.stopImmediatePropagetion`：阻止调用相同事件的其他侦听器
* `event.preventDefault`：取消该事件（假如事件是可取消的）而不停止事件的进一步传播
* `event.target`：指向触发事件的元素，在事件冒泡过程中这个值不变
* `event.currentTarget = this`：只有被点击时目标元素的`target`才会等于`currentTarget`

## 事件委托

在父元素层面阻止事件向子元素传播，也可代替子元素执行某些操作。

不在事件的发生地（直接dom）上设置监听函数，而是在其父元素上设置监听函数，通过事件冒泡，父元素可以监听到子元素上事件的触发，通过判断事件发生元素`DOM`的类型，来做出不同的响应

* 减少内存消耗，节约效率
* 动态绑定事件

## mouseover和mouseenter的区别

* `mouseover`：当鼠标移入元素或其子元素都会触发事件，所以有一个重复触发，冒泡的过程。对应的移除事件是`mouseout`
* `mouseenter`：当鼠标移除元素本身（不包含元素的子元素）会触发事件，也就是不会冒泡，对应的移除事件是`mouseleave`

## 图片懒加载和预加载

* 懒加载：主要目的是作为服务器的优化，减少请求数或延迟请求数
* 预加载：提前加载图片，当用户需要查看时直接从本地缓存中渲染

区别就在于预加载是提前加载，懒加载是迟缓加载或者不加载

## JS位置的区别

* `clientHeight`：表示的是可视区域的高度，不包含`border`和滚动条

* `offsetHeight`：表示可视区域的高度，包含了`border`和滚动条

* `scrollHeight`：表示了所有区域的高度，包含了因为滚动被隐藏的部分

* `clientTop`：表示边框`border`的厚度，在未指定的情况下一般为0

* `scrollTop`：滚动后被隐藏的高度，获取对象相对于由`offsetParent`属性指定的父坐标(css定位的元素或body元素)距离顶端的高度。

## 异步加载js 的方法

* `defer`：浏览器知道它将能够安全地读取文档的剩余部分而不用执行脚本，它将推迟对脚本的解释，直到文档已经显示给用户为止
* `async`
* 创建`script`标签，插入到`DOM`中

## JS节流（Throttling）和防抖（Debouncing）

### 节流

节流函数，只允许一个函数在一段时间内执行一次

```javascript
// 简单的节流函数
function throttle(func, wait, mustRun) {
    var timeout,
        startTime = new Date();
 
    return function() {
        var context = this,
            args = arguments,
            curTime = new Date();
 
        clearTimeout(timeout);
        // 如果达到了规定的触发时间间隔，触发 handler
        if(curTime - startTime >= mustRun){
            func.apply(context,args);
            startTime = curTime;
        // 没达到触发间隔，重新设定定时器
        }else{
            timeout = setTimeout(func, wait);
        }
    };
};
// 实际想绑定在 scroll 事件上的 handler
function realFunc(){
    console.log("Success");
}
// 采用了节流函数
window.addEventListener('scroll',throttle(realFunc,500,1000));
```

### 防抖

在一定时间内，规定事件被触发的次数

```javascript
// 简单的防抖动函数
function debounce(func, wait, immediate) {
    // 定时器变量
    var timeout;
    return function() {
        // 每次触发 scroll handler 时先清除定时器
        clearTimeout(timeout);
        // 指定 xx ms 后触发真正想进行的操作 handler
        timeout = setTimeout(func, wait);
    };
};
 
// 实际想绑定在 scroll 事件上的 handler
function realFunc(){
    console.log("Success");
}
 
// 采用了防抖动
window.addEventListener('scroll',debounce(realFunc,500));
// 没采用防抖动
window.addEventListener('scroll',realFunc);
```

## JS的垃圾回收机制

由于字符串、对象和数组没有固定大小，所有当他们的大小已知时，才能对他们进行动态的存储分配。态地分配了内存，最终都要释放这些内存以便再次使用，否则，`JavaScript`的解释器将会消耗完系统中所有可用的内存，造成系统崩溃。

### 垃圾回收方法

#### 标记清除

垃圾回收器会在运行的时候给存储在内存中的变量都加上标记，然后去掉环境变量中的变量以及被环境变量中的变量所引用的变量，删除所有被编辑的变量，删除变量无法在环境变量中被访问会被删除买最好垃圾回收器完成内存清除的工作，回收被占用的内存。

#### 计数引用

当对象被引用的次数为零时进行回收，但是循环引用时，两个对象都至少被引用了一次，因此导致内存泄漏

## eval是做什么的

将对应的字符串解析成JS并执行，非常耗性能（一次解析，一次执行）

## Commonjs、AMD和CMD的区别

模块是能实现特定功能的文件

* `Commonjs`：服务端的模块化，同步定义的模块化，每个模块都是单独的作用域，`modules.exports`模块输出，`require()`引入模块
* `AMD`：异步模块定义
  * 多个文件有依赖关系，被依赖的文件需要早于依赖它的文件加载到浏览器
  * 加载的时候浏览器会停止页面渲染，加载的文件越多，页面失去响应的时间越长
* ``

## 去除字符串首尾空格

```javascript

// 去除首尾空格
str.replace(/(^s*)|(\s*$)/g, "")
//去除左边空格
str.replace(/(^\s*)/g, "");
 
//去除右边空格
str.replace(/(\s*$)/g, "");
 
//引用JQ之后
$.trim(str);
//另一种写法
jQuery.trim(str);

 String.prototype.Trim = function(){
        return this.replace(/(^\s*)|(\s*$)/g, "");
 }
```

## JS实现跨域

* JSONP：通过动态创建`script`，再请求一个带参网址实现跨域通信
* document.domain` +` iframe`跨域：两个页面都通过js强制设置`document.domain`为基础主域，就实现了同域
* `location.hash` + `iframe`跨域：a欲与b跨域相互通信，通过中间页c来实现。 三个页面，不同域之间利用iframe的location.hash传值，相同域之间直接js访问来通信
* `postMessage`跨域：可以跨域操作的window属性之一
* `CORS`：服务端设置`Access-Control-Allow-Origin`即可，前端无须设置，若要带cookie请求，前后端都需要设置
* 代理跨域：启一个代理服务器，实现数据的转发

## Promise

`Promise`是一个对象，保存着未来要结束的事件，有两个特征：

* 对象的状态不受外部影响，`Promise`对象代表一个异步操作，有三种状态：`pending`进行中，`fulfilled`已成功，`rejected`已失败，只有异步操作的结果，才可以决定当前是哪一种状态，任何其他操作都无法改变这个状态
* 一旦状态改变，就不会再变，`promise`对象状态改变只有两种可能，从`pending`改到`fulfilled`或者从`pending`改到`rejected`，只要这两种情况发生，状态就凝固了，不会再改变，这个时候就称为定型`resolved`

```javascript
let promise = new Promise((resolve, reject) => {
    setTimeout(() => {
        resolve('ok')
    }, 1000)
})
// then接收两个函数,分别对应resolve和reject状态的回调,函数中接收实例化时传入的参数
promise.then((val) => {
    
}).catch(err => {
    
})

```

代码执行顺序：同步执行的代码-》`promise.then`->`settimeout`

## 深浅拷贝的区别和实现

### 深拷贝

完全拷贝一个对象，即使嵌套了对象，两者也会互相分离，修改一个对象的属性，不会影响另一个

```javascript
// 原理是JOSN对象中的stringify可以把一个js对象序列化为一个JSON字符串，parse可以把JSON字符串反序列化为一个js对象，通过这两个方法，也可以实现对象的深复制
// 此方法不能拷贝函数
let arr = [1, true, ['a', 'b'], {one: 1}]
let new_arr = JSON.parse(JSON.stringify(arr))


// 判断属性值类型，如果是对象就使用递归调用
let deepCopy = obj => {
    if (typeof obj !== 'object') return 
    let newObj = obj instanceof Array ? [] : {}
    for (let key in obj) {
        if (obj.hasOwnProperty(key)) {
            newObj[key] = typeof obj[key] ==='object' ? deepCopy(obj[key]) : obj[key]
        }
    }
    return newObj
}
```

### 浅拷贝

当数组是基本类型时，一般用slice`、`concat`方法返回一个新数组的特性可以实现拷贝，但是如果数组嵌套了对象或者数组，用`concat`方法克隆就不完整，之后拷贝到对象或者数组的引用，对新旧数组进行修改，两者都会发生变化，这种复制引用的方法就叫浅拷贝

```javascript

```

## JS加载阻塞解决方案

* 指定`script`标签的`async`属性
* 如果async="async"，脚本相对于页面的其余部分异步地执行（当页面继续进行解析时，脚本将被执行）
* 如果async="async"，脚本相对于页面的其余部分异步地执行（当页面继续进行解析时，脚本将被执行）

## 设计模式

* 单例模式：核心结构中值包含一个单例的特殊类，一个类只有一个实例，即一个类只有一个对象实例
* 工厂模式：在创建对象时不会对客户端暴露创建逻辑，并且是通过使用一个共同的接口来指向新创建的对象
* 发布订阅模式：发布订阅是一种[消息](https://baike.baidu.com/item/消息)[范式](https://baike.baidu.com/item/范式)，消息的发送者（称为发布者）不会将消息直接发送给特定的接收者（称为订阅者）。而是将发布的消息分为不同的类别，无需了解哪些订阅者（如果有的话）可能存在。同样的，订阅者可以表达对一个或多个类别的兴趣，只接收感兴趣的消息，无需了解哪些发布者（如果有的话）存在
* 装饰者模式：在不改变元对象的基础上，对这个对象进行包装和拓展（包括添加属性和方法），从而使这个对象可以有更复杂的功能

