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
   
   方法 / 属性 | 使用方法 | 描述
   ------ | ------ | ------
getContext() | var canvas = document.getElementById("canvas"); var ctx = canvas.getContext("2d"); |  获取绘制环境返回一个用于在画布上绘图的环境。
save() | ctx.save(); | 保存路径
restore() | ctx.restore(); | 恢复路径
scale() |ctx.scale(x, y);  //x轴缩放比例|y轴缩放比例 | 缩放
rotate() | ctx.rotage(radian); //radian 弧度=角度*Math.PI/180 | 旋转角度
translate() | ctx.translate(x, y);  //x轴的位移|Y轴的位移 | 偏移
transform() |ctx.transform(a, b, c, d, e, f);   变换
setTransform() |ctx.setTransform(a, b, c, d, e, f); |设置变换
globalAlpha |ctx.globalAlpha = 0.8; |透明度
globalCompositeOperation |ctx.globalCompositeOperation = ""; |转透明度
fillStyle |ctx.fillStyle = "#ff0000"; | 设置绘图的背景颜色
strokeStyle |ctx.strokeStyle = "blue"; |在绘制的图形上添加边框颜色
addColorStop() |ctx.addColorStop(offset, color） //offset | 在绘制的图形上添加边框颜色
createLinearGradient()|ctx.createLinearGradient(x,y,w,h); //x轴位置|y轴位置|渐变宽度|渐变高度  |颜色和边框创建一个渐变
createRadialGradient() |ctx. createRadialGradient(x0, y0, r0, x1, y1, r1); // 颜色和边框 |在绘制的图形上添加边框颜色
createPattern() |ctx.createPattern(img, repeatition); //img 图片对象 //repeatition |在绘制的图形上添加边框颜色
lineWidth |ctx.lineWidth = 10; |边界 设置绘制的图形边框
lineJoin |ctx.lineJoin = "round"; //3种格式miter|round|bevel //默认|圆角|斜角 |设置绘制的图形的辩解样式
lineCap |ctx.lineCap = "round"; //3种格式 butt|round|square //默认|圆角|高度多出线宽的一半 |设置绘制的图形的辩解样式
miterLimit |ctx.miterLimit = "";  |边框斜切限制
shadowColor |ctx.shadowColor = "red";  |投影颜色
shadowOffsetX |ctx.shadowOffsetX = 10;  |投影的水平位移
shadowOffsetY |ctx.shadowOffsetY = 10;  | 投影的垂直位移
shadowBlur |ctx.shadowBlur = 10;  |投影的模糊大小
fillRect() |ctx.fillRect(x,y,w,h); | 在画布上填充黑色背景（矩形）
strokeRect() |ctx.strokeRect(x,y,w,h); |在画布上绘制一个带边框的矩形
clearRect() |ctx.clearRect(x,y,w,h); |绘制矩形清除指定范围内的内容
beginPath() |function draw(){ beginPath();//.... closePath(); } |绘制路径开始绘制一个新的路径，避免与后面绘制的路径重叠
closePath() |代码同上 |绘制路径关闭路径，如果不设置最后一个点，则默认以第一个点结束。
moveTo() |ctx.moveTo(120, 120); //x, y |绘制路径移动到绘制的新目标点，设置一个新的点
lineTo() |ctx.lineTo(220, 320); //x, y |绘制路径新的目标点
quadraticCurveTo() |ctx.quadraticCurveTo (cpx, cpy, x, y); //贝赛尔曲线 |控制点|坐标点 |绘制路径新的目标点
bezierCurveTo() |ctx. bezierCurveTo (cp1x, cp1y, cp2x, cp2y, x, y); //贝赛尔曲线 |控制点|控制点|坐标点 |绘制路径新的目标点
arc()|ctx.arc(x, y, r, s, e, d);  //x,y,半径,起始弧度,结束弧度,旋转方向//旋转方向:false[顺时针],true[逆时针] |绘制路径画一个圆
arcTo() |ctx.arc(x1, y1, x2, y2, r);  //第一组坐标|第二组坐标|半径 |绘制路径画一个圆
rect() |ctx.rect(); //x,y,w,h |绘制路径绘制一个矩形
fill() |ctx.fill();//填充，默认黑色 |绘制路径 |把lineTO()设置的点区域用默认颜色填充成一个图形
stroke() |ctx.stroke();//画线，默认黑色 |绘制路径把lineTO()设置的点连接起来
clip() |ctx.clip();// |绘制路径
isPointInPath() |ctx.isPointInPath();// |绘制路径
drawFocusRing() |ctx.drawFocusRing (ele, canDrawCustom);// |集中管理
setCaretSelectionRect() |ctx.setCaretSelectionRect (ele, x, y, w, h); // |插入符和选择器管理
caretBlinkRate() |ctx.caretBlinkRate() // |插入符和选择器管理
font |ctx.font="" // 文本设置字体类型
textAlign = "" |ctx.textAlign = "" //start, end, left, right, center //def:start |文本对齐方式
textBaseline |ctx.textBaseline="" //def:alphabetic |文本
fillText() |ctx.fillText (text, x, y[, maxWidth ])  |设置填充的文本
strokeText() |ctx.strokeText (text, x, y[, maxWidth ])  |文本
measureText() |var metrics  = ctx.measureText(text);metrics . width  |文本
drawImage() |drawImage(image,dx,dy) drawImage(image,dx,dy,dw,dh) drawImage(image,sx,sy,sw,sh, dx,dy,dw,dh) // |图片操作在画布上载入一张图片
createImageData() |createImageData(sw,sh)  |图片操作
createImageData() |createImageData(imageData)  |图片操作
getImageData() |var imageData = createImageData(sx,sy,sw,sh) imageData.width imageData.height imageData.data  |图片操作
putImageData() |putImageData(imageData,dx,dy[, dirtyX,dirtyY,dirtyWidth, dirtyHeight])  |图片操作
        
