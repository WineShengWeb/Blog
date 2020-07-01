# vue 公共复用组件的简单封装

-   1、组件

```vue
<template>
    <div>
        // 子组件
        <div class="sub-pay">
            <div class="pay-left">
                <div class="total"><span>￥</span>{{ payAmt }}</div>
                <div class="pay-amount">实付金额</div>
            </div>
            <div class="pay-right" @click="onPayBtn">
                {{ btnname }}
            </div>
            <slot></slot> //插槽
        </div>
    </div>
</template>

<script>
//子组件
export default {
    props: {
        payAmt: {
            type: String,
            required: true,
        },
        btnname: {
            type: String,
            required: true,
        },
    },
    data() {
        return {};
    },
    methods: {
        onPayBtn() {
            //自定义事件
            this.$emit("clickBtn", true);
        },
    },
};
</script>

<style scoped lang="scss"></style>
```

-   2、使用

```vue
<template>
    <div>
        //父组件使用
        <subpay btnname="立即支付" :payAmt="form.payAmt" @clickBtn="onPay">
            //特殊情况下需要在子组件加内容 因在子组件已经加入slot
            所以可以在子组件中加入内容
            <div class="pay-detail">
                <p>明细</p>
                <img src="/static/imgs/ico-up-arrow.png" alt="" />
            </div>
        </subpay>
    </div>
</template>

<script>
export default {
    data() {
        return {};
    },
};
</script>

<style scoped lang="scss"></style>
```

-   3、如果在父组件中想更改 子组件的样式 需要 使用深度作用选择器 用到 /deep/ 下面是使用方法
    因为直接.sub-pay .pay-right{} 解析不到类名

```css
.sub-pay/deep/.pay-right {
    background: #4d6aff !important;
}
```
