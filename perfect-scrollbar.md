## perfect-scrollbar 插件学习

perfect-scrollbar 是一款轻量级的滚动插件，具体介绍详见其[官网](https://github.com/mdbootstrap/perfect-scrollbar)
你只需要知道它绝对不是为了 vue 设计的，和 vue 没半毛钱关系。

#### 安装

```node
npm install classlist-polyfill --save
npm install perfect-scrollbar --save
```

#### 使用

```js
//main.js

//引入核心框架
import Vue from "vue";
//classList的垫片
import "classlist-polyfill";
//插件的包
import PerfectScrollbar from "perfect-scrollbar";
//对应的css
import "perfect-scrollbar/css/perfect-scrollbar.css";

/**
 * @description 自动判断该更新PerfectScrollbar还是创建它
 * @param {HTMLElement} el - 必填。dom元素
 */
const el_scrollBar = (el) => {
    //在元素上加点私货，名字随便取，确保不会和已有属性重复即可，我取名叫做_ps_
    if (el._ps_ instanceof PerfectScrollbar) {
        el._ps_.update();
    } else {
        //el上挂一份属性
        el._ps_ = new PerfectScrollbar(el, { suppressScrollX: true });
    }
};

//接着，自定义Vue指令,指令名你自己随便编一个，我们假定它叫scrollBar
Vue.directive("scrollBar", {
    //使用inserted钩子函数（初次创建dom）获取使用自定义指令处的dom
    inserted(el, binding, vnode) {
        //判断其样式是否存在position 并且position为"fixed", "absolute"或"relative"
        //如果不符合条件，抛个错误。当然你也可以抛个警告然顺便给其position自动加上"relative"
        //为什么要这么做呢，因为PerfectScrollbar实现原理就是对dom注入两个div，一个是x轴一个是y轴，他们两的position都是absolute。
        //对css稍有常识的人都知道，absolute是相对于所有父节点里设置了position属性的最近的一个节点来定位的，为了能够正确定位，我们要给其设置position属性
        const rules = ["fixed", "absolute", "relative"];
        if (!rules.includes(window.getComputedStyle(el, null).position)) {
            console.error(
                `perfect-scrollbar所在的容器的position属性必须是以下之一：${rules.join(
                    "、"
                )}`
            );
        }
        //el上挂一份属性
        el_scrollBar(el);
    },
    //更新dom的时候
    componentUpdated(el, binding, vnode, oldVnode) {
        try {
            //vnode.context其实就是vue实例，这里其实无需实例也直接用Vue的静态方法
            //故而也可以写成Vue.nextTick
            vnode.context.$nextTick(() => {
                el_scrollBar(el);
            });
        } catch (error) {
            console.error(error);
            el_scrollBar(el);
        }
    },
});
```

-   对于要添加优化滚动条的元素添加 v-scrollBar style="position:relative;"

```vue
//具体组件
<template>
    <div class="container">
        <ul class="list" v-scrollBar>
            <li>巴拉巴拉</li>
            <li>炫光舞法</li>
            <!--想想这里有一堆li-->
            <li>天舞台</li>
        </ul>
    </div>
</template>

<style lang="less" scoped>
.list {
    position: relative;
    /*不写高度说明高度自适应，既然高度都无限了根本就不会出现滚动条*/
    height: 300px;
}
</style>
```
