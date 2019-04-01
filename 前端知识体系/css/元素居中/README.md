## 水平居中
### 1.行内元素水平居中
   * 利用 `text-align: center` 可以实现在**块级元素内部的行内元素**水平居中。此方法对`inline`、`inline-block`、`inline-table`和`inline-flex`元素水平居中都有效。
### 2.块级元素的水平居中
   * 将该块级元素左右外边距`margin-left`和`margin-right`设置为`auto`
   * 使用`table` + `margin`：先将子元素设置为块级表格来显示（类似），再将其设置水平居中，`display:table`在表现上类似`block`元素，但是宽度为内容宽。
   * 使用`absolute` + `transform`:先将父元素设置为相对定位，再将子元素设置为绝对定位，向右移动子元素，移动距离为父容器的一半，最后通过向左移动子元素的一半宽度以达到水平居中.不过`transform`属于`css3`内容，兼容性存在一定问题，高版本浏览器需要添加一些前缀。
   * 使用`flex`+`justify-content`
   * 使用`flex`+`margin`：通过`flex`将父容器设置为为`Flex`布局，再设置子元素居中
### 3.多块级元素水平居中
   * 利用`flex`布局:其中`justify-content` 用于设置弹性盒子元素在主轴（默认横轴）方向上的对齐方式
   * 利用`inline-block`:将要水平排列的块状元素设为`display:inline-block`，然后在父级元素上设置`text-align:center`，达到与上面的行内元素的水平居中一样的效果。
### 4.浮动元素水平居中
   * 对于定宽的浮动元素，通过子元素设置`relative` + 负`margin`
   * 对于不定宽的浮动元素，父子容器都用相对定位
   * 通用方法(不管是定宽还是不定宽)：利用弹性布局(`flex`)的`justify-content`属性，实现水平居中,子元素有无定宽不影响
### 5.绝对定位元素水平居中
   * 通过子元素绝对定位，外加`margin: 0 auto`来实现
## 垂直居中
### 1.单行内联元素垂直居中
   * 利用行高`line-height`设置为`height`的高度
### 2.多行内联元素垂直居中
   * 利用`flex`布局（`flex`）：利用`flex布局实现垂直居中，其中`flex-direction: column`定义主轴方向为纵向。这种方式在较老的浏览器存在兼容性问题
   * 利用表布局（`table`）:利用表布局的`vertical-align: middle`可以实现子元素的垂直居中
### 3.块级元素垂直居中
   * 使用`absolute`+负`margin`(已知高度宽度);通过绝对定位元素距离顶部50%，并设`margin-top`向上偏移元素高度的一半，就可以实现了
   * 使用`absolute`+`transform`:当垂直居中的元素的高度和宽度未知时，可以借助`CSS3`中`transform`属性向Y轴反向偏移50%的方法实现垂直居中。但是部分浏览器存在兼容性的问题。
   * 使用`flex`+`align-items`:通过设置`flex`布局中的属性`align-items`，使子元素垂直居中
   * 使用`table-cell`+`vertical-align`:通过将父元素转化为一个表格单元格显示（类似 `<td> `和 `<th>`），再通过设置 `vertical-align`属性，使表格单元格内容垂直居中。
## 水平垂直居中
### 1.绝对定位与负边距（已知高度宽度）
   * 需要知道被垂直居中元素的高和宽，才能计算出`margin`值，兼容所有浏览器
### 2.绝对定位与`margin:auto`（已知高度宽度）
   * 这种方式无需知道被垂直居中元素的高和宽，但不能兼容低版本的IE浏览器
### 3.绝对定位+`CSS3`(未知元素的高宽)
   * 利用`Css3`的`transform`，可以轻松的在未知元素的高宽的情况下实现元素的垂直居中。`CSS3`的`transform`固然好用，但在项目的实际运用中必须考虑兼容问题，大量的`hack`代码可能会导致得不偿失。
### 4.flex布局
   * 利用`flex`布局，其中`justify-content` 用于设置或检索弹性盒子元素在主轴（横轴）方向上的对齐方式；而`align-items`属性定义`flex`子项在`flex`容器的当前行的侧轴（纵轴）方向上的对齐方式。不能兼容低版本的IE浏览器。
### 5.`flex/grig`和`margin:0 auto`(最简单的写法)
   * 容器元素设为 `flex` 布局或是`grid`布局，子元素只要写 `margin: auto` 即可,不能兼容低版本的IE浏览器
### 参考阅读
[如何居中一个元素](https://github.com/ljianshu/Blog/issues/29)
