# vue 学习笔记

### 一、vue 中 slot 插槽详解

插槽含义：就是引入子组件后，在插入子组件元素中添加信息或者标签，使得子组件的指定位置插入信息或者标签

插槽有三种：默认插槽、具名插槽、作用域插槽，由于 vue2.6.0 后对插槽进行修改，但是兼容 2.6.0 前的版本，博文中只说明 2.6.0 后的插槽，vue3.0 后面会去除 2.60 前的版本兼容

-   有什么用

> 调用组件时，写在组件标签内的内容，默认不会被渲染
> 有时，需要组件标签内的内容能被渲染出来，slot 插槽实现

-   slot 的基本使用

> 1、定义组件时想好要在哪个位置去渲染 slot 内容
> 2、在想好的位置哪里，放置一个 slot 标签 即可 <slot></slot>
> 3、slot 内容 就会自动去替换 slot 标签

##### 1、默认插槽

> 写在 slot 标签内的内容就是这个 slot 标签的默认内容

-   子组件定义插槽

```vue
<template>
    <div>
        <div>我是子组件</div>
        <slot></slot>
    </div>
</template>
```

-   父组件调用子组件

```vue
<template>
    <div>
        <children>
            <div>我是默认插槽</div>
        </children>
    </div>
</template>
```

##### 2、具名插槽

给 slot 标签 设置一个 name 属性。这时 slot 标签叫做 具名 slot 标签

> 1、slot 在一个组件内是可以使用多次的
> 2、给 slot 取了名字之后，slot 内容想要 渲染在哪个 slot，就需要设置 slot 属性。属性的值为某个 slot 的名

-   slot 有一个默认的名字，就叫做 default，<slot></slot> => <slot name="default"></slot>

-   子组件定义插槽

```vue
<template>
    <div>
        <div>我是子组件</div>
        <slot name="top"></slot>
        <slot></slot>
    </div>
</template>
```

-   父组件调用子组件

```vue
<template>
    <div>
        <children>
            <div>你好</div>
            <div slot="top">加油</div>
        </children>
    </div>
</template>
```

##### 3、作用域插槽

> 插槽内容 中使用 子组件中的作用域

```html
<div id="app">
    <hello>
        // xxxx 如何能够用上 hello 组件中 的 msg 数据
        <p>我是一个插槽内容。xxxx</p>
    </hello>
</div>
```

-   1.定义组件的 slot 的时候，将要在插槽内容中使用的数据，绑定在 slot 标签上
    `<slot :a="msg" :b="age" ></slot>`
-   2.在插槽内容的标签上，设置 slot-scope 属性。属性值随便写。这个属性值就是上一个步骤中绑定出来的数据的一个大对象
    `<p slot-scope="obj">我是一个插槽内容。msg, age</p>`
    `obj === { a: "hello", b: 19 }`

> 注意：不能绑定 name 属性。因为 name 属性有特殊用途。name 属性用来做具名插槽的。

```html
<div id="app">
    <hello>
        <p slot-scope="{a,b}">{{b}}{{a}}</p>
    </hello>
</div>
<script src="https://cdn.jsdelivr.net/npm/vue@2.6.11/dist/vue.js"></script>
<script>
    Vue.component("hello", {
        data: function () {
            return {
                msg: "hello",
                age: 2,
            };
        },
        template: `
                <div>
                    <slot :a='msg' :b='age'></slot>
                    <h1>1</h1>
                </div>
            `,
    });
    var vm = new Vue({
        el: "#app",
        data: {},
    });
</script>
```

##### 4、v-slot

slot 插槽 在 2.6.0 这个版本的时候，做了更新。提供了一个新的指令叫做 v-slot。
后续实现具名插槽与作用域插槽都使用 v-slot 来实现

v-slot 语法
v-slot:xxxx=yyyy
xxxx 插槽名字
yyyy 作用域插槽数据

> 1、v-slot 必须用在 template 元素上。
> 2、如果插槽没有设置 name 名字的话： v-slot => v-slot:default
> 3、v-slot 简写 #：注意: 使用 简写时必须携带名字。默认的名字需要写成： ' #default '
> 4、插槽只有一个的情况下，可以不使用 template 去包裹插槽内容。而是直接将 v-slot 写在组件标签上。

```html
<div id="app">
    <helloworld2 #bottom>
        <p>加油</p>
    </helloworld2>
    <hr />
    <helloworld>
        <template #top>
            <p>我的天</p>
        </template>

        <template #default>
            <p>我的地</p>
        </template>
    </helloworld>

    <hr />

    <!-- 老语法的具名插槽使用 -->
    <hello>
        <p slot="top">我的天</p>

        <p slot="bottom">我的地</p>
    </hello>
    <!-- 新语法的具名插槽使用 -->
    <hello>
        <template #top>
            <p>我的天</p>
        </template>

        <template #bottom>
            <p>我的地</p>
        </template>
    </hello>

    <!-- 老语法的作用域插槽使用 -->
    <world>
        <p slot="top" slot-scope="{ msg, age }">我的天-{{ msg }} - {{ age }}</p>
    </world>

    <!-- 新语法的作用域插槽使用 -->
    <world>
        <template #top="obj">
            <p>我的天-{{ obj.msg }} - {{ obj.age }}</p>
        </template>
    </world>

    <!-- 新语法的作用域插槽使用 解构赋值-->
    <world>
        <template #top="{ msg, age }">
            <p>我的天-{{ msg }} - {{ age }}</p>
        </template>
    </world>
</div>

<script src="https://cdn.jsdelivr.net/npm/vue@2.6.11/dist/vue.js"></script>
<script>
    Vue.component("hello", {
        template: `
        <div>
        <slot name="top"></slot>
        <h1>hello</h1>
        <slot name="bottom"></slot>
        </div>
    `,
    });
    Vue.component("world", {
        data() {
            return {
                msg: "张三",
                age: 18,
            };
        },
        template: `
        <div>
        <slot name="top" :msg="msg" :age="age"></slot>
        <h1>world</h1>
        <slot name="bottom"></slot>
        </div>
    `,
    });
    Vue.component("helloworld", {
        template: `
        <div>
        <slot name="top"></slot>
        <h1>helloworld</h1>
        <slot></slot>
        </div>
    `,
    });
    Vue.component("helloworld2", {
        template: `
        <div>
        <h1>helloworld2</h1>
        <slot name="bottom"></slot>
        </div>
    `,
    });
    var vm = new Vue({
        el: "#app",
    });
</script>
```

将组件标签内的内容渲染出来，使用 slot 插槽
然后又想在插槽内使用组件内的数据：

1.先在 slot 标签上用动态属性的形式接收数据,例如:
:属性名='组件内的变量名'
`<slot :a='msg' :b='age'></slot>`

2.在插槽内容的标签上，设置 slot-scope
`<p slot-scope='{a,b}'>{{b}}{{a}}</p>`

3.新语法: v-slot 写在 template 上，
<template #top="{ msg, age }"> ====> v-slot= slot + slot-scope 具名+作用域'

4.默认：#default (default 不可省略)

### 二、vue 中事件监听 watch

vue 中 watch 实际上是用来监听 vue 实例中的数据变化

##### 1、监听 String

```vue
<template>
    <div @click="stringClick">{{ msg }}</div>
</template>

<script>
export default {
    name: "jianting",
    data() {
        return {
            msg: "1223",
        };
    },
    watch: {
        msg: function (newVal, oldVal) {
            // TO DO
            console.log("newVal:", newVal);
            console.log("oldVal:", oldVal);
        },
    },
    methods: {
        stringClick() {
            this.msg = Math.random() * 100;
        },
    },
};
</script>
```

##### 2、监听对象

```vue
<template>
    <div @click="click">
        <div>姓名：{{ obj.name }}，年龄：{{ obj.age }}，他的儿女有：</div>
        <div v-for="(item, index) in obj.children" :key="index">
            姓名：{{ item.name }}，年龄：{{ item.age }}
        </div>
    </div>
</template>

<script>
export default {
    name: "jianting",
    data() {
        return {
            obj: {
                name: "Tony",
                age: 50,
                children: [
                    {
                        name: "小明",
                        age: 12,
                    },
                    {
                        name: "小花",
                        age: 5,
                    },
                ],
            },
        };
    },
    watch: {
        obj: {
            handler: function (newVal, oldVal) {
                // TO DO
                console.log("newVal:", newVal);
                console.log("oldVal:", oldVal);
            },
            deep: true,
            immediate: true,
        },
        "obj.name": function (newVal, oldVal) {
            // TO DO
            console.log("newVal obj.name:", newVal);
            console.log("oldVal obj.name:", oldVal);
        },
    },
    methods: {
        click() {
            this.obj.name = "未知";
        },
    },
};
</script>
```

watch 监听对象的时候，需要加 deep:true，只有这样才能深入底层去实时监听，没有加的话，对象是监听不到变化的,添加 immediate 时会在侦听开始之后被立即调用

##### 3、监听路由

```vue
<template>
    <div @click="stringClick">{{ msg }}</div>
</template>

<script>
export default {
    name: "jianting",
    data() {
        return {
            msg: "1223",
        };
    },
    watch: {
        $route: {
            handler: function (val, oldVal) {
                console.log(val);
            },
            // 深度观察监听
            deep: true,
            immediate: true,
        },
    },
};
</script>
```

### 三、vue 传值之中央事件总线（EventBus）

在 vue 中，我们父子之间通信简单明了：

父组件向子组件传值： props，

在父组件中，用 ：要传递过去的名字 = “ 要传递的值 ”。

在子组件中 使用 props:{}接受即可

子组件向父组件传值：\$emit. 通过自定义方法，

在子组件中，我们使用 this.\$emit('方法名'，参数)，向父组件传值

在父组件中，我们使用子组件传递过来的自定义方法 ： @自定义方法名 = “ 自己随便写一个方法名，不需要跟参数，在下面使用该方法时，再写到（）中 ”

以上，是关于 vue 中父子组件通信的方法，

那么非父子组件之间的通信，又是怎么样的呢？

其实也很简单，有两种方法：

1.通过 Vuex, Vuex 中的 state.是可以共用的属性。通过调用 Vue.state 就可以获取到，非父子组件之间通信就可以解决

2.通过\$bus, 事件总线

##### 1、创建中央事件总线

首先呢。我们需要去在 `main.js` 中创建 bus

```JavaScript
// 全局事件总线
Vue.prototype.Bus = new Vue();
// Vue.prototype.$bus = new Vue()

// 特别注意：$emit 和 $on 的事件必须在一个公共的实例上
```

##### 2、使用中央事件总线传值

在 `pageA` 页面传值

然后，我们就可以使用 this.$bus.$emit(’事件名称‘，参数) 发送

```vue
<template>
    <div>
        pageA：
        <button @click="change">点击发送</button>
    </div>
</template>

<script>
export default {
    data() {
        return {
            msg: "我是A发送的消息",
        };
    },
    methods: {
        change() {
            // this.$emit（'自定义事件名',要传送的数据）；
            // 触发当前实例上的事件，要传递的数据会传给监听器；
            this.Bus.$emit("sendMsg", this.msg); // sendMsg:自定义事件名,this.msg:要传送的数据
            // this.$bus.$emit("test", res);
        },
    },
};
</script>
```

##### 3、接收值

最后，我们可以通过 this.$bus.$on('事件名称',function(参数){}) 接收

```vue
<template>
    <div>pageB： {{ message }}</div>
</template>

<script>
export default {
    data() {
        return {
            message: "我是B组件",
        };
    },
    mounted() {
        // VM.$on('事件名',callback) ---callback回调$emit要传送的数据；
        // 监听当前实例上自定义事件；
        this.Bus.$on("sendMsg", (msg) => {
            // sendMsg:监听的自定义事件名; msg: 传送过来数据的回调
            this.message = msg;
        });
        // this.$bus.$on("test", (message) => {
        //     this.projectArr.unshift(message.data);
        // });
    },
};
</script>

<style scoped lang="scss"></style>
```

这样。我们就可以通过事件总线获取到非父子组件通信

##### 4、效果

-   1、点击前

![图1](./chart/1.png)

-   2、点击后

![图2](./chart/2.png)

### 四、vue 中 v-if 判断 length 报错 undefined

在 `vue` 中使用 `v-if` 判断一个数组或字符串长度是否为 `0` 时，会出现 `length` 是 `undefined` 的错误：

`[Vue warn]: Error in render: "TypeError: Cannot read property 'length' of undefined"`

错误代码：

```vue
<template>
    <div>
        <div v-if="list.length == 0">暂无数据</div>
        <div v-else>
            <div v-for="item in list" :key="item.id">{{ item }}</div>
        </div>
    </div>
</template>
```

造成这个错误的原因是因为没有预先判断数组或字符串是否存在，需要先对数组或字符串进行非空验证：`list.length != undefined`

```vue
<template>
    <div>
        <div v-if="list.length != undefined && list.length == 0">暂无数据</div>
        <div v-else>
            <div v-for="item in list" :key="item.id">{{ item }}</div>
        </div>
    </div>
</template>
```

### 五、vue 中开发环境和生产环境的配置

##### 1、开发环境

所有的开发和配置在这个环境里进行。一般情况下，只有这个环境可以改配置和进行开发，并且一般不在这个环境下创建数据。（开发环境就是每个开发人员电脑上的开发环境，只有开发人员可以配置和开发，写数据测试放在测试环境）

在根目录下新建 `.env.development` 文件

```js
// VUE_APP_URL= url;
VUE_APP_URL = "http://192.168.1.106:8083/api/v1";
```

##### 2、生产环境

正式使用的系统环境。 一般情况下，一个环境对应一个服务器，也有一些公司把开发、测试等环境放到一个服务器的。（从 SVN 上通过 FTP 下载下来，然后在服务器上的 tomcat 部署、发布，服务器是 linux 的）

在根目录下新建 `.env.production` 文件

```js
// VUE_APP_URL = url;
VUE_APP_URL = "http://192.168.12.108:8883/api/v1";
```

##### 3、在 `axios` 中使用

```js
const service = axios.create({
    baseURL: process.env.BASE_API, // 配置在config/prod.env里的baseApi
    timeout: 5000, // 超时时间
});
```

### 六、`vue.config.js` 配置详解

```js
module.exports={
    //部署应用包时的基本url。
    //baseUrl:"/",//从 Vue CLI 3.3 起已弃用
    publicPath: process.env.NODE_ENV === "production" ? "./" : "./",
    publicPath:"/"，
    //默认情况下，Vue CLI 会假设你的应用是被部署在一个域名的根路径上，例如 https://www.my-app.com/。
    //如果应用被部署在一个子路径上，你就需要用这个选项指定这个子路径。例如，如果你的应用被部署在 https://www.my-app.com/my-app/，则设置 publicPath 为 /my-app/。
    //这个值也可以被设置为空字符串 ('') 或是相对路径 ('./')，这样所有的资源都会被链接为相对路径，这样打出来的包可以被部署在任意路径，也可以用在类似 Cordova hybrid 应用的文件系统中。
    //也可以使用三元运算符配置开发和正式环境上不同的路径

    outputDir:"dist",//打包后生成的生产环境构建文件的目录，dist是默认值。默认情况下每次打包都会清空上次打包文件（构建时传入 --no-clean 可关闭该行为）。
    //官方提示:始终使用outputDir，而不要修改 webpack 的 output.path。
    assetsDir:"",//放置生成的静态资源 (js、css、img、fonts) 的 (相对于 outputDir 的) 目录
    indexPath:"index.html",//指定生成的 index.html 的输出路径 (相对于 outputDir)。也可以是一个绝对路径。
    filenameHashing:true,//默认情况下，生成的静态资源在它们的文件名中包含了 hash 以便更好的控制缓存。然而，这也要求 index 的 HTML 是被 Vue CLI 自动生成的。如果你无法使用 Vue CLI 生成的 index HTML，你可以通过将这个选项设为 false 来关闭文件名哈希。

    //默认是undefined，配置类型是Object，这也是多页面应用的所需要配置的（具体方式，请先找度娘）
    pages:{
        index:{
          // page 的入口
          entry: 'src/index/main.js',
          // 模板来源
          template: 'public/index.html',
          // 在 dist/index.html 的输出
          filename: 'index.html',
          // 当使用 title 选项时，
          // template 中的 title 标签需要是 <title><%= htmlWebpackPlugin.options.title %></title>
          title: 'Index Page',
          // 在这个页面中包含的块，默认情况下会包含
          // 提取出来的通用 chunk 和 vendor chunk。
          chunks: ['chunk-vendors', 'chunk-common', 'index']
        },
        // 当使用只有入口的字符串格式时，
        // 模板会被推导为 `public/subpage.html`
        // 并且如果找不到的话，就回退到 `public/index.html`。
        // 输出文件名会被推导为 `subpage.html`。
        subpage: 'src/subpage/main.js'
    },

    lintOnSave:true,//在保存后eslint检查代码。将值设置为'error'是把错误直接输出为编译错误。process.env.NODE_ENV !== 'production'，在生产环境上设为false。


    runtimeCompiler:false,//是否使用包含运行时编译器的 Vue 构建版本。设置为 true 后你就可以在 Vue 组件中使用 template 选项了，但是这会让你的应用额外增加 10kb 左右。
    transpileDependencies:[],//默认情况下 babel-loader 会忽略所有 node_modules 中的文件。如果你想要通过 Babel 显式转译一个依赖，可以在这个选项中列出来。
    productionSourceMap:true,//如果你不需要生产环境的 source map，可以将其设置为 false 以加速生产环境构建。
    //在打包完成后文件夹中有.map文件，他的作用是在打包完成后，如果运行时报错，没有.map文件不能找到报错信息的准确位置。

    crossorigin:undefined,//设置类型是Sring，设置生成的 HTML 中 <link rel="stylesheet"> 和 <script> 标签的 crossorigin 属性。需要注意的是该选项仅影响由 html-webpack-plugin 在构建时注入的标签 - 直接写在模版 (public/index.html) 中的标签不受影响。
    integrity:false,//在生成的 HTML 中的 <link rel="stylesheet"> 和 <script> 标签上启用 Subresource Integrity (SRI)。如果你构建后的文件是部署在 CDN 上的，启用该选项可以提供额外的安全性。
    //需要注意的是该选项仅影响由 html-webpack-plugin 在构建时注入的标签 - 直接写在模版 (public/index.html) 中的标签不受影响。
    //另外，当启用 SRI 时，preload resource hints 会被禁用，因为 Chrome 的一个 bug 会导致文件被下载两次。
    configureWebpack:Object|Function,//如果这个值是一个对象，则会通过 webpack-merge 合并到最终的配置中。
    //如果这个值是一个函数，则会接收被解析的配置作为参数。该函数及可以修改配置并不返回任何东西，也可以返回一个被克隆或合并过的配置版本。

    chainWebpack:Function,//是一个函数，会接收一个基于 webpack-chain 的 ChainableConfig 实例。允许对内部的 webpack 配置进行更细粒度的修改。

    //css.loaderOptions:{},//Object,默认是{},向 CSS 相关的 loader 传递选项
    css: {
        modules:false,//默认情况下，只有 *.module.[ext] 结尾的文件才会被视作 CSS Modules 模块。设置为 true 后你就可以去掉文件名中的 .module 并将所有的 *.(css|scss|sass|less|styl(us)?) 文件视为 CSS Modules 模块。
        extract:Boolean,//生产环境下是 true，开发环境下是 false,是否将组件中的 CSS 提取至一个独立的 CSS 文件中 (而不是动态注入到 JavaScript 中的 inline 代码)。
        //同样当构建 Web Components 组件时它总是会被禁用 (样式是 inline 的并注入到了 shadowRoot 中)。
        //当作为一个库构建时，你也可以将其设置为 false 免得用户自己导入 CSS。
        //提取 CSS 在开发环境模式下是默认不开启的，因为它和 CSS 热重载不兼容。然而，你仍然可以将这个值显性地设置为 true 在所有情况下都强制提取。
        sourceMap:false,//Boolean,是否为 CSS 开启 source map。设置为 true 之后可能会影响构建的性能。
        loaderOptions: {
          css: {
            // 这里的选项会传递给 css-loader
          },
          postcss: {
            // 这里的选项会传递给 postcss-loader
          }
        }
     }
     //支持的 loader 有：css-loader,postcss-loader,sass-loader,less-loader,stylus-loader

    devServer:{
        clientLogLevel:'silent' | 'trace' | 'debug' | 'info' | 'warn' | 'error' | 'none' | 'warning',//使用内联模式时，DevTools中的控制台将显示消息，例如在重新加载之前，错误之前或启用热模块更换时。默认为info
        historyApiFallback: true,//使用HTML5历史记录API时，index.html可能必须提供该页面以代替任何404回复。devServer.historyApiFallback默认情况下禁用。通过传递启用它
        hot: true,//热模块替换，就是热更新页面
        compress: true,//为所服务的一切启用gzip压缩
        host: 'localhost',//指定要使用的主机。默认情况下这是localhost。
        port: 8080//端口号，
        //所有 webpack-dev-server 的选项都支持。注意：
        //有些值像 host、port 和 https 可能会被命令行参数覆写。
        //有些值像 publicPath 和 historyApiFallback 不应该被修改，因为它们需要和开发服务器的 publicPath 同步以保障正常的工作。

        //proxy:"url地址",//前端应用和后台API服务没有运行在一个主机上，设置此项在开发环境下代理到API服务器。
        proxy:{//配置不同的后台API地址
            '/api': {
                target: '<url>',
                ws: true,
                changeOrigin: true,
                pathRewrite: {
                  "^/api": "/"
                }
              },
              '/foo': {
                target: '<other_url>'
              }
        }
    }，

    parallel:require('os').cpus().length > 1,//Boolean,是否为 Babel 或 TypeScript 使用 thread-loader。该选项在系统的 CPU 有多于一个内核时自动启用，仅作用于生产构建。

   pwa:{},//向 PWA 插件传递选项。

   pluginOptions:{},//一个不进行任何 schema 验证的对象，因此它可以用来传递任何第三方插件选项


}
```
