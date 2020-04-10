<!--
 * @Author: guoxinggang<guoxinggang@gsaxns.com>
 * @Version: 1.0
 * @Date: 2019-09-02 15:27:47
 * @LastEditTime: 2019-09-02 16:33:20
 * @Description: 
 -->
# gitbook使用教程

#### gitbook简介

- [gitbook 官网](https://www.gitbook.com/)

- [gitbook 文档](https://docs.gitbook.com/)

#### 一、安装node.js

GitBook 是一个基于 Node.js 的命令行工具，使用gitbook首先要下载安装 [node.js中文网](http://nodejs.cn/)，安装完成之后，你可以使用下面的命令来检验是否安装成功。

```node
$  node -v
v10.16.3
```

#### 二、安装gitbook

输入以下命令安装gitbook

```node
$ npm install gitbook-cli -g
```

安装完成之后，你可以使用下面的命令来检验是否安装成功。

```
CLI version: 2.3.2
GitBook version: 3.2.3
```

更多详情请参照 [GitBook 安装文档](https://github.com/GitbookIO/gitbook/blob/master/docs/setup.md) 来安装 GitBook。

#### 三、安装 gitbook Editor 编辑器

去 [gitbook 官网](https://www.gitbook.com/) 下载 GitBook 编辑器；如果是 Mac 用户且安装过 brew cask 的话可以使用 brew cask install gitbook-editor 命令行来安装 GitBook 编辑器。

#### 四、创建书籍

创建一个文件夹，使用命令窗口打开该文件夹，输入以下命令：

```
$ gitbook init
info: create README.md
info: create SUMMARY.md
info: initialization is finished
```
可以看到他会创建 README.md 和 SUMMARY.md 这两个文件，README.md 应该不陌生，就是说明文档，而 SUMMARY.md 其实就是书的章节目录，其默认内容如下所示：

```
# Summary

* [Introduction](README.md)
```

#### 五、预览书籍

接下来，我们输入以下命令：

```
$ gitbook serve 
```

然后在浏览器地址栏中输入 http://localhost:4000 便可预览书籍。

效果图如下所示:

![效果图](https://upload-images.jianshu.io/upload_images/1944467-80941aa796f964d9?imageMogr2/auto-orient/strip%7CimageView2/2/w/1000/format/webp)

运行以下命令后会在书籍的文件夹中生成一个 _book 文件夹, 里面的内容即为生成的 html 文件，我们可以使用下面命令来生成网页而不开启服务器。

```
$ gitbook build
```

#### 六、目录结构

GitBook 基本的目录结构如下所示：

```
.
├── book.json
├── README.md
├── SUMMARY.md
├── chapter-1/
|   ├── README.md
|   └── something.md
└── chapter-2/
    ├── README.md
    └── something.md
```

#### 七、book.json文件和SUMMARY.md文件的解读

##### 1. book.json

```
{
    "title": "book",    //本书标题
    "author": "book",     //本书作者
    "description": "select * from learn",    //本书描述
    "language": "zh-hans",    //本书语言，中文设置 "zh-hans" 即可
    "gitbook": "3.2.3",    //指定使用的 GitBook 版本
    "styles": {    //自定义页面样式
        "website": "./styles/website.css"
    },
    "structure": {    //指定 Readme、Summary、Glossary 和 Languages 对应的文件名
        "readme": "README.md"
    },
    "links": {    //在左侧导航栏添加链接信息
        "sidebar": {
            "我的狗窝": "https://blankj.com"
        }
    },
    "plugins": [    //配置使用的插件
        "-sharing",
        "splitter",
        "expandable-chapters",    //目录折叠插件
        "expandable-chapters-small",
        "anchors",

        "github",
        "github-buttons",
        "donate",
        "sharing-plus",
        "anchor-navigation-ex",
        "favicon"
    ],
    "pluginsConfig": {    //配置插件的属性
        "github": {
            "url": "https://github.com/Blankj"
        },
        "github-buttons": {
            "buttons": [{
                "user": "Blankj",
                "repo": "glory",
                "type": "star",
                "size": "small",
                "count": true
                }
            ]
        },
        "donate": {
            "alipay": "./source/images/donate.png",
            "title": "",
            "button": "赞赏",
            "alipayText": " "
        },
        "sharing": {
            "douban": false,
            "facebook": false,
            "google": false,
            "hatenaBookmark": false,
            "instapaper": false,
            "line": false,
            "linkedin": false,
            "messenger": false,
            "pocket": false,
            "qq": false,
            "qzone": false,
            "stumbleupon": false,
            "twitter": false,
            "viber": false,
            "vk": false,
            "weibo": false,
            "whatsapp": false,
            "all": [
                "google", "facebook", "weibo", "twitter",
                "qq", "qzone", "linkedin", "pocket"
            ]
        },
        "anchor-navigation-ex": {
            "showLevel": false
        },
        "favicon":{
            "shortcut": "./source/images/favicon.jpg",
            "bookmark": "./source/images/favicon.jpg",
            "appleTouch": "./source/images/apple-touch-icon.jpg",
            "appleTouchMore": {
                "120x120": "./source/images/apple-touch-icon.jpg",
                "180x180": "./source/images/apple-touch-icon.jpg"
            }
        }
    }
}
```

##### 2.  SUMMARY.md

这个文件主要决定 GitBook 的章节目录，它通过 Markdown 中的列表语法来表示文件的父子关系，下面是一个简单的示例：

```
# Summary

* [Introduction](README.md)
* [Part I](part1/README.md)
    * [Writing is nice](part1/writing.md)
    * [GitBook is nice](part1/gitbook.md)
* [Part II](part2/README.md)
    * [We love feedback](part2/feedback_please.md)
    * [Better tools for authors](part2/better_tools.md)
```

这个配置对应的目录结构如下所示:

![示意图](https://upload-images.jianshu.io/upload_images/1944467-de97699c5919469e?imageMogr2/auto-orient/strip%7CimageView2/2/w/604/format/webp)

我们通过使用 标题 或者 水平分割线 将 GitBook 分为几个不同的部分，如下所示：

```
# Summary

### Part I

* [Introduction](README.md)
* [Writing is nice](part1/writing.md)
* [GitBook is nice](part1/gitbook.md)

### Part II

* [We love feedback](part2/feedback_please.md)
* [Better tools for authors](part2/better_tools.md)

---

* [Last part without title](part3/title.md)
```

这个配置对应的目录结构如下所示:

![示意图](https://upload-images.jianshu.io/upload_images/1944467-e80d5e46997e5eb4?imageMogr2/auto-orient/strip%7CimageView2/2/w/596/format/webp)

#### 八、插件

GitBook 有 [插件官网](https://docs.gitbook.com/v2-changes/important-differences)，默认带有 5 个插件，highlight、search、sharing、font-settings、livereload，如果要去除自带的插件， 可以在插件名称前面加 -，比如：

```
"plugins": [
    "-search"
]
```

如果要配置使用的插件可以在 book.json 文件中加入即可，比如我们添加 **plugin-github**，我们在 book.json 中加入配置如下即可：

```
{
    "plugins": [ "github" ],
    "pluginsConfig": {
        "github": {
            "url": "https://github.com/your/repo"
        }
    }
}
```

然后在终端输入 gitbook install ./ 即可。

如果要指定插件的版本可以使用 plugin@0.3.1，因为一些插件可能不会随着 GitBook 版本的升级而升级。
