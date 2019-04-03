# JavaScript
## 数据类型
一共有七种数据类型，主要为两大类：原始类型、对象类型
### 基础类型（原始值）
* 数值`number`：用于任何类型的数字，包括整数或浮点数
* 字符串`string`：字符串
* 布尔值`boolean`：逻辑类型，`true`和`false`
* 空值`null`：未知的值
* 无定义`undefined`：未定义的值
* `symbol`：创建对象的唯一标识符（`ES6`新增）
### 复杂类型（对象值）
* 对象`object`：复杂的数据结构
### instance操作符
用来比较两个操作数的构造函数。

### 隐式转换
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
#### 添加/移除元素 `pop/push`、`shift/unshift`
* `unshift`：在数组首部添加一个元素
* `shift`：取出并返回第一个元素
* `push`：在末尾添加一个元素
* `pop`:取出并返回最后一个元素
#### 添加/删除/插入元素`splice()`/`slice()`
`arr.splice(index[], deleteCount, elem1, ..., elemN])`
* 从索引位置删除几个元素，并用另外的元素替换它们。
* 将 `deleteCoun`t 设置为 0，`splice` 方法就能够插入元素而不用删除
`arr.slice(start, end)`
* 从所有元素的开始索引 "start" 复制到 "end" (不包括 "end") 返回一个新的数组
#### 合并数组`concat()`
`arr.concat(arg1, arg2...)`
#### 查询数组 `sort()`
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
* `sort()`:数组排序
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
JavaScript语言的作用域仅存在于函数范围中



