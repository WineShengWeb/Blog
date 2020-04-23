#### onlyOffice 使用笔记

##### 部署

在服务器上部署 onlyoffice，具体步骤请[百度](https://www.baidu.com)

##### 使用

###### HTML 使用

-   1、创建标签

```html
<div id="placeholder"></div>
```

-   2、引入并配置

```JavaScript
<script
    type="text/javascript"
    src="https://documentserver/web-apps/apps/api/documents/api.js"
></script>
// documentserver是你部署onlyoffice服务器的地址

<script type="text/javascript">
    window.docEditor = new DocsAPI.DocEditor("placeholder",
        {
            "document": {
                "fileType": "docx",
                "key": "E7FAFC9C22A8",
                "title": "Example Document Title.docx",
                "url": "https://example.com/url-to-example-document.docx"
            },
            "documentType": "text",
            "editorConfig": {
                "callbackUrl": "https://example.com/url-to-callback.ashx",
            },
            "height": "100%",
            "width": "100%"
        });
</script>
```

-   3、完整代码

```html
<!DOCTYPE html>
<html style="height: 100%;">
    <head>
        <meta charset="UTF-8" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
        <title>ONLYOFFICE</title>
    </head>
    <body style="height: 100%; margin: 0;">
        <div id="placeholder" style="height: 100%"></div>
        <script
            type="text/javascript"
            src="https://documentserver/web-apps/apps/api/documents/api.js"
        ></script>

        <script type="text/javascript">
            window.docEditor = new DocsAPI.DocEditor("placeholder", {
                documentType: "text", // 文档类型 'text' | 'spreadsheet' | 'presentation'
                type: "desktop", // 文档打开的样式类型 'desktop or mobile'
                document: {
                    fileType: "docx", // 文件类型
                    key:
                        "OVpYZjd5VE5BX1NNZGd1QTY5cXlCZzJHc0psdHUyempyZEZxTlBBOEsyWEg0NUtmOVZ5YWtuaFYzU0ZhWGVnWlozRGhQa2VManlXa1d4",
                    title: "",
                    url:
                        "http://documentserver/files/data/" +
                        this.$route.query.attachment,
                    permissions: {
                        // 权限配置
                        reader: true,
                        download: false, // 下载
                        edit: false, // 编辑
                        print: false, // 打印
                        review: false,
                        rename: true,
                        changeHistory: false,
                    },
                },
                editorConfig: {
                    // 定义与编辑器界面有关的参数：打开模式（查看器或编辑器），界面语言，附加按钮等）
                    mode: "view", // 界面是编辑还是预览 view、edit
                    canAutosave: true,
                    canCoAuthoring: true,
                    callbackUrl:
                        "http://documentserver/index.php?mod=onlyoffice&do=savefile&path=OVpYZjd5VE5BX1NNZGd1QTY5cXlCZzJHc0psdHUyempyZEZxTlBBOEsyWEg0NUtmOVZ5YWtuaFYzU0ZhWGVnWlozRGhQa2VManlXa1d4&uid=0",
                    createUrl: "", // 定义文档创建保存的绝对URL
                    lang: "zh-CN", // 语言
                    location: "zh-CN",
                    // "user": {
                    //   id: '27',
                    //   firstname: '郭兴刚',
                    //   name: '郭兴刚'
                    // },
                    customization: {
                        logo: {
                            // image: null,
                            // imageEmbedded: null,
                            url: "https://www.baidu.com/",
                        },
                        chat: false,
                        comments: false,
                        goback: false,
                        compactToolbar: true,
                        about: false,
                        leftMenu: true,
                        rightMenu: true,
                        toolbar: true,
                        header: false,
                        autosave: true,
                    },
                },
                events: {
                    onReady: function () {},
                    onBack: function () {},
                    onError: function () {},
                    onSave: function () {},
                },
            });
        </script>
    </body>
</html>
```

###### vue 使用

vue 的使用与 HTML 大同小异

```vue
<template>
    <div style="height: 100vh">
        <div id="placeholder" style="height: 100%"></div>
    </div>
</template>

<script
    type="text/javascript"
    src="http://documentserver/web-apps/apps/api/documents/api.js"
></script>
<script>
// import onlyOffice from './word.js'
export default {
    data() {
        return {
            key: "",
        };
    },
    mounted() {
        this.onlyOfficeInit();
    },
    methods: {
        // 随机字符串
        randomString(len) {
            len = len || 32;
            var $chars =
                "ABCDEFGHJKMNPQRSTWXYZabcdefhijkmnprstwxyz2345678"; /****默认去掉了容易混淆的字符oOLl,9gq,Vv,Uu,I1****/
            var maxPos = $chars.length;
            var pwd = "";
            for (i = 0; i < len; i++) {
                pwd += $chars.charAt(Math.floor(Math.random() * maxPos));
            }
            this.key = pwd;
        },
        onlyOfficeInit() {
            window.docEditor = new window.DocsAPI.DocEditor("placeholder", {
                documentType: "text", // 文档类型 'text' | 'spreadsheet' | 'presentation'
                type: "desktop", // 文档打开的样式类型 'desktop or mobile'
                document: {
                    fileType: "docx", // 文件类型
                    key: this.key,
                    title: this.$route.query.name,
                    url:
                        "http://documentserver/files/data/" +
                        this.$route.query.attachment,
                    permissions: {
                        // 权限配置
                        reader: true,
                        download: false, // 下载
                        edit: false, // 编辑
                        print: false, // 打印
                        review: false,
                        rename: true,
                        changeHistory: false,
                    },
                },
                editorConfig: {
                    // 定义与编辑器界面有关的参数：打开模式（查看器或编辑器），界面语言，附加按钮等）
                    mode: "view", // 界面是编辑还是预览 view、edit
                    canAutosave: true,
                    canCoAuthoring: true,
                    callbackUrl:
                        "http://documentserver/index.php?mod=onlyoffice&do=savefile&path=OVpYZjd5VE5BX1NNZGd1QTY5cXlCZzJHc0psdHUyempyZEZxTlBBOEsyWEg0NUtmOVZ5YWtuaFYzU0ZhWGVnWlozRGhQa2VManlXa1d4&uid=0",
                    createUrl: "", // 定义文档创建保存的绝对URL
                    lang: "zh-CN", // 语言
                    location: "zh-CN",
                    // "user": {
                    //   id: '27',
                    //   firstname: '酒笙',
                    //   name: '酒笙'
                    // },
                    customization: {
                        logo: {
                            // image: null,
                            // imageEmbedded: null,
                            url: "https://www.baidu.com/",
                        },
                        chat: false,
                        comments: false,
                        goback: false,
                        compactToolbar: true,
                        about: false,
                        leftMenu: true,
                        rightMenu: true,
                        toolbar: true,
                        header: false,
                        autosave: true,
                    },
                },
                events: {
                    onReady: function () {},
                    onBack: function () {},
                    onError: function () {},
                    onSave: function () {},
                },
            });
        },
    },
};
</script>

<style scoped lang="scss">
#header-logo {
    display: none;
}
</style>
```
