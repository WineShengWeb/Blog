
# 文字显示设置

### 文字按指定行显示
```css
.css {
    // 文字3行显示 start
    overflow: hidden;
    text-overflow: ellipsis;
    display: -webkit-box;
    /* autoprefixer: off */
    -webkit-box-orient: vertical;
    /* autoprefixer: on */
    -webkit-line-clamp: 3;
    // 文字3行显示 end
}
```

### 文字单行显示

```css
.css {
    width: 100px;
    overflow: hidden;
    text-overflow: ellipsis;
    white-space: nowrap;
}
```

### 文字分散对齐

```css
.css {
    width: 80px;
    text-align-last: justify;
    text-align: justify;
    text-justify: distribute-all-lines; // 这行必加，兼容ie浏览器
}
```

### 文字禁止选中

```css
.css {
    // 文字禁止复制 / 选中 start
    -moz-user-select: none; /*火狐*/
    -webkit-user-select: none; /*webkit浏览器*/
    -ms-user-select: none; /*IE10*/
    -khtml-user-select: none; /*早期浏览器*/
    user-select: none; /*open浏览器*/
    // 文字禁止复制 / 选中 end
}
```