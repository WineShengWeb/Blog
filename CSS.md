<!--
 * @Author: guoxinggang<guoxinggang@gsaxns.com>
 * @Version: 1.0
 * @Date: 2019-08-28 13:43:17
 * @LastEditTime: 2019-08-30 17:56:14
 * @Description: 
 -->

# <center>CSS 总结</center>

---

## 一、CSS概念

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;CSS 层叠样式表(英文全称：Cascading Style Sheets)是一种用来表现HTML（标准通用标记语言的一个应用）或XML（标准通用标记语言的一个子集）等文件样式的计算机语言。CSS不仅可以静态地修饰网页，还可以配合各种脚本语言动态地对网页各元素进行格式化。

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;CSS 能够对网页中元素位置的排版进行像素级精确控制，支持几乎所有的字体字号样式，拥有对网页对象和模型样式编辑的能力。

## 二、CSS 与 HTML 的结合方式

### 1.行内样式

通过标签的style属性,属性值为css内容；
如：<标签名  style="css内容"/>

    <p style="margin:0;padding:0;">123</p>

### 2.内嵌样式

一般写在head标签里，如：

    <style type="text/css">
        body{
            text-align: center;
            -webkit-user-select: none;
        }
        input[type=button]{
            width: 90px;
        }
        ul{display: none}
        #d1{
            font-family: "微软雅黑";
            background-image: url(img/HBuilder.png)
        }
    </style>

### 3.外链样式

新建一个css样式文件,在head标签里写link引入css样式文件；

    <link rel="stylesheet" type="text/css" href="css/test.css"/>

### 4.导入样式

使用@import导入样式文件，如：@import url(CSS文件路径地址);

    <style type="text/css">
        @import url(css/test.css)
    </style>

### 5.注释

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;注释用来为部分CSS代码添加额外的解释,或者用来组织浏览器解析一部分区域内的CSS代码.

语法：/* content */

    <style type="text/css">
        /* body{
            text-align: center;
            -webkit-user-select: none;
        } */
    </style>

## 三、选择器

### 1.通配选择器

- 语法：*{ css内容 }

<font color="red">注:不建议使用</font>

### 2.基本选择器

- 标签选择器.如:标签名{属性:属性值;}

    p{ margin：0; }

- 类选择器.如:.类名{属性:属性值;}

    .box{
        width：100px；
    }

  - 类选择器命名规则：
    - 不能用纯数字或者数字开头来定义类名
    - 不能使用特殊符号或者特殊符号开头（_除外）来定义类名
    - 禁止使用汉字来定义类名
    - 不推荐使用属性或者属性的值来定义类名
    - 定义类名时尽量语义化

- id选择器.如:#id名{属性:属性值;}

    #box{
        width：100px；
    }

### 3.伪选择器

- a:link(链接未被访问时的样式)

    如: a:link

- a:visited(链接被访问后的样式)

    如: a:visited

- a:hover(当鼠标悬浮在元素上方时的样式)

    如: a:hover

- a:active(向被激活的元素添加样式)

    如: a:active

- 顺序:hover要放在link和visited的后面,active要放在hover的后面

- :focus(获取焦点)

    如: 选择获得焦点的 input 元素。
    input:focus;    

- :before(在内容前加的内容)

    如: 在每个 p 元素的内容之前插入内容。
    p:before

- :after(在内容后加的内容,主要用于清除浮动)

    如: 在每个 p 元素的内容之后插入内容。
    p:after

- :first-letter(选择每行的第一个字)

    如: 选择每个 p 元素的首字母。
    p:first-letter

- :first-line(选择每行的第一行。)

    如: 选择每个 p 元素的首行。
    p:first-line
- :first-child(选择第一个子元素。)

    如: 选择属于父元素的第一个子元素的每个 p 元素。
    p:first-child

- :last-child(选择最后一个子元素)

    如: 选择属于其父元素最后一个子元素每个 p 元素。
    p:last-child

- :nth-child(n)(选择第n个元素)

    如: 选择属于其父元素的第二个子元素的每个 p 元素。
    p:nth-child(2)

- :nth-last-child(n)(选择倒数第n个元素)

    如: 选择倒数第二个 p 元素。
    p:nth-last-child(2)

- 在css3中伪元素用两个 :: 来表示，如：a::before。其中 ：代表伪类，两个 :: 表示伪元素。

### 4.组合选择器

- 群组选择器

    语法: 标签名,.class,#box{ css内容 }
    如：
    ```
    HTML,body,div,p,h1,ul{
        margin: 0;
        padding: 0;
    }
    ```

- 后代选择器

    <font color="red">注:两个元素必须是父与子的关系，可以隔代！</font>
    语法: 标签名 标签名{ css内容 }
    如: 
    ```
    ul li a{
        color: red;
    }
    ```

- 子元素选择器

    <font color="red">注:两个元素之间必须是父与子的关系,不能隔代，隔代无效！</font>
    语法: 标签名>标签名{ css内容 }
    如: 
    ```
    div>p{
        margin: 10px;
    }
    ```

### 5.选择器的优先级

<font color="red">默认样式<标签选择器<类选择器<ID选择器<行内样式<!importent(直接写在值后面)</font>

### 6.CSS的特性

- 层叠性

    当多个样式作用于同一个（同一类）标签时，样式发生了冲突，总是执行后边的代码(后边代码层叠(覆盖)前边的代码)。和标签调用选择器的顺序没有关系。

- 继承性

    继承性发生的前提是包含（嵌套关系）;
    <font color="red">文字的所有属性都可以继承。</font>
  - 特殊情况
    - h系列不能继承文字大小。
    - a标签不能继承文字颜色。

## 四、盒子模型

盒子模型是由：content(内容)、padding(内边距)、margin(外边距)、border(边框)四部分组成。

- 1.标准盒模型

    ![标准盒模型](https://images2017.cnblogs.com/blog/1265396/201711/1265396-20171119143703656-1332857321.png)
    在标准模型中，盒模型的宽高只是内容（content）的宽高，

- 2.IE盒模型

    ![IE盒模型](https://images2017.cnblogs.com/blog/1265396/201711/1265396-20171119144229156-49945808.png)
    在IE模型中盒模型的宽高是内容(content)+填充(padding)+边框(border)的总宽高。

- 3.二者互相转换

  - 标准模型: box-sizing:content-box;

  - IE模型: box-sizing:border-box;

- 4.弹性盒子

    &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;弹性盒子是 CSS3 的一种新的布局模式，是一种当页面需要适应不同的屏幕大小以及设备类型时确保元素拥有恰当的行为的布局方式。

    &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;引入弹性盒布局模型的目的是提供一种更加有效的方式来对一个容器中的子元素进行排列、对齐和分配空白空间。

    - 4.1弹性布局

      - display: flex;
      - 作用: 让当前元素形成弹性盒子
      - 特点：
        - 1.让一个子元素在弹性盒里面左右上下居中
		- 2.弹性盒里面的元素可以直接添加宽高
		- 3.弹性盒里面的元素都是沿着"主轴"排列(主轴:x轴或者y轴  默认x轴为主轴)

    - 4.2容器的属性

      - 1.flex-direction:属性决定主轴的方向（即项目的排列方向）。主轴的排列方向
        - flex-direction: row | row-reverse | column | column-reverse;
        - row（默认值）：主轴为水平方向，起点在左端。
        - row-reverse：主轴为水平方向，起点在右端。
        - column：主轴为垂直方向，起点在上沿。
        - column-reverse：主轴为垂直方向，起点在下沿。
      - 2.flex-wrap:默认情况下，项目都排在一条线（又称"轴线"）上。flex-wrap属性定义，如果一条轴线排不下，如何换行。控制子元素换行
        - flex-wrap: nowrap | wrap | wrap-reverse;
        - nowrap（默认）：不换行。
        - wrap：换行，第一行在上方。
        - wrap-reverse：换行，第一行在下方。
      - 3.flex-flow:flex-flow属性是flex-direction属性和flex-wrap属性的简写形式，默认值为row nowrap。
        - flex-flow: <flex-direction> || <flex-wrap>;
        - 
        - 
      - 4.justify-content:属性定义了项目在主轴上的对齐方式。主轴的对齐方式
        - justify-content: flex-start | flex-end | center | space-between | space-around;
        - flex-start（默认值）：左对齐
        - flex-end：右对齐
        - center： 居中
        - space-between：两端对齐，项目之间的间隔都相等。
        - space-around：每个项目两侧的间隔相等。所以，项目之间的间隔比项目与边框的间隔大一倍
      - 5.align-items:属性定义项目在交叉轴上如何对齐。具体的对齐方式与交叉轴的方向有关;侧轴的对齐方式
        - align-items: flex-start | flex-end | center | baseline | stretch;
        - flex-start：交叉轴的起点对齐。
        - flex-end：交叉轴的终点对齐。
        - center：交叉轴的中点对齐。
        - baseline: 项目的第一行文字的基线对齐。
        - stretch（默认值）：如果项目未设置高度或设为auto，将占满整个容器的高度。
      - 6.align-content:属性定义了多根轴线的对齐方式。如果项目只有一根轴线，该属性不起作用。
        - align-content: flex-start | flex-end | center | space-between | space-around | stretch;
        - flex-start：与交叉轴的起点对齐。
        - flex-end：与交叉轴的终点对齐。
        - center：与交叉轴的中点对齐。
        - space-between：与交叉轴两端对齐，轴线之间的间隔平均分布。
        - space-around：每根轴线两侧的间隔都相等。所以，轴线之间的间隔比轴线与边框的间隔大一倍。
        - stretch（默认值）：轴线占满整个交叉轴。
    - 4.3项目的属性
      - 1.order:属性定义项目的排列顺序。数值越小，排列越靠前，默认为0。
        - order: <integer>;/* 整数 */
      - 2.flex-grow:属性定义项目的放大比例，默认为0，即如果存在剩余空间，也不放大。
        - 如果所有项目的flex-grow属性都为1，则它们将等分剩余空间（如果有的话）。
        - 如果一个项目的flex-grow属性为2，其他项目都为1，则前者占据的剩余空间将比其他项多一倍。
        - flex-grow: <number>; /* default 0 */
      - 3.flex-shrink:属性定义了项目的缩小比例，默认为1，即如果空间不足，该项目将缩小。
        - 如果所有项目的flex-shrink属性都为1，当空间不足时，都将等比例缩小。
        - 如果一个项目的flex-shrink属性为0，其他项目都为1，则空间不足时，前者不缩小。
        - 负值对该属性无效。
        - flex-shrink: <number>; /* default 1 */
      - 4.flex-basis:属性定义了在分配多余空间之前，项目占据的主轴空间（main size）。
        - 浏览器根据这个属性，计算主轴是否有多余空间。它的默认值为auto，即项目的本来大小。
        - 它可以设为跟width或height属性一样的值（比如350px），则项目将占据固定空间。
        - flex-basis: <length> | auto; /* default auto */
      - 5.flex:属性是flex-grow, flex-shrink 和 flex-basis的简写，默认值为0 1 auto。后两个属性可选。
        - 该属性有两个快捷值：auto (1 1 auto) 和 none (0 0 auto)。
        - 建议优先使用这个属性，而不是单独写三个分离的属性，因为浏览器会推算相关值。
        - flex: none | [ <'flex-grow'> <'flex-shrink'>? || <'flex-basis'> ]
      - 6.align-self属性允许单个项目有与其他项目不一样的对齐方式，可覆盖align-items属性。
        - 默认值为auto，表示继承父元素的align-items属性，如果没有父元素，则等同于stretch。
        - 该属性取6个值，除了auto，其他都与align-items属性完全一致。
        - align-self: auto | flex-start | flex-end | center | baseline | stretch;

## 五、浮动

- 浮动：想要多个元素在一行显示,用浮动。
- float:  left   |   right
- 特点：
    元素浮动之后不占据原来的位置（脱标）
    浮动的盒子在一行上显示
- 作用:
    文本绕图
    制作导航
    网页布局

- 清除浮动
  - 当父盒子没有定义高度，嵌套的盒子浮动之后，下边的元素发生位置错误。
  - 清除浮动不是不用浮动，清除浮动产生的不利影响。
  - 清除浮动的方法:clear: left  |  right  |  both
    工作里用的最多的是clear:both;
  - 伪元素清除法；
  ```
    clear：after{
        content：'';
        display: block;
        height: 0;
        clear: both;
    }
  ```

## 六、定位

- 定位:用left / right / top / bottom 改变位置,用z-index值改变层级,值越大,越靠前
- 相对定位:position:relative;
  - 特点
    - 1.相对定位占位置,
	- 2.以自身位置为标准的;
- 绝对定位:position:absolute;
  - 特点:
    - 1.绝对定位不占据位置,
    - 2.以它定位的父元素为标准,父元素没有定位,以body为标准
- 固定定位:position:fixed;
    - 特点
      - 固定定位不占位置,以窗口为标准来定位的

## 七、块级元素

- 块元素
  - display:block;
  - 特点
    1.独占一整行,可以设置宽高;
    2.不设置它的宽度时,它的宽度是父元素的宽度,不设置高度时,它的高度是内容的高度.
    3.常用的块元素：
    ```
    <div> <p> <h1>-<h6> <ol> <ul> <dl> <table> <address> <blockquote> <form>
    ```

- 行内元素
  - display:inline;
  - 特点
    1.多个标签占一行,不能设置宽高;
    2.宽和高为内容的宽高.
    3.常用的行内元素：
    ```
    <a> <span> <br> <i> <em> <strong> <label> <q> <cite> <code> <var>
    ```
  
- 行内块元素
  - display:inline-block;
  - 特点
    1.多个占一行,可以设置宽高.
    2.常用的行内块元素：
    ```
    <img> <input>,textarea(文本域)
    ```
- 隐藏属性
    display:none;隐藏不占位置;
	visibility:hidden;隐藏占位置;

## 八、边距

- 外边距

  - margin-left   | right  |  top  |  bottom
  - 外边距连写
    1. margin: 20px;    上下左右外边距20PX
    2. margin: 20px 30px;   上下20px  左右30px
    3. margin: 20px  30px  40px;     上20px  左右30px   下  40px
    4. margin: 20px  30px   40px  50px; 上20px   右30px   下40px  左50px
  - 垂直方向外边距合并
    两个盒子垂直一个设置上外边距，一个设置下外边距，取的设置较大的值。
  - 嵌套的盒子外边距塌陷
    - 解决方法:  
      1.给父盒子设置边框
      2.给父盒子overflow:hidden;   bfc   格式化上下文

- 内边距
  - padding-left|right|top|bottom
  - padding连写:
    1. padding:20px;	上下左右内边距都是20px
    2. padding:20px 30px;	上下20px	左右30px
    3. padding:20px 30px 40px;	上内边距为20px	左右内边距为30px	下内边距为40px
    4. padding:20px 30px 40px 50px;	上内边距为20px	右内边距为30px	下内边距为40px	左内边距为50px

  - 内边距撑大盒子的问题
    影响盒子宽度的因素；
    内边距影响盒子的宽度；
    边框影响盒子的宽度；
    盒子的宽度=定义的宽度+边框的宽度+左右内边距。
  - 继承的盒子一般不会被撑大
    包含（嵌套）的盒子，如果子盒子没有定义宽度，给子盒子设置左右内边距，一般不会撑大盒子。
