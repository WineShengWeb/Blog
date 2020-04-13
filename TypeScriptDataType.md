<!--
 * @Author: guoxinggang<guoxinggang@gsaxns.com>
 * @Version: 1.0
 * @Date: 2019-10-16 17:21:18
 * @LastEditTime: 2020-03-07 18:38:07
 * @Description: TypeScript数据类型
 -->
# TypeScript数据类型

Undefined :Undefined类型
Number:数值类型;
string : 字符串类型;
Boolean: 布尔类型；
enum：枚举类型；
any : 任意类型，一个牛X的类型；
void：空类型；
Array : 数组类型;
Tuple : 元祖类型；
Null ：空类型。

#### 一、Undefined类型

在js中当你定义了一个变量，但没有给他赋予任何值的时候，他就是Undefined类型。这可能和你以前学的语言稍有不同，其他语言会有个类型的默认值。

```
比如我们要声明一个年龄的变量age,我们要使用数值类型，也就是Number,但是我们不给他任何的值，我们只是在控制台给它输出，然后我们来看结果。

//声明数值类型的变量age，但不予赋值
var age:number
console.log(age) // undefined
```

#### 二、Number类型

在TypeScript中，所有的数字都是Number类型，这不分是整数还是小数。比如下面我们声明一个年龄是18岁，身高是178.5厘米。

```
var age:number = 18
var stature:number = 178.5
console.log(age)
console.log(stature)
```

在TypeScrip中有几种特殊的Number类型 我们需要额外注意一下：

- NaN：它是Not a Number 的简写，意思就是不是一个数值。如果一个计算结果或者函数的返回值本应该是数值，但是由于种种原因，他不是数字。出现这种状况不会报错，而是把它的结果看成了NaN。（这就好比我们去泰国外，找了一个大长腿、瓜子脸、水蛇腰的女神。房也开好了，澡也洗完了，发现跟我们的性别统一，我们只能吃个哑巴亏，你绝不会声张）
- Infinity :正无穷大。
- Infinity：负无穷大

#### 三、string类型

由单引号或者双引号括起来的一串字符就是字符串。如：'hello word!'

```
var a:string = "hello word!"
console.log(a) // hello word!
```

#### 四、boolean布尔类型

做任何业务逻辑判断都要有布尔类型的参与，通过对与错的判断是最直观的逻辑处理。boolean类型只有两种值，true和false。

```
var b:boolean = true
var c:boolean = false
```

#### 五、enum 类型

这个世界有很多值是多个并且是固定的，比如：

- 世界上人的类型：男人、女人、中性
- 一年的季节：春、夏、秋、冬 ，有四个结果。
这种变量的结果是固定的几个数据时，就是我们使用枚举类型的最好时机：

```
enum REN{ nan , nv ,yao}
console.log(REN.yao)  //返回了2，这是索引index，跟数组很想。

如果我们想给这些枚举赋值，可以直接使用=,来进行赋值。

enum REN{
    nan = '男',
    nv = '女',
    yao= '妖'
}
console.log(REN.yao)  //返回了妖 这个字
```

#### 六、any类型

TypeScript友好的为我们提供了一种特殊的类型any，比如我们在程序中不断变化着类型，又不想让程序报错，这时候就可以使用any了。

```
var t:any =10 
t = "jspang"
t = true
console.log(t)
```

#### 七、void空类型

void 表示空类型，void 类型只能赋值为 null || undefined。也可以在函数中表示没有返回值。

```
let v: void = null;

let func = (): void => {
    alert('没有返回值');
}
```

#### 八、Array数组类型

定义数组Array的定义方法： （1）类型[]  (2)Array<类型>，这种方式也角数组的泛型（3）用接口定义数组 (4) 使用元组定义，示例如下：

```
// 方式一
let arr: number[] = [1,2,3,4]  // [1,2,3,4]

// 方式二
let arr: Array<number> = [1,2,3,4]  // [1,2,3,4]

// 方式三
interface numArr{
    [index: number]: number
}
let arr: numArr = [1,2,3,4]  // [1,2,3,4]

// 方式四
let arr: [number,string,number] = [1,'2',3]  // [1,'2',3]
```

#### 九、Tuple元祖类型

元组用来表示已知元素数量与类型的数组，在赋值时内部元素的类型必须一一对应，访问时也会得到正确类型。当给元组添加元素或者访问未知索引元素的时候，会使用他们的联合类型。

```
let tuple: [string, number];
tuple = [1, 'a'];  // Error: 不能将类型“[number, string]”分配给类型“[string, number]”
tuple = ['a', 1];

tuple.push(true);  // 类型"true"的参数不能赋给类型“string | number”的参数。
```

#### 十、Null空类型

与 Undefined 类似，都代表空。Null 代表是引用类型为空。意义不大，但是有用。

非严格空检查模式下：以下三种情况都不会报错：
严格空检查模式下：以下三种情况都会报错：

```
let str: string = undefined;

let obj: object = undefined;

let num: number = 2;
num = null;
```
