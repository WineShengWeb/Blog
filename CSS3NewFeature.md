# <center>CSS3新特性</center>

---

## 一、动画

- 动画属性
    1. animation:动画名称 持续时间 执行次数 是否反向 运动曲线 延迟时间;
    2. 动画名称:animation-name: move;
    3. 持续时间:animation-duration:5s;//一次动画持续时间,前两个属性是必须,且顺序固定;
    4. 执行次数:animation-iteration-count: infinite;//无数次 infinite;normal 正常;
    5. 是否反向:animation-direction: normal;//alternate:反向;   normal:正常;
    6. 运动曲线:animation-timing-function: ease-in-out;//ease:匀速;    ease-in:由慢到快;    ease-out:由快到慢;    ease-in-out:;
    7. 延迟时间:animation-delay: 1s;//动画延迟时间1s;
    8. 设置动画结束盒子的状态:animation-fill-mode: backwards;//backwards:保持动画开始前的状态; forwards:保持动画结束后的状态;

- 定义动画
    - 定义单个动画:
        ```
        @keyframes animationName{
            from{ 初始状态 }
            to{ 结束状态 }
        }
        ```
    - 定义多个动画
        ```
        @keyframes animationName{
            0%{
                transform:translateX(0px) translateY(0px);
                background-color: green;
                border-radius: 0px;	
            }
            25%{
                transform:translateX(500px) translateY(0px);
            }
            50%{
                transform:translateX(500px) translateY(300px);
                border-radius: 50px;
            }
            75%{
                transform:translateX(0px) translateY(300px);
            }
            100%{
                transform:translateX(0px) translateY(0px);
                background-color: red;
                border-radius: 0;
            }
        }
        ```
## 二、过渡

- 过渡属性
    1. transition: 过渡属性  持续时间  运动曲线  延迟时间;
    2. transition: all(代表所有属性都有过渡) 2s(代表时间) linear 1s;
        注:过渡必须加给盒子本身;
    3. transition-property:过渡的属性
        all:所有的属性
        如果想要某一个属性单独有过渡效果,直接写该属性名;
    4. transition-duration:过渡持续时间;
    5. transition-timing:运动曲线;
        linear:运动曲线
        ease-in:线性
        ease-out ease-in-out:先加速后减速
    6. transition-delay:延迟时间;
    7. transitionEnd:过渡结束事件

## 三、渐变

- 线性渐变
  - linear-gradient(方向,起始颜色,终止颜色)
  - 方向:to left,to right,top top,to bottom,角度:360度;如：
    ```
    background-image:linear-gradient(to right,yellow,red);//从左往右渐变
    background-image:linear-gradient(yellow,red);//不写方向,默认从上往下渐变
    background-image:linear-gradient(90deg,yellow,red);//旋转90度渐变
    ```
- 径向渐变
  - radial-gradient(辐射半径,中心位置,起始颜色,终止颜色);
  - at left right center bottom top
    ```
    background-image: radial-gradient(at left top,yellow,green);//从左上角渐变
    background-image: radial-gradient(at 50px 50px,yellow,green);
    background-image: radial-gradient(120px at center,yellow,green);
    ```

## 四、背景及颜色
- 背景大小
    ```
    background-size: 500px  500px;
	background-size: 50% 50%;
	background-size: contain;
    background-size:背景图片尺寸
        cover 会保证完全覆盖盒子,但不能保证完整显示;
	    contain 背景图片最大化的在盒子中等比例显示,但不保证能铺满盒子;
    ```
- 背景原点
    ```
    background-origin(控制背景从什么地方开始显示)
    background-origin: border-box/content-box/padding-box;
                        border-box:从border-box开始显示
                        content-box:从content-box开始显示
                        padding-box:从padding-box开始显示
    ```
- 背景裁剪:
    ```
    background-clip:border-box/content-box/padding-box;
                    border-box:从border-box开始裁剪
                    content-box:从content-box开始裁剪
                    padding-box:从padding-box开始裁剪
    ```
- 多背景:
    ```
    background: url(img/bg1.png) no-repeat left top,
                url(img/bg2.png) no-repeat right top,
                url(img/bg3.png) no-repeat right bottom,
                url(img/bg4.png) no-repeat left bottom;
    ```
- 颜色的表示
    1. transparent:可以单独的设置透明度,但是无法改变透明的值;
    2. opacity:可以给盒子设置半透明，但是会影响里面的子盒子，并且子盒子无法改变透明度;用来设置元素的不透明级别，从 0.0 （完全透明）到 1.0（完全不透明）;
    3. rgba:r：红色值；g：绿色值；b：蓝色值。三个颜色值组合在一起就形成最终颜色。a：alpha透明度。表示像素不透明性的值。
    像素越不透明，则隐藏越多呈现图像的背景。取值0~1之间。0表示完全透明的像素，1表示完全不透明的像素。
    -  注:opacity会继承父元素的 opacity 属性，而RGBA设置的元素的后代元素不会继承不透明属性。

## 五、缩放、平移、旋转

- transform:translate(平移) scale(缩放) rotate(旋转);
- 平移:
    translate(水平位移,垂直位移);
    正值:向右向下;
    负值:向左向上;
    如果只写一个值:水平移动;transform: translate(50%);
    百分比:相对于自身移动
    如：
    ```
    transform: scale(0.5) translateX(80px) translateY(-100px);
    ```
- 缩放:
    transform:scale(水平缩放比例,垂直缩放比例);
    大于1：放大
    小于1：缩小
    如果只写一个值等比例缩放
    如:
    ```
    transform:scale(1.5);
    transform:scale(1.2,1.6);
    ```
- 旋转:rotate(角度)
    正值:顺时针
    负值:逆时针
    如:
    ```
    transform: rotate(90deg);
    transform: rotate(-90deg);
    ```
- 转换成3D
    ```
    transform-style: preserve-3D;
    ```
- perspective:透视;
    设置的是用户的眼睛距离平面的距离,只是视觉上的呈现,并不是真真的3D,是加给父盒子的,所有的3D旋转,都是对着正方向;

## 六、边框及阴影

- 边框背景图
    ```
    边框图片路径:border-image-source: url(img/border.png);
    图片边框裁剪:border-image-slice: 27;
    图片边框宽度:border-image-width: 27px;
    边框图片的平铺:border-image-repeat:strech;
                repeat:正常平铺 但是会显示不完整;
                round:平铺  保证图片完整;
                stretch:拉伸显示;
    border-image:url(border.png) 30 30 round;
    ```
- 边框圆角
    ```
    border-radius: 水平半径/垂直半径;
    border-radius: 左上角  右上角  右下角  左下角;
    赋值顺序  从左上开始,顺时针赋值,如果当前角没有值,取对角的值;
    border-radius:25px;
    border-radius:25px 25px;
    border-radius:25px 25px 25px;
    border-radius:25px 25px 25px 25px;
    ```
- 边框阴影
    ```
    box-shadow:水平位移  垂直位移  模糊度  阴影大小  阴影颜色  外/内阴影(inset);默认外阴影,不用写
    box-shadow: 上  下  左  右  模糊度  阴影大小  阴影颜色  外/内阴影(inset);
    box-shadow: 10px 10px 5px #888888;
    ```
- 文本阴影
    ```
    text-shadow:文字阴影
    text-shadow:水平位移 垂直位移  模糊程度  阴影颜色;
    text-shadow: 上  下  左  右  模糊度  阴影颜色  外/内阴影(inset);
    ```

## 七、选择器

- 基础选择器
    ```
    div.box{};//div里面class名为box的元素
    div,p{};//所有div和所有p元素公用一组样式
    div+span{};//div后面相邻的第一个span
    div~p{};//选中的div后面所有的p;
    div p{};//后代选择器
    div>p{};//子代选择器
    ```
- 属性选择器
    ```
    div[class]{};//选中div中所有带class类名的元素
    div[class="box1"]{};//选中div中class名为box1的元素
    div[class^="aa"]{};//div带有class属性,并且值以aa开头
    div[class$="aa"]{};//div带有class属性,并且值以aa结尾
    div[class*="aa"]{};//div带有class属性,并且值包含aa
    ```
- 伪类选择器
    ```
    :link
    :visited
    :hover
    :active
    ```
- 结构伪类:符号:(冒号);通过结构来进行筛选
    ```
    li:first-child{};//第一个
    li:last-child{};//最后一个
    li:nth-child(11){};//第11个,注意, 编号从1开始
    li:nth-child(odd){};//奇数
    li:nth-child(2n+1){};
    li:nth-child(even){};//偶数
    li:nth-child(2n){};
    li:nth-child(-n+5){};//前5个
    li:nth-last-child(-n+5){};//后5个
    li:nth-child(7n){};//7的倍数
    ```
- 空伪类:
    ```
    empty:空
    div:empty{};//如果div是空的,则会被选中
    target伪类:配合锚点使用,表示被激活的状态
    ```
- 伪元素:  
    ```
    ::before    ::after    ::frist-letter    ::frist-line
    ::before:在元素之前插入内容
    ::after:在元素之后插入内容
    p::first-letter{};//选中第一个字
    div::first-line{}.//选中第一行
    ```

- ::和:的区别是为了区别伪类和伪元素的
    在css2中单个:表示伪类;
    在css3中双::表示伪元素.

- 私有化前缀属性:
    -webkit- ：谷歌,苹果(内核:Webkit)
    -moz- ：火狐(内核:Gecko)
    -ms- ：IE(内核:Trident)
    -o- ：Opera(内核:presto)
    注:Blink内核：谷歌(5.2版本以后)和Opera浏览器

## 八、web存储

Web Storage DOM API 为Web应用提供了一个能够替代cookie的Javascript解决方案；
对于大量复杂数据结构，一般使用IndexDB。
- sessionStorage—客户端数据存储，只能维持在当前会话范围内。
    sessionStorage 方法针对一个 session 进行数据存储。当用户关闭浏览器窗口后，数据会被删除
    ```
    ```
- localStorage—客户端数据存储，能维持在多个会话范围内。
    localStorage 对象存储的数据没有时间限制。第二天、第二周或下一年之后，数据依然可用。
    ```
    ```
## 九、语义化标签

    ```
    <header>
    <nav>
    <section>
    <article>
    <aside>
    <figcaption>
    <figure>
    <footer>
    ```
![示意图](https://images2015.cnblogs.com/blog/801509/201607/801509-20160711082959467-525706727.png)

