# Grid完全指南
> `CSS`网格布局是`CSS`中最强大的布局系统。它是一个二维系统，这意味着它可以处理列和行，而`flexbox`基本上是一个一维系统。通过将CSS规则应用于父元素(成为网格容器)和子元素(成为网格项)，可以使用网格布局。
## 介绍
`CSS`网格布局(又名“Gird”)是一个基于网格的二维布局系统，它的目标是彻底改变我们设计基于网格的用户界面的方式。`CSS`一直被用来布局我们的网页，但它从来没有做得很好。首先，我们使用了表，然后是浮点数、定位和内联块，但是所有这些方法本质上都是修改过的，并且遗漏了很多重要的功能(例如垂直居中)。`Flexbox`帮助解决了这个问题，但它的目标是更简单的一维布局，而不是复杂的二维布局(`Flexbox`和`Grid`际上可以很好地协同工作)。`Grid`是第一个专门为解决布局问题而创建的`CSS`模块。
## 基础以及浏览器支持
首先，您必须将容器元素定义为一个带有`display: grid`的网格，使用`grid-template-columns`和`grid-template-rows`设置列和行大小，然后将其子元素放入带有`grid-column`和`grid-row`的网格中。与`flexbox`类似，网格项的源顺序并不重要。您的`CSS`可以以任何顺序排列它们，这使得使用媒体查询重新排列网格变得超级容易。想象一下，定义整个页面的布局，然后用几行`CSS`完全重新排列它，以适应不同的屏幕宽度。`Grid`是有史以来`css`最强的的模块之一。

**Desktop** | **Mobile**/**Tablet**
------ | ------ 
Chrome:57<br>Opera:44<br>Firefox:52<br>Edge:16<br>Safari:10.1 | ios Safari:10.3<br> Opera Mobile:46<br>Opera Mini:No<br> Android:67<br> Android Chrome:71<br> Android Firefox:64
## 重要术语
#### Grid container(网格容器)
应用`display: grid`的元素。它是所有网格项的直接父元素。在本例中，`container`是网格容器。
```
<div class="container">
  <div class="item item-1"></div>
  <div class="item item-2"></div>
  <div class="item item-3"></div>
</div>
```
#### Grid item（网格项）
网格容器的孩子(即直接后代)。这里的`item`元素是网格项，但`sub-item`不是。
```
<div class="container">
  <div class="item"></div> 
  <div class="item">
  	<p class="sub-item"></p>
  </div>
  <div class="item"></div>
</div>
```
#### Grid Line（网格线）
构成网格结构的分界线。它们可以是垂直的(“列网格线”)，也可以是水平的(“行网格线”)，并且位于行或列的任意一边。这里的黄线是列网格线的一个例子。
[](https://css-tricks.com/wp-content/uploads/2018/11/terms-grid-line.svg)
#### Grid Track（网格轨迹）
相邻网格线之间的空间。你可以把它们想象成网格的列或行。这是第二行和第三行网格线之间的网格轨迹。
[](https://css-tricks.com/wp-content/uploads/2018/11/terms-grid-track.svg)
#### Grid Cell(网格单元)
相邻行与相邻列网格线之间的空间。它是网格的一个单一“单元”。这是行网格线1和2之间的网格单元格，列网格线2和3之间的网格单元格。
[](https://css-tricks.com/wp-content/uploads/2018/11/terms-grid-cell.svg)
#### Grid Area(网格域)
整个空间由四条网格线包围。网格区域可以由任意数量的网格单元组成。这是行网格线1和3之间的网格区域，列网格线1和3之间的网格区域。
[](https://css-tricks.com/wp-content/uploads/2018/11/terms-grid-area.svg)
## Grid属性内容表
Grid容器属性 | Grid项属性
----- | ------
**display** | **grid-column-start**
将元素定义为网格容器，并为其内容建立新的网格格式化上下文。
