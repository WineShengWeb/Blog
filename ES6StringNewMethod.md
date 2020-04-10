<!--
 * @Author: guoxinggang<guoxinggang@gsaxns.com>
 * @Version: 1.0
 * @Date: 2019-10-16 15:47:18
 * @LastEditTime: 2019-10-31 15:59:41
 * @Description: ES6
 -->
# ES6字符串新增的方法

#### 1、查找：str.includes( val )

```JavaScript
// 查找 red
let str = "red blue yellow";
 
// 以前都是用 str.indexOf( val )  返回的是索引（位置）,没找到返回 -1
if(str.indexOf("red")!= -1){
    alert(true)
}else{
    alert(false)
}
 
ES2016新增 str.includes( val )    返回的是 true/false
alert(str.includes("red"))     // 弹出 true
```

#### 2、以xx开头结尾:str.startsWith( val )、str.endsWith( val )

```JavaScript
let str = "https://blog.csdn.net/qq_41772754/article/details/88086475";

// 判断是否是以“https” 开头，多用于及检测地址
str.startsWith("https")  // 返回true

// 判断是否是以“6475” 结尾，多用于判断文件的格式
str.endsWith("6475")  // 返回true
```

#### 3、重复字符串：str.repeat( num )

```JavaScript
let str = "abc"
let str2 = str.repeat(3); // 重复3次
console.log(str2)   // abcabcabc
```

#### 4、字符串填充：str.padStart( num , val)、str.padEnd( num , val )

```JavaScript
前面填充：str.padStart( num , val) 
后面填充：str.padEnd( num , val )
    num:表示填充完后整个字符串的长度(原字符串的长度+要填充的字符串的长度)
    val:表示要填充的字符串
 
let str = "123456789";
let str2 = "abc"
str.padStart( str.length + str2.length, val)  //  abc123456789
--------------------------
str.padEnd( str.length + str2.length, val )   //  123456789abc
```
