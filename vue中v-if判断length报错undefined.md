# vue 中 v-if 判断 length 报错 undefined

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
