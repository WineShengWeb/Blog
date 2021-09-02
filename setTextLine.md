# 设置文字多行显示和单行显示

#### 单行显示

```css
p {
    width:200px;
    overflow: hidden;
    text-overflow:ellipsis;
    white-space: nowrap;
}
```

#### 多行显示

```css
// 文字 2 行显示，
// 注：-webkit-line-clamp 属性即设置具体行数
p {
    overflow: hidden;
    text-overflow: ellipsis;
    display: -webkit-box;
    -webkit-box-orient: vertical;
    -webkit-line-clamp: 2;
}
```
