# 快速清空 vue 对象属性值

#### 第一种

```js
// 清空data中的form对象的属性值
data(){
  return {
    form: {
      a: 1,
      b: 2,
      c: 3
    }
  }
}

Object.keys(form).forEach((key) => (form[key] = ""));
```

#### 第二种

```js
data(){
  return {
    form: {
      name: "",
      username:"",
    }
  }
}

this.form = this.$options.data().form
```
