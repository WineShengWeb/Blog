<!--
 * @Author: guoxinggang<guoxinggang@gsaxns.com>
 * @Version: 1.0
 * @Date: 2019-08-09 17:48:59
 * @LastEditTime: 2019-08-21 16:59:13
 * @Description:
 -->

# <center>VS code 常用插件及配置</center>

## 1. Auto Close Tag

- 作用：自动闭合 HTML 标签；

## 2. Auto Rename Tag

- 作用：自动完成另一侧标签的同步修改；

## 3. Babel JavaScript

- 作用：支持 ES201X、React、FlowType 以及 GraphQL 的语法高亮。

## 4. Beautify

- 作用：格式化 html ,js,css；

- 配置：安装后打开设置，在搜索栏中输入：**Beautify**，找到 **在 setting.json 中设置**，打开 **setting.json**，在里面输入：

        "beautify.language": {

                "js": {
                    "type": [
                        "javascript",
                        "json"
                    ],
                    "filename": [
                        ".jshintrc",
                        ".jsbeautify"
                    ]
                },
                "css": [
                    "css",
                    "scss"
                ],
                "html": [
                    "htm",
                    "html",
                    "vue"//在这里加上vue
                ]
        }

## 5. Bracket Pair Colorizer

- 作用：给括号加上不同的颜色，便于区分不同的区块，使用者可以定义不同括号类型和不同颜色；

## 6. Chinese (Simplified) Language Pack for Visual Studio Code

- 作用：VS code 的中文插件

## 7. Document This

- 作用：自动注释插件；

## 8. ESLint

- 作用：js 语法纠错；

- 配置：

        // 保存时自动格式化
        "editor.formatOnPaste": true,
        // 是否开启eslint检测
        "eslint.enable": true,
        // 文件保存时，是否自动根据eslint进行格式化
        "eslint.autoFixOnSave": true,
        // eslint配置文件
        "eslint.options": {
            "configFile": "E:/aaaworkspace/all-template/template-pc-vue-elementui/.eslintrc.js",
            "plugins": ["html"]
        },
        "eslint.validate": [
            "javascript",
            "javascriptreact",
            {
                "language": "html",
                // 保存文件时，自动格式化
                "autoFix": true
            },
            {
                "language": "vue",
                "autoFix": true
            },
            "typescript",
            "typescriptreact"
        ]

## 9. HTML CSS Support

- 作用：智能提示 CSS 类名以及 id。

## 10. HTML Snippets

- 作用：智能提示 HTML 标签，以及标签含义。

## 11. Image preview

- 作用：图片预览工具

## 12. ivue

- 作用：可以快速生成 vue 组件

## 13. JavaScript (ES6) code snippets

- 作用：ES6 语法智能提示，以及快速输入，不仅仅支持.js，还支持.ts，.jsx，.tsx，.html，.vue，省去了配置其支持各种包含 js 代码文件的时间

## 14. jQuery Code Snippets

- 作用：juqery 提示插件

## 15. koroFileHeader

- 作用：生成文件头部注释

- 配置：

        "fileheader.configObj": {

            "createFileTime": true, //设置为true则为文件新建时候作为date，否则注释生成时间为date
            "autoAdd": true, //自动生成注释，老是忘记的同学可以设置
            "annotationStr": {
            "head": "/*",
            "middle": " * @",
            "end": " */",
            "use": true //设置自定义注释可用
            }
        },

        "fileheader.cursorMode": {

            "description": "",
            "param ": "",
            "return": ""
        },
        "fileheader.customMade": {

            "Author": "xxx<xxx@163.com>", //作者
            "Version": "1.0", //版本号
            "Date": "Do not edit", //时间
            "LastEditTime": "Do not edit", //最后修改时间
            "Description": "" //文件内容描述

  }

## 16. markdownlint

- 作用：markdown 语法纠错

## 17. Markdown Preview Enhanced

- 作用：实时预览 markdown

## 18. open in browser

- 作用：在浏览器中打开当前文件，快捷键：**alt+b**

## 20. SVG Viewer

- 作用：支持打开 SVG 文件并查看。同时，它还包含了用于转换为 PNG 格式和生成数据 URI 模式的选项

## 21. Vetur

- 作用：vue 语法高亮/格式化/代码片段/语法检查等

- 配置：

        // vetur 插件
        "extensions.ignoreRecommendations": true,
        "emmet.syntaxProfiles": {
            "vue-html": "html",
            "vue": "html"
        },
        "vetur.validation.template": false,
        "eslint.options": {
            "plugins": ["html"]
        },
        "eslint.validate": ["javascript", "javascriptreact", "html", "vue"],
        "prettier.singleQuote": true,
        "prettier.semi": false,
        "vetur.format.defaultFormatter.html": "js-beautify-html",
        "vetur.format.defaultFormatterOptions": {
            "wrap_attributes": "force-aligned"
        }

        // vue 模板
        "Print to console": {
            "prefix": "vue",
            "body": [
            "<template>",
            "  <div class=\"main\">\n",
            "  </div>",
            "</template>\n",
            "<script>",
            "export default {",
            "  components: {\n",
            "  },",
            "  data() {",
            "    return {\n",
            "    }",
            "  },",
            "  methods: {\n",
            "  },",
            "  computed: { },",
            "  watch: { },",
            "  mounted() {\n",
            "  },",
            "}\n",
            "</script>\n",
            "<style scoped lang=\"less\">\n",
            ".main {\n",
            "}",
            "</style>",
            "$2"
            ],
            "description": "Log output to console"
        }
