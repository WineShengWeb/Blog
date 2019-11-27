<!--
 * @Author: guoxinggang<guoxinggang@gsaxns.com>
 * @Version: 1.0
 * @Date: 2019-09-11 09:33:04
 * @LastEditTime: 2019-09-11 12:58:28
 * @Description: 
 -->
# H5新特性

#### 一、语义化标签

```
// 新增的标签
<article>-----------定义页面独立的内容区域。
<aside>-------------定义页面的侧边栏内容。
<bdi>---------------允许您设置一段文本，使其脱离其父元素的文本方向设置。
<command>-----------定义命令按钮，比如单选按钮、复选框或按钮
<details> ----------用于描述文档或文档某个部分的细节
<dialog> -----------定义对话框，比如提示框
<summary>-----------标签包含 details 元素的标题
<figure>------------规定独立的流内容（图像、图表、照片、代码等等）。
<figcaption>--------定义 <figure> 元素的标题
<footer>------------定义 section 或 document 的页脚。
<header> -----------定义了文档的头部区域
<mark> -------------定义带有记号的文本。
<meter> ------------定义度量衡。仅用于已知最大和最小值的度量。
<nav> --------------定义导航链接的部分。
<progress>----------定义任何类型的任务的进度。
<ruby>--------------定义 ruby 注释（中文注音或字符）。
<rt> ---------------定义字符（中文注音或字符）的解释或发音。
<rp> ---------------在 ruby 注释中使用，定义不支持 ruby 元素的浏览器所显示的内容。
<section>-----------定义文档中的节（section、区段）。
<time>--------------定义日期或时间。
<wbr>---------------规定在文本中的何处适合添加换行符。

// 修改或删除的标签
hr（直线，语义化变为分割线）、
small（表示文字小，语义化变为附属细则）、
strong（加粗，语义化变为重点强调）、
font被删除、
big被删除、
```

#### 二、增强型表单

- 传统的表单元素：form 、label 、input（text、radio、chickbox、button、submit、reset、password、hidden、file...）

- 给input的type新属性：calendar（日历）、date（日期）、time（时间）、email（邮箱地址）、url、search、color（调色板）、tel（电话号码）、range（范围）、number（数字）......

- 新的表单元素

```
  <input><textarea><select><option>....

  <datalist>：数据列表，为input提供输入建议列表

  <progress>：进度条，展示连接/下载进度

  <meter>：刻度尺/度量衡，描述数据所处的阶段，红色(危险)=>黄色(警告)=>绿色(优秀)

  <output>：输出内容，语义上表示此处的数据是经过计算而输出得到的
```

- 表单的新属性
  1. autocomplete（自动补全）

  ```
  <input type="email" name="email" autocomplete="off" />
  ```

  2. autofocus: 自动获得输入焦点（自动获取焦点）

  ```
  <input type="text" name="user_name" autofocus="autofocus" />
  ```

  3. list （规定输入域的 datalist。datalist 是输入域的选项列表）

  ```
  <input type="url" list="url_list" name="link" />
  <datalist id="url_list">
    <option label="W3Schools" value="http://www.w3school.com.cn" />
    <option label="Google" value="http://www.google.com" />
    <option label="Microsoft" value="http://www.microsoft.com" />
  </datalist>
  ```

  4. min、max 和 step 属性（input 类型规定限定）

  ```
  min：允许输入的数字最小值
  max：允许输入的数字最大值
  minlength：允许输入的字符串最小长度
  maxlength：允许输入的字符串最大长度
  <input type="number" name="points" min="0" max="10" step="3" />
  ```

  5. multiple: 是否允许多个输入（email 和 file可选择多个值）

  ```
  <input type="file" name="img" multiple="multiple" />
  ```

  6. pattern: 输入框内容必须符合的正则表达式（规定用于验证 input 的正则）

  ```
  <input type="text" name="country_code" pattern="[A-z]{3}" title="Three letter country code" />
  ```

  7. placeholder: 占位提示文字（描述输入域所期待的值）

  ```
  <input type="search" name="user_search" placeholder="Search W3School" />
  ```

  8. required：输入框内容不能为空

  9. form: 指定输入元素所从属的表单，可以实现输入框放在表单外部并能被提交的效果
验证属性(了解即可)：


#### 三、视频和音频

##### 用于媒介|播放的 video 和 audio 元素

###### video 视频（安卓手机兼容性有问题：表现在全屏、自动播放等）

- [方法和属性](https://www.w3school.com.cn/jsref/dom_obj_video.asp)

视频播放：

```
<video src=""><video>
查看视频的所有属性、方法、事件：console.log(videoBirds);
```

```
<video  webkit-playsinline="true" x-webkit-airplay="true" playsinline="true" x5-video-player-type="h5" x5-video-player-fullscreen="true" width="100%"  poster="" preload="auto">
      <source src=".xxx.mp4" type="video/mp4">
</video>
```

##### audio 音频（微信自动播放需要使用自己的API启动）

- [方法和属性](https://www.w3school.com.cn/jsref/dom_obj_audio.asp)

音频播放：

```
<audio src=""></audio>
查看视频的所有属性、方法、事件：console.log(bgMusic);
```

- 案例
```
// HTML部分
<!DOCTYPE html>
<html>
<head lang="en">
    <meta charset="UTF-8">
    <title></title>
    <meta name="viewport"
          content="width=device-width, user-scalable=no, initial-scale=1.0, maximum-scale=1.0, minimum-scale=1.0"/>
    <link rel="stylesheet" href="../css/myreset.min.css">
    <link rel="stylesheet" href="../css/swiper.min.css">
    <link rel="stylesheet" href="../css/index.css">
</head>
<body>
<section class="pages">
    <div class="swiper-container">
        <ul class="swiper-wrapper">
            <li class="swiper-slide">
                <section class="topBtn clearfix">
                    <div class="voice"></div>
                    <div class="progressWrap">
                        <p>在线听宪法</p>
                        <p>科大讯飞提供语音合成</p>
                        <div class="progress">
                            <div class="bar"></div>
                        </div>
                        <div class="current">00:00</div>
                        <div class="duration">36:12</div>
                    </div>
                </section>
            </li>
            <li class="swiper-slide">
                <section class="topBtn clearfix">
                    <div class="voice"></div>
                    <div class="progressWrap">
                        <p>在线听宪法</p>
                        <p>科大讯飞提供语音合成</p>
                        <div class="progress">
                            <div class="bar"></div>
                        </div>
                        <div class="current">00:00</div>
                        <div class="duration">36:12</div>
                    </div>
                </section>
            </li>
        </ul>
        <!--底部按钮-->
        <section class="butBtn">
            <div class="swiper-pagination swiper-pagination-fraction" id="swiper-pagination"><span
                    class="swiper-pagination-current">1</span> / <span class="swiper-pagination-total">3</span></div>
            <button class="getPoster">分享</button>
            <div class="swiper-button-next"></div>
            <div class="swiper-button-prev"></div>
        </section>
    </div>
</section>
<script src="../js/common.js"></script>//兼容移动端处理rem的js
<script src="../js/jquery.js"></script>
<script src="../js/swiper.js"></script>
<script src="../js/index.js"></script>//下文中的js
</body>
</html>

// CSS部分
html {
    font-size: 100px;
    width: 100%;
    height: 100%;
    max-width: 640px;
    margin: 0 auto;
    overflow: hidden;
    background: #fff;
}
body {
    width: 100%;
    height: 100%;
    max-width: 640px;
    background: #fff no-repeat;
    overflow: hidden;
    font-size: .28rem;
    position: relative;
    top: 0;
    left: 0;
}
.pages {
    width: 100%;
    height: 100%;
    position: relative;
}
.pages .swiper-container {
    width: 100%;
    height: 100%;
    position: relative;
}
.pages .swiper-wrapper {
    position: relative;
}
.pages .swiper-slide {
    width: 100%;
    height: 100%;
    position: relative;
    float: left;
    font-size: 18px;
    background: #ffeec6;
}
.pages .topBtn {
    display: block;
    width: 4.6rem;
    height: 1.4rem;
    padding: .05rem .25rem;
    padding-bottom: 0;
    margin: .2rem auto;
    background: #fcfcfc;
}
.pages .voice {
    width: .82rem;
    height: .82rem;
    float: left;
    background: url("../images/pause_03.png") no-repeat;
    background-size: 100%;
    margin-top: .1rem;
}
.pages .progressWrap {
    float: left;
    font-size: .2rem;
    color: #b3b3b3;
    width: 3.4rem;
    margin: .1rem;
    position: relative;
}
.pages .progressWrap p:nth-of-type(1) {
    font-size: .26rem;
    line-height: .26rem;
    color: #b12e29;
}
.pages .progressWrap p:nth-of-type(2) {
    font-size: .2rem;
    margin-top: .1rem;
    line-height: .2rem;
    margin-bottom: .1rem;
    color: #666666;
}
.pages .progressWrap .current {
    position: absolute;
    width: .7rem;
    margin-top: .14rem;
    text-align: center;
    overflow: hidden;
    color: #666666;
}
.pages .progressWrap .progress {
    width: 3.4rem;
    height: .06rem;
    vertical-align: middle;
    display: inline-block;
    border-radius: .03rem;
    background: #efefef;
    position: relative;
}
.pages .progressWrap .progress .bar {
    content: "";
    display: block;
    width: .06rem;
    height: .3rem;
    background: #b12e29;
    position: absolute;
    top: -0.1rem;
}
.pages .progressWrap .duration {
    position: absolute;
    color: #666666;
    right: 0;
    top: .26rem;
    margin-top: .7rem;
    text-align: center;
}
.pages .listsHide {
    position: absolute;
    right: -6.4rem;
    transition: all .5s linear;
}
.butBtn {
    width: 100%;
    height: 1rem;
    position: absolute;
    z-index: 9;
    bottom: 0;
    background: rgba(255,238,198,.8);
    -webkit-tap-highlight-color: transparent;
    -webkit-box-shadow: 20px -20px 30px #ffeec6;
    box-shadow: 20px -20px 30px #ffeec6;
}
.getPoster {
    display: block;
    height: .5rem;
    line-height: .5rem;
    text-align: center;
    width: 2.4rem;
    font-size: .28rem;
    border: none;
    border-radius: .25rem;
    color: #fff;
    -webkit-tap-highlight-color: transparent;
    margin: 0 auto;
    margin-top: .25rem;
    margin-left: 2.5rem;
    background: #333;
    background-size: 100%;
    background: #b12e29;
}
.swiper-pagination {
    width: 1rem;
    height: 1rem;
    line-height: 1rem;
    font-size: .28rem;
    color: #d9000e;
    margin-left: 1rem;
    bottom: 0;
}
.swiper-button-prev {
    width: .52rem;
    height: .52rem;
    background: url("../images/footBtn.png") no-repeat;
    background-size: 100%;
    margin-top: -0.28rem;
}
.swiper-button-prev:hover,
.swiper-button-prev:active {
    background: url("../images/footBtn.png") no-repeat;
    background-size: 100%;
}
.swiper-button-next {
    width: .52rem;
    height: .52rem;
    background: url("../images/footBtn_05.png") no-repeat;
    background-size: 100%;
    margin-top: -0.28rem;
}
.swiper-button-next:hover,
.swiper-button-next:active {
    background: url("../images/footBtn_05.png") no-repeat;
    background-size: 100%;
}

// js部分
//初始化swiper
var voiceList = ['0.mp3','1.mp3', '2.mp3', '3.mp3',"4.mp3","5.mp3","6.mp3","7.mp3","8.mp3","9.mp3","10.mp3","11.mp3"];
function swiperInit() {
    var mySwiper=new Swiper('.swiper-container', {
        pagination: '.swiper-pagination',
        paginationClickable: '.swiper-pagination',
        nextButton: '.swiper-button-next',
        prevButton: '.swiper-button-prev',
        paginationType: 'fraction',
        touchAngle : 25,//触发水平角
        touchMoveStopPropagation : false,//阻止touchmove冒泡事件
        threshold : 80,//触发最小距离
        //onlyExternal : true,
        onSlideChangeEnd: changeCallback,
    });
    return mySwiper

}
swiperInit();
//换页回调
function changeCallback() {
    if (myAudio.audio) {
        myAudio.audioInit()
        myAudio.audioProgressContral()
    }
}

function DefinedAudio(voiceList,progressRemW){
    this.voiceList=voiceList;//歌曲列表
    this.timer='';//计时器
    this.ProgressW=progressRemW*document.documentElement.clientWidth/640*100;//进度条长度
    var that=this;
    this.init=(function(){
        that.createAudio();
        that.audioInit();
        that.play();
        that.audioProgressContral();
    })();
}
//创建audio标签
DefinedAudio.prototype.createAudio=function(){//创建audio
    this.audio = document.createElement('audio');
    document.body.appendChild(this.audio);
}
//初始audio
DefinedAudio.prototype.audioInit=function(){//初始化
    var that=this;
    this.audio.pause();
    $('.voice').css('background-image','url(../images/pause_03.png)')
    $('.bar').css('left', 0);
    clearInterval(this.timer);
    $('.current').html('00:00');
    var curIndex = $('.swiper-pagination-current').html() - 1;
    this.audio.src = 'http://microblog.people.com.cn/htmlfile/xfAudio/' + this.voiceList[curIndex]+'?'+Math.random();
    var ua = navigator.userAgent.toLowerCase();
    if (/iphone|ipad|ipod/.test(ua)) {//苹果设备预加载
        this.audio.play()
        this.audio.addEventListener('canplay', function () {
            that.audio.pause();
            var time = that.timeFormat(that.audio.duration);
            $('.duration').html(time);
        }, false);
    } else {
        this.audio.addEventListener('canplay', function () {
            var time = that.timeFormat(that.audio.duration);
            $('.duration').html(time);
        }, false)
    }
}
//时间格式换
DefinedAudio.prototype.timeFormat=function (time) {
    var min = Math.floor(time / 60);
    var sec = Math.floor(time % 60);
    min = min < 10 ? "0" + min : "" + min;
    sec = sec < 10 ? "0" + sec : "" + sec;
    return min + ":" + sec;
}
//手动控制音频进度
DefinedAudio.prototype.audioProgressContral=function (){
    var that=this;
    var bar= $('.bar')[$('.swiper-pagination-current').html()-1];
    bar.addEventListener('touchstart',start,false);
    bar.addEventListener('touchmove',move,false)
    bar.addEventListener('touchend',end,false)
    function start(e){
        that.audio.L=$('.bar').css('left');
        that.audio.X=e.touches[0].clientX
        if(that.audio.paused){
            that.audio.ProgressFlag=1;
        }else{
            that.audio.ProgressFlag=0;
        }
        return false;
    }
    function move(e){
        that.audio.changeX=e.changedTouches[0].clientX-that.audio.X;
        that.audio.changeX=that.audio.changeX+parseFloat(that.audio.L)
        that.audio.endX=that.audio.changeX<0?0:(that.audio.changeX>that.ProgressW?that.ProgressW:that.audio.changeX)
        $('.bar').css('left',that.audio.endX);
        that.audio.currentTime=that.audio.endX/that.ProgressW*that.audio.duration;
        var time = that.timeFormat(that.audio.currentTime);
        $('.current').html(time);
        return false;
    }
    function end(e){
        if(that.audio.ProgressFlag!==1){
            that.audio.play();
        }else{
            that.audio.pause();
        }
        return false;
    }
}
//播放与暂停
DefinedAudio.prototype.play=function () {
    var that=this;
    clearInterval(this.timer);
    if (this.audio.paused) {
        this.audio.play();
        $('.voice').css('background-image','url(../images/play_03.png)')
    } else {
        this.audio.pause();
        $('.voice').css('background-image','url(../images/pause_03.png)')
        clearInterval(this.timer);
        return;
    }
    //进度条
    progress()
    this.timer = setInterval(progress, 1000);
    function progress() {
        if (that.audio.currentTime > that.audio.duration) {
            clearInterval(that.timer);
        }
        var time = that.timeFormat(that.audio.currentTime);
        $('.current').html(time);
        var $bar = $('.bar');
        $bar.css('left', that.audio.currentTime / that.audio.duration * 100 + "%");
    }
}
//控制音量(volume 属性设置或返回音频的音量，从 0.0 (静音) 到 1.0 (最大声)。)
DefinedAudio.prototype.vol=function(n){
    this.volume = n;
}
//实例
var myAudio=new DefinedAudio(voiceList,'3.4');
$('.voice').on('click',function(){
    myAudio.play();
})
```

#### 四、canvas绘图

##### WEB中可用的绘图技术：

    (1)Canvas绘图：H5原生技术，基于网页画布绘制2D位图绘图技术，善于表现细腻颜色

    (2)SVG绘图：H5借鉴技术，基于SVG绘图空间绘制2D矢量图绘图技术，缩放不会失真

    (3)WebGL绘图：尚不是H5标准技术，基于HTML5 Canvas提供硬件3D加速渲染；有一个非常强大3D扩展库：three.js

H5原生技术，基于网页画布2D位图绘图技术，善于表现细腻颜色，可用于统计图表、页面游戏、地图应用、网页特效等。

```
// 使用Canvas的步骤：
<canvas id="c2" width="400" height="300"></canvas>
Canvas自身是一个300*150的inline-block元素；注意：Canvas画布尺寸不能使用CSS设置——会对整个图像进行扭曲！

// 使用H5 Canvas API进行绘图：
var ctx = c2.getContext('2d'); 

//绘制矩形
ctx.fillStyle = '#000'  // 填充颜色/渐变色对象

ctx.strokeStyle = '#000'  // 描边颜色/渐变色对象

ctx.lineWidth = 1  // 描边线宽度

ctx.fillRect(x, y, w, h)：  // 填充矩形

ctx.strokeRect(x, y, w, h)：  // 描边矩形

ctx.clearRect(x, y, w, h)：  // 描边矩形

//绘制文本
ctx.font = '10px sans-serif'

ctx.textBaseline = 'alphabetic/top/bottom'

ctx.fillStyle = '#000'

ctx.strokeStyle = '#000'

ctx.fillText(txt, x, y)  // 填充文本

ctx.strokeText(txt, x, y)  // 描边文本

ctx.measureText(txt).width  // 测量文本基于当前字体设置的宽度

//绘制路径——概念上类似于PS中的钢笔工具
ctx.beginPath()

ctx.moveTo()

ctx.lineTo()

ctx.arc()

ctx.rect()

ctx.ellipse()

ctx.closePath()

-----------------------------

ctx.stroke()  // 基于现有路径进行描边

ctx.fill()  // 基于现有路径进行填充

ctx.clip()  // 基于现有路径进行裁切

//绘制图像
ctx.drawImage(img, x, y)  // 绘制图像(原始尺寸)

ctx.drawImage(img, x, y, w, h)  // 绘制图像(指定尺寸)

//绘图上下文变形和状态保持
ctx.rotate()  // 图像旋转

ctx.translate()  // 图像平移

ctx.scale()  // 图像缩放

------------------

ctx.save()  // 绘图上下文的保存

ctx.restore()  // 绘图上下文的恢复
```

#### 五、SVG绘图

```
Scalable Vector Graphic，可缩放向量图

在H5标准之前的使用方法：SVG标签不能直接书写在网页中，只能编写在独立的XML文档中；

网页中使用<img src="x.svg">进行嵌入

纳入H5标准后的使用方法：SVG标签可以直接书写在网页中。

常用的SVG图形：

(1)矩形
<rect width="100" height="50" x="400" y="350" fill="#f0f" fill-opacity="0.3" stroke="#00f" stroke-width="6" stroke-opacity=".3"></rect>

(2)圆形
<circle r="100" cx="400" cy="300" fill="#f0f" fill-opacity="0.4" stroke="#00f" stroke-width="6" stroke-opacity=".4"></circle>

(3)椭圆
<ellipse rx="100" ry="50" cx="400" cy="350" fill="#f0f" fill-opacity=".4" stroke="#00f" stroke-width="6" stroke-opacity=".4"></ellipse>        

(4)直线（没有fill只有stroke）
<line x1="45" y1="350" x2="450" y2="350" stroke="#f00" stroke-width="4px" stroke-opacity=".4"></line>

(5)折线（fill必须设置透明/stroke必须手工指定）
<polyline points="150,200  250,100  350,300  450,50" stroke="#00f" stroke-width="6" stroke-opacity=".4" fill="transparent"></polyline>

(6)多边形
<polygon points="100,150 100,300  400,300  400,150  250,220" fill="#f0f" fill-opacity=".4" stroke="#00f" stroke-width="6" stroke-opacity=".4"></polygon>

(7)文本
<text alignment-baseline="before-edge" font-size="40" fill="#f0f" stroke="#00f">达内科技2018ajgy</text>

(8)图像
<image xlink:href="img/p3.png" x="400" y="200" width="100" height="200"></image>

扩展小知识：

(1)使用滤镜（高斯模糊）
参考MDN手册：https://developer.mozilla.org/zh-CN/docs/Web/SVG/Element/filter

声明滤镜：
<filter id="f2">
    <feGaussianBlur stdDeviation="3"></feGaussianBlur>
</filter>

使用滤镜：
<image/text/rect  filter="url(#f2)">

(2)使用颜色渐变对象

声明渐变对象：
<linearGradient id="g2" x1="0" y1="0" x2="100%" y2="0">
    <stop offset="0" stop-color="red"></stop>
    <stop offset="0.5" stop-color="yellow"></stop>
    <stop offset="1" stop-color="green"></stop>
</linearGradient>

使用渐变对象：
<text/rect fill="url(#g2)" stroke="url(#g2)">
```

##### Canvas与SVG的不同

1. Canvas是位图；SVG是矢量图
2. Canvas是JS绘图技术(不是DOM元素)；SVG是标签绘图技术(是DOM元素)
3. Canvas内容不能使用CSS；SVG内容可以使用CSS；
4. Canvas内容不方便绑定事件处理；SVG内容方便进行事件绑定

#### 六、地理定位

```
通过浏览器获取当前用户的所在地理坐标，以实现“LBS服务”（Location Based Service），如实时导航、周边推荐。

情形1：用户使用手机浏览器——可以根据内置GPS芯片读取数据

情形2：用户使用PC浏览器——可以根据电脑的IP地址进行反向查询(需要很大的IP分配库)

window.navigator.geolocation : {

    watchPosition(){},

    clearWatch(){},

    getCurrentPosition(function(pos){

        '定位成功'

        定位时间：pos.timestamp

        维度：pos.coords.latitude

        经度：pos.coords.longitude

        海拔：pos.coords.altitude

        速度：pos.coods.speed

    }, function(err){

        '定位失败'

    }){},

}
```

#### 七、拖放API

```
H5之前没有拖放API，可以使用“鼠标按下 + 鼠标移动”两个事件来模拟用户拖动事件。
H5之后专门提供了七个鼠标拖动相关事件句柄：

拖动的源对象(source)可能触发的事件：

    dragstart：拖动开始
    drag：拖动中
    dragend：拖动结束

拖动的目标对象(target)可能触发的事件：

    dragenter：拖动进入
    dragover：拖动悬停
    drop：松手释放
    dragleave：拖动离开

注意：拖放API事件句柄中所有的事件对象都有一个dataTransfer属性（数据运输对象），用于在源对象和目标对象间传递数据。

源对象：event.dataTransfer.setData(key, value)

目标对象：var value = event.dataTransfer.getData(key)
```

#### 八、WebWorker

- 背景：Chrome浏览器中发起资源请求的有6个线程；但是只有1个线程负责渲染页面——称为UI主线程——浏览器中所有的代码只能由一个线程来执行。

- 问题：若浏览器加载了一个很耗时的JS文件(可能影响DOM树结构)，浏览器必须等待该文件执行完成才会继续执行后续的代码(HTML/CSS/JS等)——如果一个JS文件要执行10s(可能有很深的循环/递归等科学计算/解密)，会发生什么？——执行耗时JS任务过程中，会暂停页面中一切内容的渲染以及事件的处理。

- 解决方案：H5新特性——Web Worker

- Worker的本质：就是一个执行指定任务的独立线程；且该线程可以与UI主线程进行消息数据传递。使用方法：

```
// HTML文件中：

var w = new Worker('js/x.js')

w.postMessage('发送给Worker线程的消息');

w.onmessage = function(e){

    e.data; //来自Worker线程的消息

}

// JS文件中：

onmessage = function(e){

var data = e.data;  //接收UI线程的消息

//执行耗时任务....

postMessage(result);   //给UI线程发送消息

}
```

#### 九、WebStorage

##### Web项目存储数据常用的方案：

1. 服务器端存储

  - 数据库存储，如商品、用户等核心数据
  - Session/内存存储，如用户的登录信息

2. 客户端存储

  - Cookie存储，如用户偏好、访问历史，浏览器兼容性好但处理麻烦且容量限制

  - H5 WebStorage存储，如用户偏好、访问历史等安全要求的数据，老IE不兼容但易使用且容量大

##### H5WebStorage存储具体涉及到两个对象：

1. window.sessionStorage：类数组对象，通过key=>value对存储字符串数据——会话级存储

  - 添加数据：sessionStorage['key'] = 'value'

  - 修改数据：sessionStorage['key'] = 'newValue'

  - 删除数据：delete sessionStorage['key']

  - 获得数据：var  v = sessionStorage['key']

2. window.localStorage：类数组对象，通过key=>value对存储字符串数据——本地/跨会话级/永久存储

  - 添加数据：localStorage['key'] = 'value'

  - 修改数据：localStorage['key'] = 'newValue'

  - 删除数据：delete localStorage['key']

  - 获得数据：var  v = localStorage['key']

#### 十、WebSocket
