## 一、布局

### 1、使用vw定制rem自适应布局

> 移动端通过JS设置不同屏幕宽度高比的`font-size`，结合`vw`和`calc()`脱离JS控制

```css
html {
    font-size: calc(100vw/7.5)
}
```

### 2、text-align-last:justify对齐文本两端

```css
text {
    text-align-last:justify
}
```



### 3、object-fit图片自适应

> 使图像脱离约束，让图片尺寸自适应

```css
img {
        width: 100%;
        height: 260px;
        background-color: #3c9;
        &.cover {
            object-fit: cover;
        }
        &.contain {
            object-fit: contain;
        }
        &.fill {
            object-fit: fill;
        }
        &.scale-down {
            object-fit: scale-down;
        }
    }
```

### 4、overflow-x横向排版

> 通过`flexbox`或者`inline-block`横向排列元素，对其父元素设置`overflow-x:auto`横向滚动

### 5、text-overflow:ellipsis控制文本溢出

```css
p {
    display: -webkit-box;
    overflow: hidden;
    text-overflow: ellipsis;
}
```

### 6、transform:scale3d()翻转内容

> 通过`transform:scale3d()`对内容进行翻转(水平翻转、垂直翻转、倒序翻转)

```css
text {
    transform: scale3d(-1, 1, 1);
}
```

### 7、letter-spacing排版倒序文本

> 通过`letter-spacing`设置负值字体间距将文本倒序

```css
.reverse-text {
    font-weight: bold;
    font-size: 50px;
    color: #f66;
    letter-spacing: -100px; // letter-spacing最少是font-size的2倍
}
```

### 8、margin-left排版左重右轻列表

> 使用`flexbox横向布局`时，最后一个元素通过`margin-left:auto`实现向右对齐

```css
HTML SCSSResult
EDIT ON
.left-list {
    display: flex;
    align-items: center;
    padding: 0 10px;
    width: 600px;
    height: 60px;
    background-color: #3c9;
    li {
        padding: 0 10px;
        height: 40px;
        background-color: #3c9;
        line-height: 40px;
        font-size: 16px;
        color: #fff;
        & + li {
            margin-left: 10px;
        }
        &:last-child {
            margin-left: auto;
        }
    }
}
```

## 行为

### overflow-scrolling:touch弹性滚动

> iOS页面`非body元素`的滚动操作会非常卡(Android不会出现此情况)，通过`overflow-scrolling:touch`调用Safari原生滚动来支持弹性滚动，增加页面滚动的流畅度

```css
body {
    -webkit-overflow-scrolling: touch;
}
.elem {
    overflow: auto;
}
```

### transform启动GPU硬件加速

```css
.elem {
    transform: translate3d(0, 0, 0); /* translateZ(0)亦可 */
}
```

### :valid和:invalid校验表单

> `input`使用伪类`:valid`和`:invalid`配合`pattern`校验表单输入的内容

```css
.form-validation {
    width: 500px;
    div {
        margin-top: 10px;
        &:first-child {
            margin-top: 0;
        }
    }
    label {
        display: block;
        padding-bottom: 5px;
        font-weight: bold;
        font-size: 16px;
    }
    input,
    textarea {
        display: block;
        padding: 0 20px;
        outline: none;
        border: 1px solid #ccc;
        width: 100%;
        height: 40px;
        caret-color: #09f;
        transition: all 300ms;
        &:valid {
            border-color: #3c9;
            box-shadow: inset 5px 0 0#3c9;
        }
        &:invalid {
            border-color: #f66;
            box-shadow: inset 5px 0 0 #f66;
        }
    }
    textarea {
        height: 122px;
        resize: none;
        line-height: 30px;
        font-size: 16px;
    }
}
```

### pointer-events禁用事件触发

> 通过`pointer-events:none`禁用事件触发(默认事件、冒泡事件、鼠标事件、键盘事件等)，相当于``的`disabled`，可以**限时点击按钮**(发送验证码倒计时)、**事件冒泡禁用**(多个元素重叠且自带事件、a标签跳转)

```css
.disabled-trigger {
    padding: 0 20px;
    border-radius: 10px;
    height: 40px;
    background-color: #66f;
    pointer-events: none;
    line-height: 40px;
    color: #fff;
}
```

### 使用+或~美化选项框

> ``使用`+`或`~`配合`for`绑定`radio`或`checkbox`的选择行为

```css
HTML SCSSResult
EDIT ON
.beauty-selection {
    display: flex;
    li {
        display: flex;
        align-items: center;
        margin-left: 20px;
        &:first-child {
            margin-left: 0;
        }
    }
    input:checked + label {
        background-color: #f90;
    }
    label {
        margin-right: 5px;
        padding: 2px;
        border: 1px solid #f90;
        border-radius: 100%;
        width: 18px;
        height: 18px;
        background-clip: content-box;
        cursor: pointer;
        transition: all 300ms;
        &:hover {
            border-color: #09f;
            background-color: #09f;
            box-shadow: 0 0 7px #09f;
        }
    }
    span {
        font-size: 16px;
    }
}
```

### 使用:focus-within分发冒泡响应

> 表单控件触发`focus`和`blur`事件后往父元素进行冒泡，在父元素上通过`:focus-within`捕获该冒泡事件来设置样式
>
> **登录注册弹框**、**表单校验**、**离屏导航**、**导航切换**

### 使用:hover描绘鼠标跟随

> 将整个页面等比划分成小的单元格，每个单元格监听`:hover`，通过`:hover`触发单元格的样式变化来描绘鼠标运动轨迹

### 使用max-height切换自动高度

> 通过`max-height`定义收起的最小高度和展开的最大高度，设置两者间的过渡切换
>
> **隐藏式子导航栏**、**悬浮式折叠面板**

### 使用transform模拟视差滚动

> 通过`background-attachment:fixed`或`transform`让多层背景以不同的速度移动，形成立体的运动效果

### 使用resize拉伸分栏

> 通过`resize`设置横向自由拉伸来调整目标元素的宽度

```css
.resize-bar {
    overflow: scroll;
    width: 200px;
    height: 100%;
    opacity: 0;
    resize: horizontal;
    &::-webkit-scrollbar {
        width: 200px;
        height: 100%;
    }
    &:hover,
    &:active {
        & ~ .resize-line {
            border-left: 1px dashed #09f;
        }
    }
}
```

## 颜色

### 使用color改变边框颜色

> `border`没有定义边框颜色时，设置`color`后，`border-color`会被定义为`color`

```css
.elem {
    border: 1px solid;
    color: #f66;
}
```

### 使用filter开启悼念模式

> 通过`filter:grayscale()`设置灰度模式来悼念某位去世的仁兄或悼念因灾难而去世的人们

```css
html {
    filter: grayscale(100%);
}
.mourning-mode {
    img {
        width: 400px;
    }
}
```

### 使用::selection改变文本选择颜色

> 通过`::selection`根据主题颜色自定义文本选择颜色

```css

::selection {
    background-color: #66f;
    color: #fff;
}
.select-color {
    line-height: 50px;
    font-weight: bold;
    font-size: 30px;
    color: #f66;
}
.special::selection {
    background-color: #3c9;
}
```

### 使用linear-gradient控制背景渐变

> 通过`linear-gradient`设置背景渐变色并放大背景尺寸，添加背景移动效果

```css
.gradient-bg {
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100%;
    background: linear-gradient(135deg, #f66, #f90, #3c9, #09f, #66f) left center/400% 400%;
    font-weight: bold;
    font-size: 100px;
    color: #fff;
    animation: move 10s infinite;
}
@keyframes move {
    0%,
    100% {
        background-position-x: left;
    }
    50% {
        background-position-x: right;
    }
}
```

### linear-gradient控制文本渐变

> 通过`linear-gradient`设置背景渐变色，配合`background-clip:text`对背景进行文本裁剪，添加滤镜动画

```css
HTML SCSSResult
EDIT ON
.gradient-text {
    background-image: linear-gradient(90deg, #f66, #f90);
    background-clip: text;
    line-height: 60px;
    font-size: 60px;
    animation: hue 5s linear infinite;
    -webkit-text-fill-color: transparent;
}
@keyframes hue {
    from {
        filter: hue-rotate(0);
    }
    to {
        filter: hue-rotate(-1turn);
    }
}
```

### caret-color改变光标颜色

### ::scrollbar改变滚动条样式

```css
.scroll-indicator {
    position: relative;
    overflow: hidden;
    border: 1px solid #66f;
    width: 500px;
    height: 300px;
    &::after {
        position: absolute;
        left: 0;
        right: 5px;
        top: 2px;
        bottom: 0;
        background-color: #fff;
        content: "";
    }
}
.article {
    overflow: auto;
    height: 100%;
    &::-webkit-scrollbar {
        width: 5px;
    }
    &::-webkit-scrollbar-track {
        background-color: #f0f0f0;
    }
    &::-webkit-scrollbar-thumb {
        border-radius: 2px;
        background-color: #66f;
    }
    article {
        padding: 0 20px;
        background: linear-gradient(to right top, #f66 50%, #f0f0f0 50%) no-repeat;
        background-size: 100% calc(100% - 298px + 5px);
        > * {
            position: relative;
            z-index: 9;
        }
    }
    h1 {
        line-height: 40px;
        text-align: center;
        font-weight: bold;
        font-size: 20px;
    }
    p {
        margin-top: 20px;
        line-height: 20px;
        text-indent: 2em;
    }
}
```

### 使用filter模拟Instagram滤镜

```css
HTML SCSSResult
EDIT ON
.instagram-filter {
    display: flex;
    flex-wrap: wrap;
    justify-content: space-between;
    align-content: space-between;
    width: 1635px;
    height: 630px;
    li {
        overflow: hidden;
        position: relative;
        width: 225px;
        height: 150px;
    }
    img {
        width: 100%;
        height: 100%;
    }
    p {
        position: absolute;
        right: 0;
        bottom: 0;
        padding: 0 10px;
        width: fit-content;
        height: 30px;
        background-color: #000;
        filter: none;
        line-height: 30px;
        color: #fff;
    }
}
.obscure {
    filter: brightness(80%) grayscale(20%) contrast(1.2) opacity(.6);
}
```

## 绘制

### div描绘各种图形

> <div>配合其伪元素(::before、::after)通过clip、transform等方式绘制各种图形

### 使用mask雕刻镂空背景

### linear-gradient描绘波浪线

### linear-gradient描绘彩带

```css
.colour-bar {
    width: 500px;
    height: 50px;
    background-image: repeating-linear-gradient(90deg, #f66, #f66 50px, #66f 50px, #66f 100px);
}
```

### linear-gradient描绘方格背景

```css
.square-bg {
    width: 500px;
    height: 300px;
    background-image: linear-gradient(45deg, #eee 25%, transparent 25%, transparent 75%, #eee 75%),
        linear-gradient(45deg, #eee 25%, transparent 25%, transparent 75%, #eee 75%);
    background-position: 0 0, 20px 20px;
    background-size: 40px 40px;
}
```

### conic-gradient描绘饼图

```css
.pie-chart {
    border-radius: 100%;
    width: 300px;
    height: 300px;
    background-image: conic-gradient(#f66 0 25%, #66f 25% 30%, #f90 30% 55%, #09f 55% 70%, #3c9 70% 100%);
}
```

### 使用box-shadow描绘单侧投影

```css
.aside-shadow {
    display: flex;
    justify-content: center;
    align-items: center;
    border: 1px solid;
    width: 100px;
    height: 100px;
    box-shadow: -7px 0 5px -5px #f90;
    font-weight: bold;
    font-size: 30px;
    color: #f90;
}
```

### 使用filter描绘头像彩色阴影

> 通过`filter:blur() brightness() opacity()`模拟阴影效果

```css
$avatar: "https://yangzw.vip/static/codepen/thor.jpg";

.avatar-shadow {
    position: relative;
    border-radius: 100%;
    width: 200px;
    height: 200px;
    background: url($avatar) no-repeat center/cover;
    &::after {
        position: absolute;
        left: 0;
        top: 10%;
        z-index: -1;
        border-radius: 100%;
        width: 100%;
        height: 100%;
        background: inherit;
        filter: blur(10px) brightness(80%) opacity(.8);
        content: "";
        transform: scale(.95);
    }
}
```

### box-shadow裁剪图像

### outline描绘内边框

> 通过`outline`设置轮廓进行描边，可设置`outline-offset`设置内描边

## 组件

### 迭代计数器

### 下划线跟随导航栏

```html
<div class="bruce flex-ct-x">
    <ul class="underline-navbar">
        <li>Alibaba阿里巴巴</li>
        <li>Tencent腾讯</li>
        <li>Baidu百度</li>
        <li>Jingdong京东</li>
        <li>Ant蚂蚁金服</li>
        <li>Netease网易</li>
    </ul>
</div>


```

```css
.underline-navbar {
    display: flex;
    li {
        position: relative;
        padding: 10px;
        cursor: pointer;
        font-size: 20px;
        color: #09f;
        transition: all 300ms;
        &::before {
            position: absolute;
            left: 100%;
            top: 0;
            border-bottom: 2px solid transparent;
            width: 0;
            height: 100%;
            content: "";
            transition: all 300ms;
        }
        &:active {
            background-color: #09f;
            color: #fff;
        }
        &:hover {
            &::before {
                left: 0;
                top: 0;
                z-index: -1;
                border-bottom-color: #09f;
                width: 100%;
                transition-delay: 100ms;
            }
            & + li::before {
                left: 0;
            }
        }
    }
}
```

### 气泡背景墙

```html
HTML SCSSResult
EDIT ON
<div class="bruce">
    <ul class="bubble-bgwall">
        <li>Love</li>
        <li>Love</li>
        <li>Love</li>
        <li>Love</li>
        <li>Love</li>
        <li>Love</li>
        <li>Love</li>
        <li>Love</li>
        <li>Love</li>
        <li>Love</li>
    </ul>
</div>
```

```css
.bruce {
    background-image: linear-gradient(270deg, #8146b4, #6990f6);
}
.bubble-bgwall {
    overflow: hidden;
    position: relative;
    margin: 0 auto;
    width: 1200px;
    height: 100%;
    li {
        display: flex;
        position: absolute;
        bottom: -200px;
        justify-content: center;
        align-items: center;
        border-radius: 10px;
        width: 50px;
        height: 50px;
        background-color: rgba(#fff, .15);
        color: #ccc;
        animation: bubble 15s infinite;
        &:nth-child(1) {
            left: 10%;
        }
        &:nth-child(2) {
            left: 20%;
            width: 90px;
            height: 90px;
            animation-duration: 7s;
            animation-delay: 2s;
        }
        &:nth-child(3) {
            left: 25%;
            animation-delay: 4s;
        }
        &:nth-child(4) {
            left: 40%;
            width: 60px;
            height: 60px;
            background-color: rgba(#fff, .3);
            animation-duration: 8s;
        }
        &:nth-child(5) {
            left: 70%;
        }
        &:nth-child(6) {
            left: 80%;
            width: 120px;
            height: 120px;
            background-color: rgba(#fff, .2);
            animation-delay: 3s;
        }
        &:nth-child(7) {
            left: 32%;
            width: 160px;
            height: 160px;
            animation-delay: 2s;
        }
        &:nth-child(8) {
            left: 55%;
            width: 40px;
            height: 40px;
            font-size: 12px;
            animation-duration: 15s;
            animation-delay: 4s;
        }
        &:nth-child(9) {
            left: 25%;
            width: 40px;
            height: 40px;
            background-color: rgba(#fff, .3);
            font-size: 12px;
            animation-duration: 12s;
            animation-delay: 2s;
        }
        &:nth-child(10) {
            left: 85%;
            width: 160px;
            height: 160px;
            animation-delay: 5s;
        }
    }
}
@keyframes bubble {
    0% {
        opacity: .5;
        transform: translateY(0) rotate(45deg);
    }
    25% {
        opacity: .75;
        transform: translateY(-400px) rotate(90deg);
    }
    50% {
        opacity: 1;
        transform: translateY(-600px) rotate(135deg);
    }
    100% {
        opacity: 0;
        transform: translateY(-1000px) rotate(180deg);
    }
}
```

### 滚动指示器

```css
.scroll-indicator {
    position: relative;
    overflow: hidden;
    border: 1px solid #66f;
    width: 500px;
    height: 300px;
    &::after {
        position: absolute;
        left: 0;
        right: 5px;
        top: 2px;
        bottom: 0;
        background-color: #fff;
        content: "";
    }
}
.article {
    overflow: auto;
    height: 100%;
    &::-webkit-scrollbar {
        width: 5px;
    }
    &::-webkit-scrollbar-track {
        background-color: #f0f0f0;
    }
    &::-webkit-scrollbar-thumb {
        border-radius: 2px;
        background-color: #66f;
    }
    article {
        padding: 0 20px;
        background: linear-gradient(to right top, #f66 50%, #f0f0f0 50%) no-repeat;
        background-size: 100% calc(100% - 298px + 5px);
        > * {
            position: relative;
            z-index: 9;
        }
    }
    h1 {
        line-height: 40px;
        text-align: center;
        font-weight: bold;
        font-size: 20px;
    }
    p {
        margin-top: 20px;
        line-height: 20px;
        text-indent: 2em;
    }
}
```

### 故障文本

```css
.bruce {
    background-color: #000;
}
.fault-text {
    position: relative;
    font-weight: bold;
    font-size: 100px;
    color: #fff;
    &::before,
    &::after {
        overflow: hidden;
        position: absolute;
        top: 0;
        background-color: #000;
        clip: rect(0, 900px, 0, 0);
        color: #fff;
        content: attr(data-text);
        animation: shake 3s linear infinite alternate-reverse;
    }
    &::before {
        left: -2px;
        text-shadow: 1px 0 #09f;
    }
    &::after {
        left: 2px;
        text-shadow: -1px 0 #f66;
        animation-duration: 2s;
    }
}
@keyframes shake {
    $steps: 20;
    @for $i from 0 through $steps {
        #{percentage($i * (1 / $steps))} {
            clip: rect(random(100) + px, 9999px, random(100) + px, 0);
        }
    }
}
```

### 换色器

> 通过拾色器改变图像色相的换色器

```css
<div class="bruce">
    <div class="color-changer">
        <input type="color" value="#ff6666">
        <img src="https://yangzw.vip/static/codepen/car.jpg">
    </div>
</div>

.color-changer {
    overflow: hidden;
    position: relative;
    height: 100%;
    input {
        position: absolute;
        width: 100%;
        height: 100%;
        cursor: pointer;
        mix-blend-mode: hue;
    }
    img {
        width: 100%;
        height: 100%;
        object-fit: cover;
    }
}
```

### 状态悬浮球

```html
<div class="bruce flex-ct-x">
    <div class="state-ball warning">
        <div class="wave"></div>
    </div>
</div>
.state-ball {
    overflow: hidden;
    position: relative;
    padding: 5px;
    border: 3px solid #3c9;
    border-radius: 100%;
    width: 150px;
    height: 150px;
    background-color: #fff;
    &::before,
    &::after {
        position: absolute;
        left: 50%;
        top: 0;
        z-index: 20;
        margin-left: -100px;
        width: 200px;
        height: 200px;
        content: "";
    }
    &::before {
        margin-top: -150px;
        border-radius: 45%;
        background-color: rgba(#fff, .5);
        animation: rotate 10s linear -5s infinite;
    }
    &::after {
        margin-top: -160px;
        border-radius: 40%;
        background-color: rgba(#fff, .8);
        animation: rotate 15s infinite;
    }
    &.warning {
        border-color: #f90;
        .wave {
            background-image: linear-gradient(-180deg, #f0c78a 13%, #f90 91%);
        }
    }
    &.danger {
        border-color: #f66;
        .wave {
            background-image: linear-gradient(-180deg, #f78989 13%, #f66 91%);
        }
    }
}
.wave {
    position: relative;
    border-radius: 100%;
    width: 100%;
    height: 100%;
    background-image: linear-gradient(-180deg, #af8 13%, #3c9 91%);
}
@keyframes rotate {
    from {
        transform: rotate(0);
    }
    to {
        transform: rotate(1turn);
    }
}
```

### 票券

```html
<div class="bruce flex-ct-x">
    <div class="mall-ticket">
        <h3>100元</h3>
        <p>网易考拉代金券</p>
    </div>
</div>

.mall-ticket {
    display: flex;
    position: relative;
    width: 300px;
    height: 100px;
    background: radial-gradient(circle at right top, transparent 10px, #f66 0) top left/100px 51% no-repeat,
        radial-gradient(circle at right bottom, transparent 10px, #f66 0) bottom left/100px 51% no-repeat,
        radial-gradient(circle at left top, transparent 10px, #ccc 0) top right/200px 51% no-repeat,
        radial-gradient(circle at left bottom, transparent 10px, #ccc 0) bottom right/200px 51% no-repeat;
    filter: drop-shadow(2px 2px 2px rgba(#fff, .2));
    line-height: 100px;
    text-align: center;
    color: #fff;
    &::before {
        position: absolute;
        left: 100px;
        top: 0;
        bottom: 0;
        margin: auto;
        border: 1px dashed #66f;
        height: 80px;
        content: "";
    }
    &::after {
        position: absolute;
        left: 100%;
        top: 0;
        width: 5px;
        height: 100%;
        background-image: linear-gradient(180deg, #ccc 5px, transparent 5px, transparent),
            radial-gradient(10px circle at 5px 10px, transparent 5px, #ccc 5px);
        background-size: 5px 15px;
        content: "";
    }
    h3 {
        width: 100px;
        font-size: 30px;
    }
    p {
        flex: 1;
        font-weight: bold;
        font-size: 18px;
    }
}
```

