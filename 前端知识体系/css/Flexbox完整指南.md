
# [Flexbox（弹性盒模型）布局完全指南](https://css-tricks.com/snippets/css/a-guide-to-flexbox/)
> 这个指南讲诉了flexbox的所有内容，重点介绍了父元素（`flex`容器）和子元素（`flex`元素）的所有不同可能属性。它还包括历史记录、演示、模式和浏览器支持图表。
## 背景
`Flexbox`布局（弹性盒模型）模块的目的在于提供一种更有效的方法在容器中的项之间布局、对齐和分配空间，即使它们的大小未知或是动态的(因此使用“`flex`一词)。

`flex`布局背后的主要思想是让容器能够更改其项（`item`）的宽度/高度(和顺序)，以最佳地填充可用空间(主要是为了适应各种显示设备和屏幕大小)。`flex`容器（`container`）扩展项以填充可用的空闲空间，或者收缩项以防止溢出。

最重要的是，与常规布局(基于垂直的块和基于水平的内联块)相比，`flexbox`布局是与方向无关的。虽然这些常规方法在页面上运行得很好，但是它们缺乏灵活性来支持大型或复杂的应用程序(特别是在改变方向、调整大小、拉伸、收缩等方面)。

**注意**:`Flexbox`布局最适合应用程序的组件和小规模布局，而`Grid`布局则适用于更大规模的布局。

## 基本术语
由于`flexbox`是一个完整的模块而不是一个单独的属性，所以它涉及到很多东西，包括它的整个属性集。其中一些是要在容器上设置的(父元素，称为“`flex container`”)，而其他的是要在子元素上设置的(称为“`flex item`”)。

如果“常规”布局基于块和内联流方向，那么`flex`布局则基于“`flex-flow`方向”。请从规范中查看这个图，解释`flex`布局背后的主要思想。
![](https://css-tricks.com/wp-content/uploads/2018/11/00-basic-terminology.svg)
`item`将沿着主轴（`main axis`）(从主轴开始（`main-start`）到主轴结束（`main-end`）)或纵轴()(从纵轴开始（`cross-start`）到纵轴结束（`cross-end`）)布置。

**main axis**：伸缩容器的主轴是放置伸缩项的。**注意，它不一定是水平的，它取决于`flex-direction`属性(参见下面)**。

**main-start|main-end**：`flex`项被放置在容器中，从`main-start`到`main-end`。

**main size**：伸缩项（`flex item`）的宽度或高度，无论在主维度（`main`）中是哪个，都是项的主尺寸。`flex item`的`main``size`属性是“`width`”或“`height`”属性，两者在主维度中都有。

**cross axis**：垂直于主轴（`main axis`）的轴称为横轴。它的方向取决于主轴方向。

**cross-start|cross-end**：伸缩线由`item`填充，并从伸缩容器的`cross-start`侧开始，一直到`corss-end`侧，然后放入容器中。

**cross size**：`flex item`的宽度或高度，无论在`corss`维度中是哪个，都是`item`的`cross size`。`cross size`属性是在`corss`维度中的“宽度”或“高度”中的任何一个。

父元素属性(`flex container`) | 子元素属性(`flex item`)
------ | ------
![父元素属性(`flex container`)](https://css-tricks.com/wp-content/uploads/2018/10/01-container.svg) | ![子元素属性(`flex item`)](https://css-tricks.com/wp-content/uploads/2018/10/02-items.svg)
**dispaly** | **order**
  | ![](https://css-tricks.com/wp-content/uploads/2018/10/order.svg)
定义了一个`flex`容器，内联或块取决于它给定的值。它为所有直接子元素启用`flex`上下文<br>**注意**：`css`列对`flex`容器没有影响 | 默认情况下，`flex item`按源顺序排列。然而，`order`属性控制它们在`flex`容器中出现的顺序
.container{<br>display:flex;//或者 inline-flex<br>} | .item{<br>order:<整数值>;//默认为0<br>}
**flex-direction** | **flex-grow**
![](https://css-tricks.com/wp-content/uploads/2018/10/flex-direction.svg) | ![](https://css-tricks.com/wp-content/uploads/2018/10/flex-grow.svg)
这将建立主轴，从而定义放置在`flex`容器中的方向`flex item`。<br>`flexbox`(除了可选的包装)是一个单向布局概念。可以将`flex item`主要放在水平行或垂直列中 | 这定义了`flex item`在必要时增长的能力。<br>它接受一个作为比例的无单位值。它指定`item`在`flex`容器中应该占用多少可用空间。<br>如果所有项目都将`flex- growth`设置为1，容器中剩余的空间将平均分配给所有子元素。如果其中一个子元素的值为2，那么剩余的空间将会占用两倍于其他元素的空间(或者至少它会尝试这样做)<br>**注意**：负数无效
.container{ <br>flex-direction:row / row-reverse / column / column-reverse;<br>}<br><br>**row(默认)**:`ltr`是从左到右；`rtl`是从右到左;<br>**row-reverse**：`ltr`是从右到左，`rtl`是从左到右<br>**column**:从上到下<br>**column-reverse**：从下到上| .item{<br>flex-grow: <数值>; //默认为0<br>}
**flex-wrap** | **flex-shrink**
![](https://css-tricks.com/wp-content/uploads/2018/10/flex-wrap.svg) | 
默认情况下，`flex item`都会试着放在一行上。您可以更改此属性，并允许根据需要使用此属性对项进行包装 | 这定义了`flex item`在必要时的伸缩能力
.container{<br>flex-wrap: nowrap / wrap / wrap-reverse;<br>}<br><br>**nowrap（默认）**：所有`flex item`将在一条线上<br>**wrap**：`flex item`将会从上到下分为多行<br>**wrap-reverse**：`flex item`将会从下到上分为多行 | .item{<br> flex-shrink:<数值>;<br>}<br>负数无效
**flex-flow(用于父felx容器元素** | **flex-basis**
这是一个简化的`flex-direction`和`flex-wrap`属性，它们一起定义`flex`容器的主轴和交叉轴。默认值是`row nowrap`。 | 这定义了在分配剩余空间之前元素的默认大小。它可以是一个长度(例如20%，5rem，等等)或者一个关键字。<br>`auto`关键字的意思是“查看我的宽度或高度属性”(这是由`main-size`关键字临时完成的，直到被弃用)。<br>`content`关键字的意思是“根据项目的内容调整大小”——这个关键字还没有得到很好的支持，因此很难进行测试，而且更难知道它的兄弟`max-content`、`min-content`和`fit-content`做了什么。
felx-flow: <'felx-direction'>  <'flex-wrap'> | .item{<br>flex-basis: <长度> / auto; //默认是auto<br>}<br>如果设置为0，则不考虑内容周围的额外空间<br>如果设置为`auto`，则根据其`flex-growth`值分配额外的空间
**justify-content** | **flex**
![](https://css-tricks.com/wp-content/uploads/2018/10/justify-content.svg) | 
这定义了沿着主轴的对齐。<Br>当一行中的所有`flex item`都是不灵活的，或者都是灵活的，但已经达到最大大小时，它可以帮助分配剩余的额外空闲空间。当项目溢出行时，它还对它们的对齐方式施加一些控制。  | 这是`flex-growth`、`flex-shrink`和`flex-base`组合的简写。<br>第二个和第三个参数(`flex-shrink`和`flex-base`)是可选的。默认值是0 1 auto。
  .container{<br>justify-content: flex-start / felx-end / center;<br>}<br>**flex-start(默认)**：
