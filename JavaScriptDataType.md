<!--
 * @Author: guoxinggang<guoxinggang@gsaxns.com>
 * @Version: 1.0
 * @Date: 2019-10-31 08:51:18
 * @LastEditTime: 2019-10-31 09:43:42
 * @Description: dataType
 -->
# JavaScript的数据类型

#### 一、基本数据类型

##### 1、Number类型

```
// 数值类型
var a = 34.00;
var b = 34;
var c = 123e5; // 12300000
var d = 123e-5; // 0.00123
```

##### 2、String类型

```
// 字符串类型
var carName = "Porsche 911";   // 使用双引号
var carName = 'Porsche 911';   // 使用单引号
var answer = "It's alright";             // 双引号内的单引号
var answer = "He is called 'Bill'";    // 双引号内的单引号
var answer = 'He is called "Bill"';    // 单引号内的双引号
```

##### 3、Boolean类型

```
// 布尔值只有两个值：true 或 false。
var x = true;
var y = false;
```

##### 4、NaN类型

```
// NaN是not a number的缩写，表示不是一个数字
var x = Number('abcd');   //结果是NaN
alert( typeof (x) );     //结果是number

特点：
（1）NaN 在布尔值里是 false
var x = Number('abcd');
if( x ){
     alert( '真' );
}else{
    alert( '假' );   //结果是假
}

（2）NaN自己和自己不相等，其他的数据类型自己和自己相等
var x = Number('abcd');
alert( x === x );    // false
```

##### 5、Undefined类型

###### 出现undefined的情景

- 此类型需要注意，当一个变量只声明，未定义时值为Undefined，类型为Undefined！

```
var name;
console.log(name); // undefined
```

- 访问对象上不存在的属性

```
var obj={};
console.log(obj.age); // undefined
```

- 函数定义了形参，但调用时未传实参

```
// 这种写法是函数的自调用,和fa ()效果一样
(function fa(a){
   console.log(a);
}())
```

###### 总结：undefined出现多是数据原始状态的保留结果，造化钟神秀的感觉，天然雕饰

##### 6、Null类型

###### Null出现的场景

- 意志形态，是将要发生的事
- 简单来说，你定义了一个变量，打算保存接下来用到的某个对象，初始化时候建议赋值null
- 类似情况就是一个对象在两个函数内部都要使用，但函数自身就是一个作用域，对外界封闭
- 此时就需要将该对象提成全局变量，初始化赋值为null

```
var person = null;           // 值是 null，但是类型仍然是对象
```

##### Undefined 与 Null 的区别

```
// Undefined 与 null 的值相等，但类型不相等
typeof undefined              // undefined
typeof null                   // object
null === undefined            // false
null == undefined             // true
```

##### 8、Symbol（ES6）类型

Symbol这种数据类型提供一个独一无二的值;

```
var s = Symbol("a");
console.log(s); //Symbol()
console.log(typeof s); //symbol

var s2 = Symbol("b");
console.log(s2); //Symbol()
console.log(s === s2); //false Symbol 中代表独一无二的值 避免键名重复

//var s3 = new Symbol(); 不可以用new
var obj = {
    a:1
}
obj.b = 2;
obj.a = 3;
console.log(obj); //Object {a: 3, b: 2}
var a = Symbol("b");
obj[a] = "sa";
console.log(obj); //Object {a: 3, b: 2, Symbol(b): "sa"}
console.log(obj[a]); //sa

var b = Symbol("b");
obj[b] = "sb";
console.log(obj); //Object {a: 3, b: 2, Symbol(b): "sa", Symbol(b): "sb"}
console.log(obj[b]); //sb

// for( var attr in obj){
//     console.log(attr)//a,b
// }
console.log(Object.getOwnPropertySymbols(obj)); //[Symbol(b), Symbol(b)]
//symbol 不可以加减乘除
console.log(Boolean(b)); //true
````

#### 二、引用数据类型

##### 1、Array类型

```
// 数组类型
var cars = ["Porsche", "Volvo", "BMW"];
```

##### 2、Object类型

```
// 对象类型
var person = {firstName:"Bill", lastName:"Gates", age:62, eyeColor:"blue"};
```

##### 3、Function类型

```
// 函数类型
typeof function myFunc(){}   // 返回 "function"
```
