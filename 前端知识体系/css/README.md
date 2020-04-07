
# CSS
## CSS常用属性
## 盒模型
> 盒模型（`box model`）是元素大小的呈现方式。盒模型默认的值是`content-box`，新增的值是`padding-box`和border-box`

盒模型分为标准盒模型和怪异盒模型（IE模型）

```css
box-sizing: content-box; // 标准盒模型 
box-sizing: border-box; // 怪异盒模型
```


**盒模型计算元素宽高的区别如下**：

**content-box(默认)**：

width+margin+border+padding宽度

**padding-box**:

width = width(包含padding-left + padding-right) + border-top + border-bottom;

height = height(包含padding-top + padding-bottom) + border-top + border-bottom;

**border-box**:

width = width(包含padding-left + padding-right + border-left + border-right);

height = height(包含padding-top + padding-bottom + border-top + border-bottom);
## BFC
`BFC`就是块级格式上下文，是一个独立渲染区域，让处于`BFC`内部的元素和外部的元素相互隔离，使内部元素的定位不会相互影响

#### BFC的作用
* 防止`margin`重叠
* 清除内部浮动
#### 如何触发BFC
* display：inline-block | flex | inline-flex | table-cell | table-caption
* position:absolute | fixed
* float:left | right
* overflow:hidden | auto | scroll
## CSS常用选择器
* 通配符：`*`
* ID选择器：`#id`
* 类选择器：`.class`
* 元素选择器：`div`\`p`等
* 后代选择器：`a img`、`div p `等
* 伪类选择器：`a:hover`等
* 属性选择器：`input[type="text"]`等
* 子元素选择器：`li:firth-child`等
* 相邻兄弟选择器：`p + span`
* 群组选择器：`h1, h2, h3,...,h6`

**选择器优先级顺序**：`!important`> 行内样式 > ID选择器 > 类选择器 > 元素和伪元素 > 通配符 > 继承 > 默认
#### [返回顶部](#css)
## CSS单位
单位 | 描述
----- | -----
% | 百分比
`px` | 像素
`em` | 相对单位。相对于父元素计算，该元素的1em = 父元素px * 2
`rem` | 相对单位。相对于根元素`html`，该元素的1rem = html的px * 2
 `rpx` | 微信小程序的相对单位，1rpx = 屏幕宽度/750px
## CSS定位
#### 1.display属性
将元素分为块级元素（`block`）和内联级元素（`inline`）。块级元素可以设置宽度，独占一行。内联元素宽度由内容决定，与其他元素并列占一行。<br>常见块级元素有：`div, h1-h6, ui, li, ol, dl, dd, dt`<br>常见内联元素有：`span, a, em`

**block**：独占一行，宽高可以设置，默认宽度由父容器决定，默认高度由内容决定

**inline**：宽高由内容决定，与其他元素共占一行

**inline-block**：宽度可设置，但是与其他元素共占一行

**table-cell**:让标签元素以表格单元格的形式呈现

#### 2.position属性
元素在也页面中的布局遵守文档流的方式，默认定位属性是`static`。如果元素被定位了，它的`top`\`left`\`bottom`\`left`值就会生效，能设置定位属性`relative`\`absolute`\`fixed`。被定位的元素层级（`z-index`）会被提高。

**static(静态定位)**：

HTML元素定位默认是静态的，不受顶部、底部、左部、右部影响，总是根据页面正常流定位。

**relative(相对定位)**：

设置之后，通过修改`top left bottom right`值，元素会在自身文档流里偏离位置，但是其他元素不会调整位置来弥补它偏离后剩下的空隙。

**absolute(绝对定位)**：

设置之后元素脱离文档流，其他元素会调整位置弥补它偏离了后留下的空隙。

元素偏离是相当于离它最近的设置了定位属性的元素（`position`的值不为`static`）d的位置进行偏离。

如果该元素为块级元素，那么它设置定位属性，宽度是由内容撑开的。因为默认文档流中（`position`为`static`）块级元素如果没有设置宽度属性，会自动填满整行。

**fixed(固定定位)**：

设置之后，元素相对的偏移的参考可视窗口的，即使在页面滚动的情况下，也会在固定位置。

**sticky(粘性定位)**：

根据用户的滚动位置定位
#### 3.z-index重叠顺序
## css溢出overflow
`overflow`属性具有以下属性值：
* `visible`：默认。溢出不会被截断，内容呈现溢出的部分
* `hidden`: 溢出被截断，隐藏
* `scroll`：添加滚动条显示溢出部分内容
* `auto`：和`scroll`类型，只是在需要时才会添加滚动条
#### [返回顶部](#css)
## CSS浮动float
#### 1.什么是浮动
浮动元素会脱离文档流，按照指定方向移动，遇到父级边界或者相邻的浮动元素停止。
#### 2.浮动的作用
* 设置文字环绕
* 使元素宽度由内容填充　页面布局
＊　多个元素内联排列
#### 3.注意
如果浮动元素高度大于父级容器，设置父级容器的`overflow:auto`，使其自动充满，防止父级高度塌陷。
#### 4.清除浮动的原因
当容器的高度`auto`，并且内有浮动元素，容器的高度不能自动撑开以适应内容的高度，是的内容溢出到容器外部，从而影响布局造成浮动溢出，所以要进行CSS清除浮动。
#### 5.清除浮动的方法
** 使用带clear属性的空元素**：
```html
<div class="box-wrapper">
    <div class="box"></div>
    <div class="box"></div>
    <div class="box"></div>
    <div style="clear:both;"></div>
</div>
```

**使用clearfix hack**：
```css
// 现代浏览器clearfix方案，不支持IE6/7
.clearfix:after {
    display: table;
    content: " ";
    clear: both;
}

// 全浏览器通用的clearfix方案
// 引入了zoom以支持IE6/7
.clearfix:after {
    display: table;
    content: " ";
    clear: both;
}
.clearfix{
    *zoom: 1;
}

// 全浏览器通用的clearfix方案
// 引入了zoom以支持IE6/7
// 同时加入:before以解决现代浏览器上边距折叠的问题
.clearfix:before,
.clearfix:after {
    display: table;
    content: " ";
}
.clearfix:after {
    clear: both;
}
.clearfix{
    *zoom: 1;
}
```

**BFC清除浮动**：

给父元素设置`overflow:hidden`实现简单的BFC清除浮动，但是这样元素阴影和下拉菜单会被截断。
#### [返回顶部](#css)
## css居中布局
[水平居中+垂直居中+水平垂直居中](https://github.com/sueRimn/Blog/tree/master/%E5%89%8D%E7%AB%AF%E7%9F%A5%E8%AF%86%E4%BD%93%E7%B3%BB/css/%E5%85%83%E7%B4%A0%E5%B1%85%E4%B8%AD)
## css常见对齐方式
**水平居中**：

* 1.块元素，使用`margin:0 auto`，设置元素的宽度
* 2.文本居中，使用`text-align:center`
* 3.图像居中，左右边距`auto`，`display: block`块元素显示
* 4.Flex：`display：flex; justify-content: center`
* 5.左右对齐：
   * 使用`position:absolute`
   * 使用`float`

**垂直居中**：

* 1.使用填充`padding`
* 2.使用`line-height`等于`height`
* 3.使用`position`和`transform`
* 4.`flex: display: flex; align-item: center`
## css伪类
伪类用于定义元素的特殊状态，用单冒号`:`连接
* 锚伪类：`:link` `:visited` `:hover` `:active`
* 孩子伪类：`:first-child`匹配的指定的元素是另一个元素的第一个孩子
## css伪元素
伪元素用于设置元素指定的部分样式，使用双冒号`::`连接,可多样结合
* `::first-line`：用于向文本的第一行添加特殊样式，只能用于块级元素
* `::dirst-letter`：用于向文本的第一个字母添加特殊样式，只能用于块级元素
* `::before`:用于元素内容之前插入某些内容
* `::after`：用于元素的内容之后插入某些内容
* `::selection`：用于元素匹配用户选择的部分
## CSS3的过渡、变换和动画
* `transition`:过渡
 * `transition-property`：过渡属性
 * `transition-duration`：过渡持续时间，单位为`s`
 * `transition-delay`：延迟时间
 * `transition-timing-function`：过渡类型 `ease` | `liner` | `ease-in` | `ease-out` | `ease-in-out` | `cubic-bezier`
* `transform`：变换
 * `skew`：倾斜
 * `scale`：缩放
 * `rotate`：旋转
 * `translate`：平移
* `animation`：动画
 * `animation-name`：动画名称
 * `animation-duration`：动画持续时间
 * `animation-iteration-count`：动画重复次数
 * `animation-direction`：动画执行完一次后方向的变化方式
 * `animation-timing-function`：变化的模式

 #### [返回顶部](#css)
## link和@import的区别
 区别  |  link | @import
--- | ---  | ------
功能 |  较多 | 只能用于加载`css`
加载顺序 | 解析`link`时，页面同步加载所引用的`css` | 页面加载完后才被加载
浏览器支持 |   | `IE5`以上
JS动态引入 | Yes | No
## 多行文本省略

```css
text {
    overflow : hidden;
    text-overflow: ellipsis;
    display: -webkit-box;
    -webkit-line-clamp: 3;
    -webkit-box-orient: vertical
}
```

## CSS规范与书写顺序

规范参考[京东前端开发规范](https://guide.aotu.io/docs/css/code.html)
### css代码规范
样式文件必须写上 `@charset` 规则，并且一定要在样式文件的第一行首个字符位置开始写，编码名用 `“UTF-8”`
### css代码风格
* 1.代码格式化：展开格式（Expanded）
```css
.jdc{
    display: block;
    width: 50px;
}
```
* 2.代码大小写：样式选择器，属性名，属性值关键字全部使用小写字母书写，属性字符串允许使用大小写
* 3.选择器：
 * 尽量少用通用选择器 `*`
 * 不使用ID选择器
 * 不使用无具体语义定义的标签选择器
* 4.代码缩进：使用四个空格
* 5.分号：每个属性声明末尾都要加分号
* 6.代码易读性：左括号与类名之间一个空格，冒号与属性值之间一个空格，逗号之后一个空格，单个css选择器开启新行,不要为 0 指明单位
属性值十六进制数值能用简写的尽量用简写

```css
.jdc, 
.jdc_logo, 
.jdc_hd {
    color: #ff0;
}
```
* 7.属性值引号：属性值需要用到引号时，统一使用单引号
* 8.属性书写顺序：
 * 布局定位属性：`display / position / float / clear / visibility / overflow`
 * 自身属性：`width / height / margin / padding / border / background`
 * 文本属性：`color / font / text-decoration / text-align / vertical-align / white- space / break-word`
 * 其他属性（`CSS3`）：`content / cursor / border-radius / box-shadow / text-shadow / background:linear-gradient` …
* 8.css3浏览器私有前缀写法：浏览器私有前缀在前，标准前缀在后
```css
.jdc {
    -webkit-border-radius: 10px;
    -moz-border-radius: 10px;
    -o-border-radius: 10px;
    -ms-border-radius: 10px;
    border-radius: 10px;
}
```
#### [返回顶部](#css)
### css注释规范

* 1.单行注释：注释内容两边要有空格，单独占一行
```css
/* Comment Text */
.jdc{}
```
* 2.模块注释：注释内容第一个字符和最后一个字符都是一个空格字符，/* 与 模块信息描述占一行，多个横线分隔符-与*/占一行，行与行之间相隔两行
```css
/* Module A
---------------------------------------------------------------- */
.mod_a {}
```
* 3.文件信息注释：在样式文件编码声明 @charset 语句下面注明页面名称、作者、创建日期等信息
```css
@charset "UTF-8";
/**
 * @desc File Info
 * @author Author Name
 * @date xxxx-xx-xx
 */
```
### 重置样式
* 1.移动端
```css
* { -webkit-tap-highlight-color: transparent; outline: 0; margin: 0; padding: 0; vertical-align: baseline; }
body, h1, h2, h3, h4, h5, h6, hr, p, blockquote, dl, dt, dd, ul, ol, li, pre, form, fieldset, legend, button, input, textarea, th, td { margin: 0; padding: 0; vertical-align: baseline; }
img { border: 0 none; vertical-align: top; }
i, em { font-style: normal; }
ol, ul { list-style: none; }
input, select, button, h1, h2, h3, h4, h5, h6 { font-size: 100%; font-family: inherit; }
table { border-collapse: collapse; border-spacing: 0; }
a { text-decoration: none; color: #666; }
body { margin: 0 auto; min-width: 320px; max-width: 640px; height: 100%; font-size: 14px; font-family: -apple-system,Helvetica,sans-serif; line-height: 1.5; color: #666; -webkit-text-size-adjust: 100% !important; text-size-adjust: 100% !important; }
input[type="text"], textarea { -webkit-appearance: none; -moz-appearance: none; appearance: none; }
```
#### [返回顶部](#css)
* 2.PC端
```css
html, body, div, h1, h2, h3, h4, h5, h6, p, dl, dt, dd, ol, ul, li, fieldset, form, label, input, legend, table, caption, tbody, tfoot, thead, tr, th, td, textarea, article, aside, audio, canvas, figure, footer, header, mark, menu, nav, section, time, video { margin: 0; padding: 0; }
h1, h2, h3, h4, h5, h6 { font-size: 100%; font-weight: normal }
article, aside, dialog, figure, footer, header, hgroup, nav, section, blockquote { display: block; }
ul, ol { list-style: none; }
img { border: 0 none; vertical-align: top; }
blockquote, q { quotes: none; }
blockquote:before, blockquote:after, q:before, q:after { content: none; }
table { border-collapse: collapse; border-spacing: 0; }
strong, em, i { font-style: normal; font-weight: normal; }
ins { text-decoration: underline; }
del { text-decoration: line-through; }
mark { background: none; }
input::-ms-clear { display: none !important; }
body { font: 12px/1.5 \5FAE\8F6F\96C5\9ED1, \5B8B\4F53, "Hiragino Sans GB", STHeiti, "WenQuanYi Micro Hei", "Droid Sans Fallback", SimSun, sans-serif; background: #fff; }
a { text-decoration: none; color: #333; }
a:hover { text-decoration: underline; }
```
### 媒体查询
#### 常用媒体查询语句
* 1.判断设备横竖屏
```css
/* 横屏 */
@media all and (orientation :landscape) {

} 

/* 竖屏 */
@media all and (orientation :portrait) {

}
```
* 2.判断设备宽高
```css
/* 设备宽度大于 320px 小于 640px */
@media all and (min-width:320px) and (max-width:640px) {
    
}
```
#### [返回顶部](#css)
* 3.判断设备像素比
```css
/* 设备像素比为 1 */
@media only screen and (-webkit-min-device-pixel-ratio: 1), only screen and (min-device-pixel-ratio: 1) {
    
}

/* 设备像素比为 1.5 */
@media only screen and (-webkit-min-device-pixel-ratio: 1.5), only screen and (min-device-pixel-ratio: 1.5) {
    
}

/* 设备像素比为 2 */
@media only screen and (-webkit-min-device-pixel-ratio: 2), only screen and (min-device-pixel-ratio: 2) {
    
}
```
#### 常用设备设置
**iPhone**：
```css
/* ----------- iPhone 4 and 4S ----------- */

/* Portrait and Landscape */
@media only screen 
  and (min-device-width: 320px) 
  and (max-device-width: 480px)
  and (-webkit-min-device-pixel-ratio: 2) {

}

/* Portrait */
@media only screen 
  and (min-device-width: 320px) 
  and (max-device-width: 480px)
  and (-webkit-min-device-pixel-ratio: 2)
  and (orientation: portrait) {
}

/* Landscape */
@media only screen 
  and (min-device-width: 320px) 
  and (max-device-width: 480px)
  and (-webkit-min-device-pixel-ratio: 2)
  and (orientation: landscape) {

}

/* ----------- iPhone 5 and 5S ----------- */

/* Portrait and Landscape */
@media only screen 
  and (min-device-width: 320px) 
  and (max-device-width: 568px)
  and (-webkit-min-device-pixel-ratio: 2) {

}

/* Portrait */
@media only screen 
  and (min-device-width: 320px) 
  and (max-device-width: 568px)
  and (-webkit-min-device-pixel-ratio: 2)
  and (orientation: portrait) {
}

/* Landscape */
@media only screen 
  and (min-device-width: 320px) 
  and (max-device-width: 568px)
  and (-webkit-min-device-pixel-ratio: 2)
  and (orientation: landscape) {

}

/* ----------- iPhone 6 ----------- */

/* Portrait and Landscape */
@media only screen 
  and (min-device-width: 375px) 
  and (max-device-width: 667px) 
  and (-webkit-min-device-pixel-ratio: 2) { 

}

/* Portrait */
@media only screen 
  and (min-device-width: 375px) 
  and (max-device-width: 667px) 
  and (-webkit-min-device-pixel-ratio: 2)
  and (orientation: portrait) { 

}

/* Landscape */
@media only screen 
  and (min-device-width: 375px) 
  and (max-device-width: 667px) 
  and (-webkit-min-device-pixel-ratio: 2)
  and (orientation: landscape) { 

}

/* ----------- iPhone 6+ ----------- */

/* Portrait and Landscape */
@media only screen 
  and (min-device-width: 414px) 
  and (max-device-width: 736px) 
  and (-webkit-min-device-pixel-ratio: 3) { 

}

/* Portrait */
@media only screen 
  and (min-device-width: 414px) 
  and (max-device-width: 736px) 
  and (-webkit-min-device-pixel-ratio: 3)
  and (orientation: portrait) { 

}

/* Landscape */
@media only screen 
  and (min-device-width: 414px) 
  and (max-device-width: 736px) 
  and (-webkit-min-device-pixel-ratio: 3)
  and (orientation: landscape) { 

}
```
#### [返回顶部](#css)
**Galaxy Phones**:
```css
/* ----------- Galaxy S3 ----------- */

/* Portrait and Landscape */
@media screen 
  and (device-width: 320px) 
  and (device-height: 640px) 
  and (-webkit-device-pixel-ratio: 2) {

}

/* Portrait */
@media screen 
  and (device-width: 320px) 
  and (device-height: 640px) 
  and (-webkit-device-pixel-ratio: 2) 
  and (orientation: portrait) {

}

/* Landscape */
@media screen 
  and (device-width: 320px) 
  and (device-height: 640px) 
  and (-webkit-device-pixel-ratio: 2) 
  and (orientation: landscape) {

}

/* ----------- Galaxy S4 ----------- */

/* Portrait and Landscape */
@media screen 
  and (device-width: 320px) 
  and (device-height: 640px) 
  and (-webkit-device-pixel-ratio: 3) {

}

/* Portrait */
@media screen 
  and (device-width: 320px) 
  and (device-height: 640px) 
  and (-webkit-device-pixel-ratio: 3) 
  and (orientation: portrait) {

}

/* Landscape */
@media screen 
  and (device-width: 320px) 
  and (device-height: 640px) 
  and (-webkit-device-pixel-ratio: 3) 
  and (orientation: landscape) {

}

/* ----------- Galaxy S5 ----------- */

/* Portrait and Landscape */
@media screen 
  and (device-width: 360px) 
  and (device-height: 640px) 
  and (-webkit-device-pixel-ratio: 3) {

}

/* Portrait */
@media screen 
  and (device-width: 360px) 
  and (device-height: 640px) 
  and (-webkit-device-pixel-ratio: 3) 
  and (orientation: portrait) {

}

/* Landscape */
@media screen 
  and (device-width: 360px) 
  and (device-height: 640px) 
  and (-webkit-device-pixel-ratio: 3) 
  and (orientation: landscape) {

}
```
#### [返回顶部](#css)
**HTC Phones**：
```csss
/* ----------- HTC One ----------- */

/* Portrait and Landscape */
@media screen 
  and (device-width: 360px) 
  and (device-height: 640px) 
  and (-webkit-device-pixel-ratio: 3) {

}

/* Portrait */
@media screen 
  and (device-width: 360px) 
  and (device-height: 640px) 
  and (-webkit-device-pixel-ratio: 3) 
  and (orientation: portrait) {

}

/* Landscape */
@media screen 
  and (device-width: 360px) 
  and (device-height: 640px) 
  and (-webkit-device-pixel-ratio: 3) 
  and (orientation: landscape) {

}
iPads
/* ----------- iPad mini ----------- */

/* Portrait and Landscape */
@media only screen 
  and (min-device-width: 768px) 
  and (max-device-width: 1024px) 
  and (-webkit-min-device-pixel-ratio: 1) {

}

/* Portrait */
@media only screen 
  and (min-device-width: 768px) 
  and (max-device-width: 1024px) 
  and (orientation: portrait) 
  and (-webkit-min-device-pixel-ratio: 1) {

}

/* Landscape */
@media only screen 
  and (min-device-width: 768px) 
  and (max-device-width: 1024px) 
  and (orientation: landscape) 
  and (-webkit-min-device-pixel-ratio: 1) {

}

/* ----------- iPad 1 and 2 ----------- */

/* Portrait and Landscape */
@media only screen 
  and (min-device-width: 768px) 
  and (max-device-width: 1024px) 
  and (-webkit-min-device-pixel-ratio: 1) {

}

/* Portrait */
@media only screen 
  and (min-device-width: 768px) 
  and (max-device-width: 1024px) 
  and (orientation: portrait) 
  and (-webkit-min-device-pixel-ratio: 1) {

}

/* Landscape */
@media only screen 
  and (min-device-width: 768px) 
  and (max-device-width: 1024px) 
  and (orientation: landscape) 
  and (-webkit-min-device-pixel-ratio: 1) {

}

/* ----------- iPad 3 and 4 ----------- */

/* Portrait and Landscape */
@media only screen 
  and (min-device-width: 768px) 
  and (max-device-width: 1024px) 
  and (-webkit-min-device-pixel-ratio: 2) {

}

/* Portrait */
@media only screen 
  and (min-device-width: 768px) 
  and (max-device-width: 1024px) 
  and (orientation: portrait) 
  and (-webkit-min-device-pixel-ratio: 2) {

}

/* Landscape */
@media only screen 
  and (min-device-width: 768px) 
  and (max-device-width: 1024px) 
  and (orientation: landscape) 
  and (-webkit-min-device-pixel-ratio: 2) {

}
```


