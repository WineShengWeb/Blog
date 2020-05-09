## element-china-area-data 省市区三级联动插件学习

[element-china-area-data 官网](https://www.npmjs.com/package/element-china-area-data)

#### 安装

```node
npm install element-china-area-data -S
```

#### 引入

```
import { provinceAndCityData, regionData, provinceAndCityDataPlus, regionDataPlus, CodeToText, TextToCode } from 'element-china-area-data'
```

-   1、provinceAndCityData 是省市二级联动数据（不带“全部”选项）
-   2、regionData 是省市区三级联动数据（不带“全部”选项）
-   3、provinceAndCityDataPlus 是省市区三级联动数据（带“全部”选项）
-   4、regionDataPlus 是省市区三级联动数据（带“全部”选项）
-   5、"全部"选项绑定的 value 是空字符串""
-   6、CodeToText 是个大对象，属性是区域码，属性值是汉字 用法例如：CodeToText['110000']输出北京市
-   7、TextToCode 是个大对象，属性是汉字，属性值是区域码 用法例如：TextToCode['北京市'].code 输出 110000,TextToCode['北京市']['市辖区'].code 输出 110100,TextToCode['北京市']['市辖区']['朝阳区'].code 输出 110105

#### 使用

```vue
<template>
    <div id="app">
        <el-cascader
            v-model="cascader"
            :options="options"
            @change="handleChange"
        ></el-cascader>
    </div>
</template>

<script>
import { regionData, CodeToText } from "element-china-area-data";
export default {
    data() {
        return {
            options: regionData,
        };
    },

    methods: {
        handleChange(arr) {
            if (CodeToText[arr[1]] === undefined) {
                this.createCustomer.address = CodeToText[arr[0]];
            } else if (CodeToText[arr[2]] === undefined) {
                this.createCustomer.address =
                    CodeToText[arr[0]] + CodeToText[arr[1]];
            } else {
                this.createCustomer.address =
                    CodeToText[arr[0]] +
                    CodeToText[arr[1]] +
                    CodeToText[arr[2]];
            }
        },
    },
};
</script>
```
