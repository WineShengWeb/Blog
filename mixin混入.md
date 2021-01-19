# vue mixin 组件混入学习笔记

#### 准备页面文件

1、准备一个页面 pageA.vue。

```vue
<template>
    <div>pageA的值是:</div>
</template>

<script>
export default {
    data() {
        return {};
    },
};
</script>

<style scoped></style>
```

2、在 src 目录下新建 mixin 文件夹，在 mixin 文件夹中新建 mixin.js 文件。混入对象跟 Vue 实例的格式是一样的。

```js
//抛出混入对象，方便外部访问
export const mixin = {
    data() {
        return {
            number: 10,
        };
    },
};
```

#### 局部混入

pageA 页面

```vue
<template>
    //这里读的 number 值其实是 mixin 的值，因为这个时候 mixin 已经混入到 vue
    实例中了
    <div>pageA的值是:{{ number }}</div>
</template>

<script>
//引入mixin.js
import { mixin } from "./mixin/mixin";
export default {
    //这里注意：属性名为mixins，值为数组类型
    mixins: [mixin],
    data() {
        return {};
    },
};
</script>

<style scoped></style>
```

#### 全局混入

> 全局混入我们只需要把 mixin.js 引入到 main.js 中，然后将 mixin 放入到 Vue.mixin()方法中即可；
> 注意：全局混入更为便捷，我们将不用在子组件声明，全局混入将会影响每一个组件的实例，使用的时候需要小心谨慎；这样全局混入之后，我们可以直接在组件中通过 this.变量/方法来调用 mixin 混入对象的变量/方法

main.js 文件

```js
// 引入
import mixin from "./mixin/mixin.js";
// 实例化
Vue.mixin(mixin);
```

#### mixin 混入对象和 Vuex 的区别

-   Vuex 是状态共享管理，所以 Vuex 中的所有变量和方法都是可以读取和更改并相互影响的；

-   mixin 可以定义公用的变量或方法，但是 mixin 中的数据是不共享的，也就是每个组件中的 mixin 实例都是不一样的，都是单独存在的个体，不存在相互影响的；

-   mixin 混入对象值为函数的同名函数选项将会进行递归合并为数组，两个函数都会执行，只不过先执行 mixin 中的同名函数；

-   mixin 混入对象值为对象的同名对象将会进行替换，都优先执行组件内的同名对象，也就是组件内的同名对象将 mixin 混入对象的同名对象进行覆盖；
