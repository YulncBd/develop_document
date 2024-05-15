## CSS基础

### css的创建方式

```html
<!-- 外部样式：单独定义一个css文件，然后在需要的页面用<link>引入 -->
<link ref="stylesheet" type="text/css" href="mystyle.css" />

<!-- 内部样式：通过<style>创建 -->
<style>
  .label {
    color: red;
  }
</style>

<!-- 内联样式：直接在元素中使用 -->
<p style="color: red;">学习VUE</p>

<!-- 如果多种css样式同时使用，其优先级是：内联>内部>外部>浏览器默认 -->
```

### 选择器 id，class与属性

```html
<p id="para1">hello</p>
<p class="para2">hello</p>
<p title="hello">hello</p>
<a title="world">world</a>
<div title="hello world">hello world</div>
<!-- id 用 # -->
<!-- class 用 . -->
<!-- 属性用 [] -->
<!-- 一般在css中用class，javascript中用id -->
<style>
  #para1 {
    color: red;
  }
  .para2 {
    color: blue;
  }
  /* 所有包含title的元素变为红色 */
  [title] {
    color: red;
  }
  /* title=hello的元素字体大小为12px */
  [title='hello'] {
    font-size: 12px;
  }
  /* title的值包含hello的元素变为蓝色 */
  [title~='hello'] {
    color: blue;
  }
</style>
```

### css背景

```html
<style>
  .class1 {
    /* 背景颜色 */
    background-color: #e0ffff;
    /* 背景图片 */
    background-image: url('xxxx.png');
    /* 背景图片重复方式 */
    background-repeat: no-repeat;
    /* 背景图是固定还是随页面滚动，默认滚动 */
    background-attachment: fixed;
    /* 背景图的起始位置 */
    background-position: left top;
    /* 上面所有属性的简写，其顺序依次是：color image repeat attachment position */
    background: #ffffff url('img_tree.png') no-repeat right top;
  }
</style>
```

### css文本和字体

```html
<style>
  /* 设置文本样式 */
  .text {
    /* 字体颜色 */
    color: red;
    /* 字体布局 */
    text-align: center;
    /* 主要用来清除链接下划线 */
    text-decoration: none;
    /* 文本的大小写（包括首字母和所有字母） */
    text-transform: uppercase;
    /* 文本缩进 */
    text-indent: 50px;
    /* 文本的阴影 */
    text-shadow: 2px 2px #ff0000;
    /* 字间距 */
    word-spacing: 30px;
    /* 行高 */
    line-height: 200%;
  }
  /* 设置字体样式 */
  .font {
    /* 字体名字 */
    font-family: Times;
    /* 字体倾斜 */
    font-style: normal;
    /* 字体大小：通常用px，也可以用em 16px = 1em */
    font-size: 16px;
    /* 字体粗细 */
    font-weight: 700;
  }
</style>
```

### css链接

```html
<!-- 
链接有四个状态：同时有多个状态时，其设置顺序依次为：link visited hover active
a:link 未访问过的链接
a:visited 已访问过的链接
a:hover 鼠标放在链接上时
a:active 链接被点击的那一刻 
-->
<style>
  a:link {
    color: #000000;
  } /* 未访问链接*/
  a:visited {
    color: #00ff00;
  } /* 已访问链接 */
  a:hover {
    color: #ff00ff;
  } /* 鼠标移动到链接上 */
  a:active {
    color: #0000ff;
  } /* 鼠标点击时 */
</style>
```

### css列表

```html
<!-- 无序列表，用小黑点或小方块 -->
<ul>
  <li>name1</li>
  <li>name2</li>
</ul>
<!-- 有序列表，用数字或字母 -->
<ol>
  <li>name1</li>
  <li>name2</li>
</ol>

<style>
  ul {
    list-style-type: circle;
  }

  ol {
    list-style-type: upper-roman;
  }
</style>
```

### css表格

```html
<!-- table表格 tr表格的一行 th表头单元格 td单元格 -->
<table>
  <tr>
    <th>Name</th>
    <th>Age</th>
  </tr>
  <tr>
    <td>Tom</td>
    <td>20</td>
  </tr>
</table>
<style>
  table,
  th,
  td {
    border: 1px solid black;
  }
</style>
```

### box模型

```html
<!--
css盒模型，从外到内： margin border padding content
outline 外边框，在border的外面，不占用具体的空间 
margin和padding：值可以是10px，也可以是10%，其顺序为 上 右 下 左（顺时针） -->

<style>
  .border {
    border-width: 1px;
    /* 边框样式， 实线/虚线/双重/3d等 */
    border-style: none;
    border-color: #fff;
    border: 5px solid red;
    /* 单独设置某一个边 */
    border-top: 5px solid red;
  }
  .margin {
    margin: 20px 20px 20px 20px;
    padding: 20px 20px 20px 20px;
  }
</style>
```

### css分组和嵌套选择器

```html
<!-- 分组：所有的h1，h2和p标题的字体颜色都会是红色 -->
<style>
  h1,
  h2,
  p {
    color: red;
  }
  /* 嵌套： */
  /* 为所有class='marked'元素内的p元素设置样式 */
  .marked p {
    color: white;
  }
  /* 为所有class='marked'的p元素设置样式 */
  p.marked {
    text-decoration: underline;
  }
</style>
```

### 尺寸

```html
<!-- 设置元素的宽高和最小最大宽度 -->
<style>
  .size {
    width: 100px;
    height: 30%;
    min-height: 20%;
    max-width: 300px;
  }
</style>
```

### display 与 visibility

```html
<!-- display:none 隐藏某个元素，隐藏后不占空间 -->
<!-- visibility：hidden 隐藏某个元素，隐藏后仍占用空间 -->
<!-- 块与内联元素 -->
<!-- 块：占用全部宽度，前后都是换行符，如<h1><div><p> -->
<!-- 内联元素：只占用必要的宽度，不强制换行，如<span><a> -->
<style>
  /* 可通过display更改块和内联元素 */
  .class {
    display: block;
    display: inline;
  }
</style>
```

### css定位position

```html
<!-- 
position 属性的五个值：
static：默认，没有定位
fixed：固定位置，不会随窗口移动
relative：相对定位
absolute：绝对定位
sticky：粘性定位，基于用户滚动位置来定位
-->

<style>
  .pos {
    position: absolute;
    top: 100px;
    left: 10px;
    /* 重叠元素，通过z-index来指定堆叠顺序 */
    z-index: -1;
    /* 元素溢出时如何处理 hidden scroll等 */
    overflow: hidden;
  }
</style>
```

### float 一般用于图片

```html
<!-- 
float 会使元素水平移动，不能上下移动
float 后面的元素会将其围绕
多个float元素在一起，如果空间足够会彼此相邻
清除float需要使用clear
-->
<style>
  img {
    float: right;
  }
</style>
```

### 对齐

```html
<style>
  /* 水平居中：使用margin:auto，必须设置width否则不生效，必须要是块元素或设置display: block */
  .center {
    margin: auto;
    width: 50%;
    padding: 10px;
  }
  /* 水平文本居中 */
  .text-center {
    text-align: center;
  }
  /* 图片水平居中, display:block; margin:auto width:200px */
  .img-center {
    display: block;
    margin: auto;
    width: 200px;
  }
  /* 左右对齐，position或float */
  .right {
    position: absolute;
    right: 0px;
    width: 100px;
  }
  .left {
    float: left;
    width: 100px;
  }
  /* 上下居中对齐，padding */
  .center-v {
    padding: 20px 0;
  }
  /* 垂直居中 padding + text-align */
  .center-hv {
    padding: 20px 0;
    text-align: center;
  }
  /* 垂直居中 position + transform */
  /* top 和left 设置50%，然后通过transform再平移内容的50%达到居中的效果 */
  .center-hv2 {
    margin: 0;
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    -ms-transform: translate(-50%, -50%);
    -webkit-transform: translate(-50%, -50%);
  }
</style>
```

### 伪类和伪元素

```html
<!-- 伪类：已有元素处于某个状态时为其添加样式（本身不存在，只有在特定情况下才触发的样式） -->
<!-- 伪元素：创建一个不在dom树的元素并为其添加样式，虽然可见但是其不在dom树中 -->
<!-- CSS3中伪类用但冒号， 伪元素用双冒号 -->
<style>
  /* 伪类 */
  a:hover {
    background-color: red;
  }
  /* 伪元素 */
  /* 在每个<p>元素之前插入内容 */
  p::before {
    content: 'p.before';
    color: red;
  }
  /* 选择器匹配作为任何元素的第一个子元素的<p>元素 */
  p::first-child {
    color: blue;
  }
</style>
```

### css 导航栏

<!-- 使用 ul 和 li -->

<!-- 垂直导航栏 -->

```html
<ul>
  <li><a href="#home">主页</a></li>
  <li><a href="#news">新闻</a></li>
  <li><a href="#contact">联系</a></li>
</ul>

<style>
  ul {
    /* 移除列表前的小标志 */
    list-style-type: none;
    /* 将浏览器默认填充设置为0 */
    margin: 0;
    padding: 0;
    /* 导航固定 */
    position: fixed;
    /* 如果导航栏过多，允许滚动 */
    overflow: auto;
  }
  li a {
    /* 设置成块元素，让整个块元素可点击，而不是只有文字点击 */
    display: block;
    width: 100px;
    text-decoration: none;
  }
  /* 鼠标移动到选项时修改背景色 */
  li a:hover {
    background-color: red;
    color: yellow;
  }
  li {
    border-bottom: 1px solid red;
  }
  /* 最后一个没有下边框 */
  li:last-child {
    border-bottom: none;
  }
</style>
```

<!-- 水平导航栏 -->

```html
<!-- inline 或 float -->
<ul>
  <li><a href="#home">主页</a></li>
  <li><a href="#news">新闻</a></li>
  <li><a href="#contact">联系</a></li>
</ul>
<style>
  li {
    /* 使用inline 或 float */
    display: inline;
    /* float： left */
  }
  a {
    /* 设置块元素，设置宽度并增加点击区域 */
    display: block;
    width: 100px;
  }
</style>
```

### 下拉菜单 和 提示文字

<!-- 鼠标移动到元素上后，出现下拉菜单或提示文字  display visibility opacity -->

<!-- 下拉菜单 -->

```html
<div class="dropdown">
  <span>标题</span>
  <div class="dropdown-item">
    <div>item1</div>
    <div>item2</div>
  </div>
</div>

<style>
  .dropdown {
    /* relative 出现在内容下方， absolute 出现在右上角 */
    position: relative;
    /* 允许在元素上设置宽高，但是不会自动换行，是inline和block的结合体 */
    display: inline-block;
    /* 鼠标样式 */
    cursor: pointer;
  }
  .dropdown-item {
    /* 先隐藏 */
    display: none;
    position: absolute;
    min-width: 100px;
    box-shadow: 0px 10px 10px 10px red;
    padding: 2px;
  }
  /* 鼠标移动到dropdown上时显示下拉菜单 */
  .dropdown:hover .dropdown-item {
    display: block;
  }
</style>
```

 <!-- 文字提示 tooltip -->

```html
<div class="tooltip">
  提示信息
  <span class="tooltiptext">具体的提示信息内容</span>
</div>

<style>
  .tooltip {
    position: relative;
    display: inline-block;
  }
  .tooltiptext {
    visibility: hidden;
    width: 100px;
    color: #fff;
    background-color: black;
  }
  .tooltiptext {
    visibility: hidden;
    width: 120px;
    bottom: 100%;
    left: 50%;
    margin-left: -60px;
  }

  /* 添加箭头 */
  /* 这其实是一个正方形，然后设置其border，让其他三个border隐藏，达到三角形的效果 */
  .tooltiptext::after {
    /* content 必须要设置 */
    content: '';
    position: absolute;
    /* top:100% 箭头将显示在工具底部 */
    top: 100%;
    left: 50%;
    /* border-width 设置箭头大小，如果修改其值，margin-left也要改变 */
    margin-left: -5px;
    border-width: 5px;
    border-style: solid;
    /* 将内容转为箭头，顶部设置为黑色，其他透明 */
    border-color: black transparent transparent transparent;
  }

  .tooltip:hover .tooltiptext {
    visibility: visible;
  }
</style>
```

### 图像拼合技术

```html
<!-- 在CSS中可以显示图片的一部分 -->
<!-- tran.gif 是一个透明的图像 -->
<div>
  <img class="home" src="assets/images/tran.gif" />
  <img class="next" src="assets/images/tran.gif" />
</div>

<style>
  img.home {
    width: 44px;
    height: 44px;
    background: url('assets/iamges/img.gif') 0 0;
  }
  img.next {
    width: 44px;
    height: 44px;
    /* 左 -90 上 0 */
    background: url('assets/iamges/img.gif') -90px 0;
  }
</style>
```

### 媒体类型

```html
<!-- 允许在不同的媒体上呈现不同的样式 -->
<!-- screen 显示器 print 打印机 -->
<style>
  @media screen {
    p.text {
      font-size: 14px;
    }
  }
  @media print {
    p.text {
      font-size: 15px;
    }
  }
  @media screen, print {
    p.text {
      font-weight: 700;
    }
  }
</style>
```

### !importment

<!-- 使用 !importment 后，此声明会覆盖其他声明，应尽量避免使用。 -->

## CSS3 教程

### 圆角

```html
<style>
  div {
    border: 2px solid red;
    box-shadow: 10px 10px 10px red;
    /* 可以单独设置每个角，也可以统一设置 */
    border-radius: 12px;
    /* 椭圆 */
    border-radius: 50%;
    border-radius: 15px/50px;
  }
</style>
```

### 背景

```html
<style>
  div {
      background: url('xxx.png');
      background-size: 100px 80px; // 大小
      background-repeat: no-repeat;
      background-origin: content-box; // content-box padding-box border-box
      /* 可以设置多个背景 */
      background: url('xxx.png'), url('xxx2.png');

  }
</style>
```

### 渐变gradients

Linear Gradients 线性变化
Radual Gradients 中心变化

```html
<style>
  div {
    background-image: linear-gradient(#f32f32, #333333);
    /* 从左到右 */
    background-image: linear-gradient(to right, #f32f32, #333333);
    /* 对角 */
    background-image: linear-gradient(to bottom right, #f32f32, #333333);
    /* 使用角度 根据坐标系判断 0deg从上到下 90deg从左到右  -90deg = 270deg */
    background-image: linear-gradient(-90deg, #f32f32, #333333);
    /* 重复的线性变化 */
    background-image: repeating-linear-gradient(red, yellow 10%, green 20%);
  }

  /* 中心变化 */
  div {
    background-image: radial-gradient(red, yellow, green);
    /* 设置形状 circle 表示圆形，ellipse 表示椭圆形*/
    background-image: radial-gradient(circle, red, yellow, green);
  }
</style>
```

### 文本效果

```html
<style>
  div {
    white-space: nowrap;
    width: 12em;
    overflow: hidden;
  }

  text {
    /* 阴影 */
    text-shadow: 5px 5px 5px red;
    /* 处理溢出文本 ellipsis 省略 clip裁剪，父组件使用white-space width overflow */
    text-overflow: ellipsis;
    /* 允许单词换行 */
    word-wrap: break-word;
    /* 单词拆分换行规则 keep-all break-all */
    word-break: keep-all;
  }

  /* 引入字体, src：是字体文件路径 */
  @font-face {
    font-family: myFontName;
    src: url('xxxxx.woff');
  }
  @font-face {
    font-family: myFontName;
    src: url('xxxxx.woff');
    font-weight: bold;
  }
</style>
```

### 2D和3D转换：平面旋转，移动，缩放等

<!-- IE/Firefox/Opera支持transform，Chrome/Safari 要加前缀-webkit-，IE9要加前缀-ms- -->

```html
<style>
  div {
      width 100px;
      height: 40px;
      /* 旋转 值是正的顺时针， 值是负的逆时针 */
      transform: rotate(30deg);
      -ms-transform: rotate(30deg);
      -webkit-transform: rotate(30deg);
      /* 平移 向有平移50px，向下平移60px  */
      transform: translate(50px, 60px);
      -ms-transform:translate(50px, 50px);
      -webkit-transform: translate(50px, 50px);
      /* 缩放 宽度放大2倍 高度放大3倍 */
      transform: scale(2,3);
      -ms-transform:scale(2,3);
      -webkit-transform:scale(2,3);
      /* skew 参数1 x轴倾斜角度 参数2 y轴倾斜角度， 也可以用skewX 和 skewY 来单独设置x轴和y轴 */
      transform: skew(30deg,20deg);
      -ms-transform: skew(30deg,20deg);
      -webkit-transform: skew(30deg,20deg);
      /* matrix(scaleX(),skewY(),skewX(),scaleY(),translateX(),translateY())*/
      transform: matrix(0.8,0.5,-0.5,0.8,0,0);
      -ms-transform: matrix(0.8,0.5,-0.5,0.8,0,0);
      -webkit-transform: matrix(0.8,0.5,-0.5,0.8,0,0);
  }

  div {
    /* 沿X轴旋转 */
    transform: rotateX(120deg);
    -ms-transform: rotateX(120deg);
    -webkit-transform: rotateX(120deg);
    /* 沿y轴旋转 */
    transform: rotateY(120deg);
    -ms-transform: rotateY(120deg);
    -webkit-transform: rotateY(120deg);
  }
</style>
```

### 过度

<!--
元素从一种样式变为另一种样式的过程，不许要明确以下两点：
指定要添加效果的CSS属性
指定效果的持续时间
-->

```html
<style>
  /* transition 监听的属性是width 效果持续时间2s */
  div {
    width: 100px;
    height: 100px;
    background: red;
    transition: width 2s;
    -ms-transition: width 2s;
    -webkit-transiton: width 2s;
  }
  /* 鼠标在上面时修改宽度 */
  div:hover {
    width: 300px;
  }

  /* 可以改变多个值，用逗号隔开 */
  div {
    width: 100px;
    height: 100px;
    background: red;
    transition:
      width 2s,
      height 2s,
      transform 2s;
    -webkit-transition:
      width 2s,
      height 2s,
      transform 2s;
    -ms-transition:
      width 2s,
      height 2s,
      transform 2s;
  }
  div:hover {
    width: 200px;
    height: 200px;
    transform: rotate(180deg);
    -webkit-transform: rotate(180deg);
    -ms-transform: rotate(180deg);
  }
</style>
```

### 动画 keyframs

```html
<div></div>

<style>
  div {
    width: 100px;
    height: 100px;
    background: red;
    animation: myfirst 5s;
    -ms-animation: myfirst 5s;
    -webkit-animation: myfirst 5s;
  }

  /* 同时进行多个属性动画 */
  @keyframes myfirst {
    0% {
      background: red;
      left: 0px;
      top: 0px;
    }
    25% {
      background: yellow;
      left: 200px;
      top: 0px;
    }
    50% {
      background: blue;
      left: 200px;
      top: 200px;
    }
    75% {
      background: green;
      left: 0px;
      top: 200px;
    }
    100% {
      background: red;
      left: 0px;
      top: 0px;
    }
  }

  @-webkit-keyframes myfirst {
    0% {
      background: red;
      left: 0px;
      top: 0px;
    }
    25% {
      background: yellow;
      left: 200px;
      top: 0px;
    }
    50% {
      background: blue;
      left: 200px;
      top: 200px;
    }
    75% {
      background: green;
      left: 0px;
      top: 200px;
    }
    100% {
      background: red;
      left: 0px;
      top: 0px;
    }
  }
</style>
```

### 多列

<!--
将文本内容设计成向报纸一样排列
column-count // 几列
column-gap // 间距
column-style-width // 两列之间的边框
-->

### 调整尺寸

<!-- resize // 是否允许用户调整大小 -->
<!-- box-sizing // content-box border-box -->

### 分页

```html
<ul class="pagination">
  <li><a href="#"><<</a></li>
  <li><a href="#">1</a></li>
  <li><a class="active" href="#">2</a></li>
  <li><a href="#">3</a></li>
  <li><a href="#">4</a></li>
  <li><a href="#">>></a></li>
</ul>
<style>
  ul.pagination {
    display: inline-block;
    padding: 0px;
    margin: 0px;
  }

  ul.pagination li {
    display: inline;
  }
  ul.pagination li a {
    color: black;
    float: left;
    padding: 8px 16px;
    text-decoration: none;
    border: 1px solid #ddd;
  }
  ul.pagination li a:active {
    background-color: red;
    color: white;
  }
  ul.pagination li a:hover:not(.active) {
    background-color: #ddd;
  }
  ul.pagination li:first-child a {
    border-top-left-radius: 6px;
    border-bottom-left-radius: 6px;
  }
  ul.pagination li:last-child a {
    border-top-right-radius: 6px;
    border-bottom-right-radius: 6px;
  }
</style>
```

### 弹性盒子 flex

```html
<style>
  div {
    /* 开启弹性布局 */
    display: flex;
    /* 布局方式 row|row-reverse水平布局，column|column-reverse垂直布局*/
    flex-direction: row;
    /* 主轴线对齐方式：row是x轴 column是y轴 flex-start | flex-end | center | space-between | space-around */
    justify-content: center;
    /* 侧轴线对齐方式：row是y轴 column是x轴 flex-start | flex-end | center | space-between | space-around */
    align-items: center;
    /*  元素换行方式 flex-wrap: nowrap（单行）|wrap（自动换行）|wrap-reverse（反wrap）|initial|inherit; */
    flex-wrap: nowrap;
    /* 搭配flex-wrap使用，设置的是各行的对齐方式 align-content: flex-start | flex-end | center | space-between | space-around | stretch */
    align-content: center;
    /* 搭配display: flex 完美的居中布局 */
    margin：auto;
    /* 弹性盒子分配占比 flex: 1 */
    flex: auto;
  }
</style>
```

### 多媒体查询

<!--
在CSS2 中通过@media可以针对不同媒体类型制定不同规则，但是这还不够友好
如果expressions返回true 就展示对于的样式
not 用来排除某些特殊媒体设备 only用来针对某种特殊媒体类型
@media not|only mediatype and (expressions) {}
-->

```html
<style>
  /* 屏幕尺寸小于480px，背景色为红色 */
  @media screen and (max-width: 480px) {
    body {
      background: red;
    }
  }
  /* 屏幕尺寸大于480，背景色为黑色 */
  @media screen and (min-width: 480px) {
    body {
      background: black;
    }
  }
  /* 可以同时设置多个条件 */
  @media screen and (max-width: 1000px) and (min-width: 700px) {
    body {
      background: yellow;
    }
  }
</style>
```

### 网格布局 grid

```html
<style>
  .grid-container {
      /* grid或inline-grid 网格布局 */
      display: grid;
      /* 来创建列数 */
      grid-template-columns: auto auto auto auto;
      /* 引入fr 单位，等同flex， 创建4个等分的列*/
      grid-template-columns: 1fr 1fr 1fr 1fr;
      /* 来定义行高， 第一行100px 第二行300px */
      grid-template-rows：100px 300px;
      /* 设置间距 */
      grid-gap: 10px 20px;
      grid-row-gap:10px;
      grid-column-gap: 20px;
      /* 网格元素延主轴（水平）的分布 */
      justify-content: space-evenly;
        /* 设置垂直方向上元素的布局方式 */
      align-content: center;
  }

  .item1 {
      /* 网格线
      从上到下，从左到右。从1开始排序
      */
      /* row 是行 从最左侧开始，占两格 */
      grid-row-start: 1;
      grid-row-end: 3;
      /* column 是列 */
      /* grid-column 是grid-column-start 和 grid-column-end 的缩写 */
      grid-column: 1 / 5;
      /* 如果没有span 是从line1 开始到line5 结束，总共4列，加上span 则表示从line1 开始往右5列，总共5列+ */
      grid-column: 1 / span 5;
      grid-column-start: 1;
      grid-column-end: 5;
      /* 属性值依次是 grid-row-start, grid-column-start grid-row-end grid-column-end */
      grid-area: 1 / 2 / 5 / 6;
  }

  /* 网格元素命名 */
  .item2 {
    grid-area: myArea;
  }
  .grid-container {
    grid-template-areas: 'myArea myArea myArea myArea myArea';
    /* . 表示剩余的item */
    grid-template-areas: 'myArea myArea . . .'

  }
</style>
```
