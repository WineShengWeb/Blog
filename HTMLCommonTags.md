<!--
 * @Author: guoxinggang<guoxinggang@gsaxns.com>
 * @Version: 1.0
 * @Date: 2019-09-11 09:31:31
 * @LastEditTime: 2019-09-11 11:17:25
 * @Description: 
 -->
# HTML常用标签

#### 1. 什么是HTML?

    Hyper text markup language  //超文本标记语言

    超文本:文字,视频,音频,图片,输入框,超链接等

#### 2. HTML标准结构

```
<!doctype  html>..................................声明文档格式
<html>........................................根标签
    <head>....................................头部标签
        <meta charset="UTF-8">................描述 HTML 文档标签,此处为编码格式规定设置
        <title>My frist demo</title>.......................标题标签
    </head>
    <body>.............................主体标签
        <div>我的第一个网页</div>........内容
    </body>
</html>
```

#### 3. 图片标签

```
<img src="zhaosi.jpg"  alt="尼古拉斯赵四"  title="亚洲气质舞王" />
```

##### 属性:

- src：图片的来源
- alt:当图片不显示时,显示文字
- title:当鼠标移向图片,显示文字
- width:宽度
- height:高度

- 注意:当未定义宽高时,图片显示原来尺寸，当只定义宽或高时,图片等比例缩放，当宽高都定义时,图片大小由定义决定

- 路径问题:
    1. 文件和图片在同一级目录时,直接写文件名.
    2. 图片在HTML文档下一级目录时,目录名+图片文件名
    3. 图片在HTML上一级目录里时,../+文件名字从HTML文件出发寻找路径

#### 4. 超链接

```
<a href="" target=""></a>
```

##### 属性

- href: url 跳转的地址
- target:
  1. _self: 在原来的窗口打开
  2. _blank: 在新的窗口打开
  3. _parent: 在父框架集中打开被链接文档
  4. _top: 在整个窗口中打开被链接文档
  5. framename: 在指定的框架中打开被链接文档
- title:当鼠标移向超链接时,显示的文字
- style:text-decoration:none..................超链接去底线

```
<a href="www.baidu.com">百度</a>

// 阻止a链接跳转
<a href="#">百度</a>
<a href="javascript:;">百度</a>
<a href="#" onclick="fn()">百度</a>  // 给链接返回一个错误
fn (){ return false; }  // 函数返回错误

// 锚点
<a id="back"></a>  // 先定义一个锚点
<a href="#back">回到顶部</a>  // 超链接到锚点
```

注: 伪类请查看CSS总结.

#### 5. 列表

##### 无序列表

```
<ul type="none/circle/square/disc">
    <li>买了佛冷</li>
    <li>买了佛冷</li>
    <li>买了佛冷</li>
    <li>买了佛冷</li>
</ul>

type:
1.disc...........实心圆圈
2.square.........实心方块
3.circle.........空心圆圈
4.none...........空
```

##### 有序列表

```
<ol type="a/A/i/I/l" start="">
    <li>买了佛冷</li>
    <li>买了佛冷</li>
    <li>买了佛冷</li>
    <li>买了佛冷</li>
</ol>

注:
1.type的值为:l,a,A,i,I
2.start:开始的位置(填数字)
```

##### 自定义列表

```
<dl>
    <dt>抖音神曲</dt>.............大标题
    <dd>抖音神曲</dd>.............小标题
    <dd>抖音神曲</dd>.............小标题
    <dd>抖音神曲</dd>.............小标题
</dl>
```

#### 6. 表格标签

1. 格式:

```
<table border="">.....................表格
    <tr>..............................行
        <th></th>.....................表头
    </tr>
    <tr>
        <td></td>.....................列
    </tr>
</table>
```

简单的 HTML 表格由 table 元素以及一个或多个 tr、th 或 td 元素组成。

tr 元素定义表格行，th 元素定义表头，td 元素定义表格单元。

更复杂的 HTML 表格也可能包括 caption、col、colgroup、thead、tfoot 以及 tbody 元素

2. 属性:

- border:边框
- width:宽
- height:高
- cellspacing:单元格与单元格的距离
- cellpadding:内容与边框的距离
- align:位置
  - left/right/center  内容居左/中/又
  - 如果直接给表格用align="center",表格居中
  - 如果直接给tr或td用,tr或td内容居中
- background-color="":背景颜色

3. 表头和单元格的合并

- caption:表头
- rowspan:合并同一列单元格(写在tr)
- colspan:合并同一行单元格(写在td)

#### 7. 表单

```
<form action="">
    <input type="text">
</form>
```

1. 表单域

属性：
  - action:处理信息,数据提交的地址.
  - Method=”get | post”   数据提交的方式.
      - Get:通过浏览器提交,不安全,数据大小有限制;通过地址栏提供（传输）信息，安全性差。会暴露密码;
      - Post:通过http协议提交;数据大小无限制;通过1.php来处理信息，安全性高。打包邮寄,不会暴露密码

2. 输入框:

属性:
  - type="": 输入框的类型
    - button: 按钮
    - checkbox: 复选框
    - file: 上传文件
    - hidden: 定义隐藏的输入字段
    - image: 上传图片
    - password: 密码框
    - radio: 定义单选按钮
    - reset: 重置
    - submit: 提交
    - text: 文本框
  - maxlength="6": 限制输入字符长度
  - readonly="": 将输入框设置为只读状态(不能编辑),但可以向服务端提交
    - 1:readonly="readonly"
    - 2:readonly="true"
    - 3:readonly/readonly="false"
  - disabled="": 框变灰,内容不能修改,内容不可以修改;输入框未激活状态
    - 1:disabled="disabled"
    - 2:disabled="true"
    - 3:disabled/disabled="false"
  - name="username": 输入框的名称
  - value="": 将输入框内容传输给处理文件

```
// 密码框
<input type="password" name="username">
// 单选框
<input type="radio" />
// 复选框
<input type="checkbox" name="yuqiansandaaihao">抽烟
<input type="checkbox" name="yuqiansandaaihao">喝酒
<input type="checkbox" name="yuqiansandaaihao">烫头
// 文件上传
<input type="file">
// 提交按钮
<input type="submit>
10.重置按钮
<input type="reset">
```

#### 8. 下拉列表

```
<select>
    <optgroup label="好吃的">
        <option value="">驴肉火烧</option>
        <option value="">鸡蛋灌饼</option>
        <option value="">麻辣烫</option>
        <option selected="selected">铁锅焖面</option>
        <option>红烧牛肉面</option>
    </optgroup>
    <optgroup label="好玩的">
        <option value="">驴肉火烧</option>
        <option value="">鸡蛋灌饼</option>
        <option value="">麻辣烫</option>
        <option selected="selected">铁锅焖面</option>
        <option>红烧牛肉面</option>
    </optgroup>
</select>
```
- 属性
  - selected="selected"默认值
  - multiple="multiple"将下拉列表设置为多选项
  - option: 具体的选项
  - optgroup: 对下拉列表进行分组
  - label=””  分组名称
  - type="checkbox"
#### 9. 文本域

```
<textarea name=""></textarea>
```
- 属性
cols=""控制输入字符的长度
rows=""控制输入字符的行数

#### 10. meta标签

```
<meta charset="UTF-8">  // 设置编码格式
<meta http-equiv="refresh" content="5+某网站">  // 网页重新定向,数字代表网页停留秒数
<meta name="keywords" content="百度">  // 网页搜索关键字
<meta name="description" content="搜索引擎">  // 网页内容的描述
<meta name="author" content="你的姓名">  // 网页制作的作者
<meta name="robots" content="all/none/index/noindex/follow/nofollow">
属性:
  content:
    all:文件被检索,且页面上的链接可以被查询
    none:文件将不被检索,且页面上的链接不可以被查询
    index:文件将被检索
    noindex:文件将不被检索,且页面上的链接可以被查询
    follow:页面上的链接可以被查询
    nofollow:文件将不被检索,且页面上的链接可以被查询
    <base href="http://www.runoob.com/images/" target="_blank">定义页面中所有链接默认的链接目标地址。
```

#### 11. link标签

```
// 链接样式表(CSS文件)
<link rel="stylesheet" type="text/css" href="reset.css" />

// 图标(头部显示)
<link rel="icon" href="favicon.ico"/>
```

##### 属性
- rel属性值:
    - alternate:文档的替代版本（比如打印页、翻译或镜像）
    - stylesheet:文档的外部样式表
    - start:集合中的第一个文档
    - next:集合中的下一个文档
    - prev:集合中的上一个文档
    - contents:文档的目录
    - index:文档的索引
    - glossary:在文档中使用的词汇的术语表（解释）
    - copyright:包含版权信息的文档
    - chapter:文档的章
    - section:文档的节
    - subsection:文档的小节
    - appendix:文档的附录
    - help:帮助文档
    - bookmark:相关文档
- href属性值:
    URL:可能的值：

  - 绝对 URL - 指向另一个站点（比如 href="http://www.example.com/theme.css"）
    
  - 相对 URL - 指向站点内的某个文件（href="/themes/theme.css"）

