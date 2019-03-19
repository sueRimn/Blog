
# CSS
## CSS常用属性
## 盒模型
> 盒模型（`box model`）是元素大小的呈现方式。盒模型默认的值是`content-box`，新增的值是`padding-box`和border-box`

**盒模型计算元素宽高的区别如下**：

**content-box(默认)**：

width = width + padding-left + padding-right + border-left + border-right;

height = height + padding-top + padding-bottom + border-top + border-bottom;

**padding-box**:

width = width(包含padding-left + padding-right) + border-top + border-bottom;

height = height(包含padding-top + padding-bottom) + border-top + border-bottom;

**border-box**:

width = width(包含padding-left + padding-right + border-left + border-right);

height = height(包含padding-top + padding-bottom + border-top + border-bottom);
## BFC
`BFC`就是块级格式上下文，是一个独立渲染区域，让处于`BFC`内部的怨怒是和外部的元素相互隔离，使内部元素的定位不会相互影响
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

**relative(相对定位)**：

设置之后，通过修改`top left bottom right`值，元素会在自身文档流里偏离位置，但是其他元素不会调整位置来弥补它偏离后剩下的空隙。

**absolute(绝对定位)**：

设置之后元素脱离文档流，其他元素会调整位置弥补它偏离了后留下的空隙。

元素偏离是相当于离它最近的设置了定位属性的元素（`position`的值不为`static`）d的位置进行偏离。

如果该元素为块级元素，那么它设置定位属性，宽度是由内容撑开的。因为默认文档流中（`position`为`static`）块级元素如果没有设置宽度属性，会自动填满整行。

**fixed(固定定位)**：

设置之后，元素相对的偏移的参考可视窗口的，即使在页面滚动的情况下，也会在固定位置。
## CSS浮动
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
```
<div class="box-wrapper">
    <div class="box"></div>
    <div class="box"></div>
    <div class="box"></div>
    <div style="clear:both;"></div>
</div>
```

**使用clearfix**：
```
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
## css居中布局
[水平居中+垂直居中+水平垂直居中](https://github.com/sueRimn/Blog/tree/master/%E5%89%8D%E7%AB%AF%E7%9F%A5%E8%AF%86%E4%BD%93%E7%B3%BB/css/%E5%85%83%E7%B4%A0%E5%B1%85%E4%B8%AD)
## link和@import的区别
 区别  |  link | @import
--- | ---  | ------
功能 |  较多 | 只能用于加载`css`
加载顺序 | 解析`link`时，页面同步加载所引用的`css` | 页面加载完后才被加载
浏览器支持 |   | `IE5`以上
JS动态引入 | Yes | No
## CSS规范与书写顺序
#### 语义化命名
#### 书写顺序
* 位置顺序（`position` `top` `right` `z-index` `display` `float`等）
* 大小（`width` `height` `padding` `margin`）
* 文字（`font` `line-height` `letter-sapce` `color-text-align`等）
* 背景（`background` `border`等）
* 其他（`animation` `transition`等）
