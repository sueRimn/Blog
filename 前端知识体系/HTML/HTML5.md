# HTML5
## 新特性（来自[MDN](https://developer.mozilla.org/zh-CN/docs/Web/Guide/HTML/HTML5)）
    * 语义：能够让你更恰当地描述你的内容是什么
    * 连通性：能够让你和服务器之间通过创新的新技术方法进行通信
    * 离线 & 存储：能够让网页在客户端本地存储数据以及更高效地离线运行
    * 多媒体：使 video 和 audio 成为了在所有 Web 中的一等公民
    * 2D/3D 绘图 & 效果：提供了一个更加分化范围的呈现选择
    * 性能 & 集成：提供了非常显著的性能优化和更有效的计算机硬件使用
    * 设备访问 Device Access：能够处理各种输入和输出设备
    * 样式设计: 让作者们来创作更加复杂的主题
## 语义化
> 语义化有利于更好的构架网页内容，便于搜索引擎的索引和抓取内容，并有利于团队的开发和维护
### 1.`<article>`
    * `<article>`：显示一个独立的文章内容
    * `artilce`可以嵌套，则内层的`artilce`对外层的``article`标签有隶属的关系
### 2.`<sction>`
    * 标签定义文档中的节（`section`、区段）。比如章节、页眉、页脚或文档中的其他部分
### 3.`<aside>`
    * 非正文类的内容。例如广告，成组的链接，侧边栏等等
### 4.`<hgroup>`
    * 用于对网页或区段的标题元素（`h1-h6`）进行组合。例如，在一个区段中你有连续的h系列的标签元素，则可以用hgroup将他们括起来
### 5.`<nav>`
    * 应该放入一些当前页面的主要导航链接
### 6.`<header>`
    * 定义文档的页面组合，通常是一些引导和导航信息
### 7.`<footer>`
    * 定义 `section` 或 `document` 的页脚
### 8.`<time>`
    * 定义公历的时间（24 小时制）或日期，时间和时区偏移是可选的
### 9.`<mark>`
    * 定义带有记号的文本,需要突出显示文本时使用
### 10.`<figure>`
    * 规定独立的流内容（图像、图表、照片、代码等等）。`figure` 元素的内容应该与主内容相关，但如果被删除，则不应对文档流产生影响。
### 11.`<figcaption>`
    * 定义 `figure` 元素的标题（`caption`）。"`figcaption`" 元素应该被置于 "`figure`" 元素的第一个或最后一个子元素的位置。
### 12.`<contextmenu>`
    * 添加到系统右键菜单 [貌似这个功能只有firefox支持]
## 表单的改进
### 1.`email`
    * 要求输入格式正确的`email`地址,否则浏览器是不允许提交的,并会有一个错误信息提示.此类型在`Opera`中必须指定`name`值,否则无效果.`<input type="email" >`
### 2.`<url>`
    * 要求输入格式正确的URL地址,Opera中会自动在开始处添加`http://`。`<input type="url" >`
### 3.`<number>`
    * 要求输入格式数字，默认会有上下两个按钮。`<input type="number" >`
### 4.`<tel>`
    * 要求输入一个电话号码。`<input type="tel" >`
### 5.`<range>`
    * 显示一个可拖动的滑块条,并可通过设定`max/min/step`值限定拖动范围.拖动时会反馈给value一个值。`<input type="range" min="20" max="100" step="2" >`
### 6.`<color>`
    * 此类型表单,可让用户通过颜色选择器选择一个颜色值,并反馈到value中。`<input type="color" value="#ff0000" >`
### 7.`<date>\<time>\<datetime><datetime-local>\<month>\<week>`
    ```
     <input type="date" >
     <input type="time" >
     <input type="datetime" >
     <input type="datetime-local" >
     <input type="month" >
     <input type="week" >

    ```
### 8.`<search>`
    * 输入的将是一个搜索关键字
### 9.`<required>`
    * 表单验证属性为`require`类型时,若输入值为空,则拒绝提交,并会有一个提示.这个很有用.并且可以用于`textarea`以及`hidden/image/submit`类型.`<input type="text" required >`
### 10.`<pattern>`
    * 类型为正则验证,可以完成各种复杂的验证
### 11.`<placeholder>`
    * 输入提示信息.`<input type="text" placeholder="hint message" >`
### 12.`<autofocus>`
    * 默认聚焦属性.`<input type="text" autofacus="true" >`
### 13.`<list>`
    * 需要与`datalist`属性共用,`datalist`是对选择框的记忆,而`list`属性可以为选择框自定义记忆的内容
    ```
    <input type="text" list="ilist">
    <datalist id="ilist">
        <option label="a" value="a">aaaaa</option>
        <option label="b" value="b">bbbbb</option>
        <option label="c" value="c">ccccc</option>
    </datalist>
    ```
### 14.`<autocomplete>`
    * 为表单提供自动完成功能.如果该属性为打开状态可很好地自动完成.一般来说,此属性必须启动浏览器的自动完成功能.`<input type="text" autocomplete="on" >`
### 15.`<keygen>`
    * 规定用于表单的密钥对生成器字段。当提交表单时，私钥存储在本地，公钥发送到服务器。所有主流浏览器都支持 `keygen` 标签，除了 `Internet Explorer` 和 `Safari`
### 16.`<datalist>`
    * 定义选项列表。
    * 与 `input` 元素配合使用该元素，来定义 `input` 可能的值
    * `datalist` 及其选项不会被显示出来，它仅仅是合法的输入值列表
    * 用 `input` 元素的 `list` 属性来绑定 `datalist`
    ```
    <label for="search">搜索引擎</label> 
    <input type="url" name="search" id="search" list="searchlist" autocomplete="on" pattern="https?://.+" />
    <datalist id="searchlist">
    　　<option value="http://www.baidu.com/" >
    　　<option value="http://www.google.com/" >
    　　<option value="http://www.sogou.com/" >
    </datalist>
    ```
### 17.`<output>`
    * 定义不同类型的输出
### 18.`<meter>`
    * 标签定义度量衡
### 19.`<progress>`
    * 定义运行中的进度（进程）。可以使用 `progress` 标签来显示 `JavaScript` 中耗费时间的函数的进度
### 20.`<contenteditable>`
    * 让每个元素里面的文本节点或值变为可编辑
## 音频
## 画布canvas
### 1.兼容性
> 除IE外所有的浏览器都支持canvas,可以使用[这个](https://github.com/arv/explorercanvas)为IE添加这个新特性
### 2.使用
    * `width`：设置宽度
    * `height`：设置高度
    * `API`：
        