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
### 隐式转换
主要涉及三种转换：
* 值->原始值：`ToPrimitive()`
* 值->数字：`ToNumber()`
* 值->字符串：`ToString()`
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
### 过滤数组`filter()`
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
#### `this`关键字

### 构造函数

