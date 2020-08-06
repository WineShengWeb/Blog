# vue 中事件监听 watch

vue 中 watch 实际上是用来监听 vue 实例中的数据变化

监听 String

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

监听对象

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

监听路由

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
