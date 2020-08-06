<!--
 * @Author: guoxinggang<guoxinggang@gsaxns.com>
 * @Version: 1.0
 * @Date: 2019-10-31 08:51:18
 * @LastEditTime: 2019-10-31 09:43:42
 * @Description: dataType
 -->

# JavaScript 的数据类型

JavaScript 数据类型：Number、String、Boolean、Null、undefined、object、symbol、bigInt。

在 ES5 的时候，我们认知的数据类型确实是 6 种：Number、String、Boolean、undefined、object、Null。

ES6 中新增了一种 Symbol 。这种类型的对象永不相等，即始创建的时候传入相同的值，可以解决属性名冲突的问题，做为标记。

谷歌 67 版本中还出现了一种 bigInt。是指安全存储、操作大整数。（但是很多人不把这个做为一个类型）。

-   JS 数据类型：JS 的数据类型有几种？

    8 种。Number、String、Boolean、Null、undefined、object、symbol、bigInt。

-   JS 数据类型：Object 中包含了哪几种类型？

        其中包含了Data、function、Array等。这三种是常规用的。

-   JS 数据类型：JS 的基本类型和引用类型有哪些呢？

    基本类型（单类型）：除 Object。 String、Number、boolean、null、undefined。

    引用类型：object。里面包含的 function、Array、Date。

-   JS 数据类型：JS 中 typeof 输出分别是什么？

    { } 、[ ] 输出 object。

    console.log( ) 输出 function。

-   JS 数据类型：如何判断数据类型？

    1､typeof 操作符（通用：上面有内容有讲到）

    2､toString ( )

    作用：其他类型转成 string 的方法

    支持：number、boolean、string、object

    不支持：null 、undefined

    ```js
    let a = true;
    a.toString(); // "true"
    let b = 45;
    b.toString(); // "45"
    ```

    3､toLocaleString ( )

    把数组转成本地字符串

    ```js
    let arr = ["1", "2", "3"];
    arr.toLocaleString(); // "1,2,3"
    ```

    4､检测数组类型的方法

    ① instanceof 操作符

    ```js
    let arr = ["1", "2", "3"];
    console.log(arr instanceof Array); // true

    let test = "1";
    console.log(test instanceof Array); // false
    ```

    ② 对象的 constructor 属性

    ```js
    let arr = ["1", "2", "3"];
    console.log(arr.constructor === Array); // true

    let arr1 = 123;
    console.log(arr1.constructor === Array); // false
    ```

    ③ Array.isArray( ) 检验值是否为数组

    ```js
    let arr = ["1", "2", "3"];
    console.log(Array.isArray(arr)); // true

    let arr1 = 123;
    console.log(Array.isArray(arr1)); // false
    ```

#### 一、基本数据类型

##### 1、Number 类型

数字类型，表示数据的整数和浮点数。某些语言中也称为“双精度值”。

```js
// 数值类型
var a = 34.0;
var b = 34;
var c = 123e5; // 12300000
var d = 123e-5; // 0.00123
```

###### NaN

-   注意一点：NaN 是 Number 中的一种，非 Number 。
-   用 isNaN（） 检测是否是非数值型。

```js
// NaN是not a number的缩写，表示不是一个数字
var x = Number("abcd"); //结果是NaN
alert(typeof x); //结果是number

// 特点：
// （1）NaN 在布尔值里是 false
var x = Number("abcd");
if (x) {
    alert("真");
} else {
    alert("假"); //结果是假
}

// （2）NaN自己和自己不相等，其他的数据类型自己和自己相等
var x = Number("abcd");
alert(x === x); // false
```

##### 2、String 类型

字符串可以有单引号、双引号表示。字符串是不可变的，一旦创建，值就不能改变

要改变某个变量保存的字符串，首先要销毁原来的字符串，然后于用另一个包含的字符串填充该变量。

注）toString()可以输出二进制、八进制、十进制，十六进制。

null 和 undefined 没有 toString()方法，用 String 函数不返回这两个值的字面量。

```js
// 字符串类型
var carName = "Porsche 911"; // 使用双引号
var carName = "Porsche 911"; // 使用单引号
var answer = "It's alright"; // 双引号内的单引号
var answer = "He is called 'Bill'"; // 双引号内的单引号
var answer = 'He is called "Bill"'; // 单引号内的双引号
```

##### 3、Boolean 类型

使用最多的一个类型，有两个字面值，分别是 true、false。true 不一定等于 1,false 不一定等于 0。

boolean 类型的字面值是区分大小写的。True 和 False 是标识符

```js
// 布尔值只有两个值：true 或 false。
var x = true;
var y = false;
```

##### 4、Undefined 类型

###### 出现 undefined 的情景

-   此类型需要注意，当一个变量只声明，未定义时值为 Undefined，类型为 Undefined！

```js
var name;
console.log(name); // undefined
```

-   访问对象上不存在的属性

```js
var obj = {};
console.log(obj.age); // undefined
```

-   函数定义了形参，但调用时未传实参

```js
// 这种写法是函数的自调用,和fa ()效果一样
(function fa(a) {
    console.log(a);
})();
```

###### 总结：undefined 出现多是数据原始状态的保留结果，造化钟神秀的感觉，天然雕饰

##### 5、Null 类型

###### Null 出现的场景

-   意志形态，是将要发生的事
-   简单来说，你定义了一个变量，打算保存接下来用到的某个对象，初始化时候建议赋值 null
-   类似情况就是一个对象在两个函数内部都要使用，但函数自身就是一个作用域，对外界封闭
-   此时就需要将该对象提成全局变量，初始化赋值为 null

-   只有一个值。null 是表示一个空对象指针，这也是 typeof 操作符检测 null 值时会返回 object 的原因。

-   JS 数据类型：null 不存在的原因是什么？如何解决？

    不存在的原因是：

        1､方法不存在

        2､对象不存在

        3､字符串变量不存在

        4､接口类型对象没初始化

    解决方法：

        做判断处理的时候，放在设定值的最前面

```js
var person = null; // 值是 null，但是类型仍然是对象
```

##### Undefined 与 Null 的区别

Null 只有一个值，是 null。不存在的对象。

Undefined 只有一个值，是 undefined。没有初始化。undefined 是从 null 中派生出来的。

简单理解就是：undefined 是没有定义的，null 是定义了但是为空。

```js
// Undefined 与 null 的值相等，但类型不相等
typeof undefined; // undefined

typeof null; // object

null === undefined; // false

null == undefined; // true
```

-   JS 数据类型：== 和 === 有什么区别，什么场景下使用？

    == 表示相同。

        比较的是物理地址，相当于比较两个对象的 hashCode ，肯定不相等的。

        类型不同，值也可能相等。

    === 表示严格相同。

        例：同为 null／undefined ，相等。

    简单理解就是 == 就是先比较数据类型是否一样。=== 类型不同直接就是 false。

#### 6、Object 类型

ECMAjavascript 中的对象其实就是一组数据和功能的集合。对象可以通过执行 new 操作符后跟要创建的对象类型的名称来创建。创建 object 类型的实例并为其添加属性（或）方法，就可以自定义创建对象。

如：var o = new Object( );

object 的每个实例都有下列属性和方法：

constructor：保存着用于创建当前对象的函数。（构造函数)constructor 就是 object();

hasOwnProperty(propertyName):用于检查给定的当前属性在当前对象实例中）而不是在实例原型中）是否存在。其中，作为参数的属性名（propertyName)必须以字稚串形式指定（例如：o.hasOwnProperty(“name”))。

isPrototypeOf(object):用于检查传入的对象是否是传入对象原型。

propertyIsEnumerable(propertyName):用于检查给定属性是否能够用 for-in 语句。与 hasOwnProperty（）方法一样，作为参数的属性名必须以字符串形式指定。

toLocaleString( ):返回对象的字符串表示，该字符串与执行环境的地区对应。

toString( ):返回对象的字符串表示。

valueOf( ):返回对象的字符串、数值或者布尔值表示。通常与 toString( )方法的返回值得相同。

ECMAJS 中 object 是所有对象的基础，因些所有对象都具有这些基本的属性和方法。

-   JS 数据类型：对象可以比较吗？

    对象是可以比较，遍历比较 key 和 value 就行， Object.is(value1, value2)。

#### 7、Symbol（ES6）类型

Symbol 这种数据类型提供一个独一无二的值;

Symbol 类型的对象永远不相等，即便创建的时候传入相同的值。因此，可以用解决属性名冲突的问题（适用于多少编码），做为标记。

这是 es6 新增的数据类型。

```js
var s = Symbol("a");
console.log(s); //Symbol()
console.log(typeof s); //symbol

var s2 = Symbol("b");
console.log(s2); //Symbol()
console.log(s === s2); //false Symbol 中代表独一无二的值 避免键名重复

//var s3 = new Symbol(); 不可以用new
var obj = {
    a: 1,
};
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
```

#### 8、BigInt 类型

Javascript 中的任意精度整数，可以安全存储和操作大整数。即始超出 Number 能够表示的安全整数范围。是 chrome 67 中的新功能。

#### 二、引用数据类型

##### 1、Array 类型

```js
// 数组类型
var cars = ["Porsche", "Volvo", "BMW"];
```

##### 2、Object 类型

```js
// 对象类型
var person = {
    firstName: "Bill",
    lastName: "Gates",
    age: 62,
    eyeColor: "blue",
};
```

##### 3、Function 类型

```js
// 函数类型
typeof function myFunc() {}; // 返回 "function"
```
