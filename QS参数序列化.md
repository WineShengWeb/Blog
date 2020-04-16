### QS 参数序列化

##### 安装

```node
npm install qs
```

##### 引入

在 main.js 文件中引入，挂载到原型上

```JavaScript
import qs from 'qs';
Vue.prototype.qs = qs;
```

##### stringify() 和 parse() 方法

```JavaScript
let comments = {content: this.inputValue}

qs.stringify()  // 转换成查询字符串
let comValue = qs.stringify(comments)

qs.parse() // 转换成json对象
let comValue = qs.parse(comments)
```
