# vuetify 栅格布局

Vuetify 附带了一个使用 flex-box 构建的 12 点栅格系统 相当于将页面宽度平均分成了 12 等分 可以独立设置每个元素在页面的的宽度 在栅格系统的最外层是<v-container>标签 该标签能使里面的内容居中水平填充在页面上展示

-   在<v-container>标签上添加 fluid 可使其有更小的左右边距

用<v-row>标签包裹每一行的内容

-   使用 justify 属性设置对齐方式 该属性即为即 css 的 justify-content 属性 属性值也是一样的 例如 justify="space-between"
    用<v-col>标签包裹每一行中的每一块 里面放入内容 在<v-col>标签上 可以设置在不同大小的屏幕上 该块内容的所占比：

-   用 cols 属性设置设置组件扩展的默认列数 即 xs 屏幕大小下的该块内容所占大小 可选值有 1-12 和 auto

-   用 sm md lg xl 这四个属性设置当处于该屏幕大小时 该块内容所占大小

```
xs: 小于 600px；
sm: 大于 600px，小于 960px；
md: 大于 960px，小于 1264px；
lg: 大于 1264px，小于 1904px；
xl: 大于 1904px；
```

案例： 由于默认是将屏幕横向分成 12 块 因此 在下面的案例中： 当屏幕处于 md 大小时 第一个按钮占一半 二三四按钮加起来占半行 当屏幕处于 sm 大小时 第一个按钮占一整行 二三四按钮加起来占一行 如此 即可实现在不同屏幕大小下不同的页面布局

```vue
<template>
    <v-container fluid>
        <v-row>
            <v-col
                cols="12"
                xs="12"
                sm="6"
                md="4"
                lg="3"
                v-for="item in list"
                :key="item.id"
            >
                <v-hover v-slot:default="{ hover }">
                    <v-card
                        :color="item.color"
                        :elevation="hover ? 16 : 2"
                        class="card"
                    >
                        <div class="title">{{ item.title }}</div>
                    </v-card>
                </v-hover>
            </v-col>
        </v-row>
    </v-container>
</template>
```
