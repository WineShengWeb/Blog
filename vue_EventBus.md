# vue 传值之中央事件总线（EventBus）

##### 1、创建中央事件总线

在 `main.js` 中创建

```JavaScript
// 全局事件总线
Vue.prototype.Bus = new Vue();

// 特别注意：$emit 和 $on 的事件必须在一个公共的实例上
```

##### 2、使用中央事件总线传值

在 `pageA` 页面传值

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
        },
    },
};
</script>
```

##### 3、接受值

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
    },
};
</script>

<style scoped lang="scss"></style>
```

##### 4、效果

-   1、点击前

![图1](./chart/1.png)

-   2、点击后

![图2](./chart/2.png)

##### 5、`$emit`、 `$on` 、`$off`

1、vm.\$on( event, callback )

-   监听当前实例上的自定义事件。事件可以由 vm.\$emit 触发。回调函数会接收所有传入事件触发函数的额外参数。

2、vm.\$emit( event, […args] )

-   触发当前实例上的事件。附加参数都会传给监听器回调，如果没有参数，形式为 vm.\$emit(event)

3、vm.\$off( [event, callback] )

-   移除自定义事件监听器。
-   如果没有提供参数，则移除所有的事件监听器；
-   如果只提供了事件，则移除该事件所有的监听器；
-   如果同时提供了事件与回调，则只移除这个回调的监听器。
