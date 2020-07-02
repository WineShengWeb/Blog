# vue 中 slot 插槽详解

插槽含义：就是引入子组件后，在插入子组件元素中添加信息或者标签，使得子组件的指定位置插入信息或者标签

插槽有三种：默认插槽、具名插槽、作用域插槽，由于 vue2.6.0 后对插槽进行修改，但是兼容 2.6.0 前的版本，博文中只说明 2.6.0 后的插槽，vue3.0 后面会去除 2.60 前的版本兼容

##### 有什么用

> 调用组件时，写在组件标签内的内容，默认不会被渲染
> 有时，需要组件标签内的内容能被渲染出来，slot 插槽实现

##### slot 的基本使用

> 1、定义组件时想好要在哪个位置去渲染 slot 内容
> 2、在想好的位置哪里，放置一个 slot 标签 即可 <slot></slot>
> 3、slot 内容 就会自动去替换 slot 标签

##### 默认插槽

> 写在 slot 标签内的内容就是这个 slot 标签的默认内容

子组件定义插槽

```vue
<template>
    <div>
        <div>我是子组件</div>
        <slot></slot>
    </div>
</template>
```

父组件调用子组件

```vue
<template>
    <div>
        <children>
            <div>我是默认插槽</div>
        </children>
    </div>
</template>
```

##### 具名插槽

给 slot 标签 设置一个 name 属性。这时 slot 标签叫做 具名 slot 标签

> 1、slot 在一个组件内是可以使用多次的
> 2、给 slot 取了名字之后，slot 内容想要 渲染在哪个 slot，就需要设置 slot 属性。属性的值为某个 slot 的名

-   slot 有一个默认的名字，就叫做 default，<slot></slot> => <slot name="default"></slot>

子组件定义插槽

```vue
<template>
    <div>
        <div>我是子组件</div>
        <slot name="top"></slot>
        <slot></slot>
    </div>
</template>
```

父组件调用子组件

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

##### 作用域插槽

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

##### v-slot

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
        <p slot="top" slot-scope="{ msg, age }">
            我的天-{{ msg }} - {{ age }}
        </p>
    </world>

    <!-- 新语法的作用域插槽使用 -->
    <world>
        <template #top="obj">
            <p>
                我的天-{{ obj.msg }} - {{ obj.age }}
            </p>
        </template>
    </world>

    <!-- 新语法的作用域插槽使用 解构赋值-->
    <world>
        <template #top="{ msg, age }">
            <p>
                我的天-{{ msg }} - {{ age }}
            </p>
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
