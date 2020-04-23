### pdf.js 使用笔记

#### 下载

[官网下载地址](https://mozilla.github.io/pdf.js/getting_started/#download)
下载 `Prebuilt (ES5-compatible)`(兼容 ES5) 的 `Stable` (稳定版) 的 `pdf.js` 包，`vue2.0` 放在 `static` 目录下、`vue3.0` 放在 `public` 目录下，并在 `vue.config.js` 中配置 `punlic` 文件夹的路径。 下载后将 pdf.js 放到服务器上 如：http://xxxx:8080/static/pdfjs

#### 引入使用

使用 pdf.js 在 web 页展示 pdf 文件的关键是打开 viewer.html，也就是在 web 页打开一个 html

```JavaScript
// 定义服务器地址 + 文件路径
let url = 'http://www.baidu.com/files/data/' + e.attachment
// 文件在新窗口打开
window.open('./pdf/web/viewer.html?file=' + url)
```

#### 取消下载和打印功能

在 `pdf/web/viewer.html` 文件中让下载按钮和打印按钮根据权限隐藏或者直接删除
