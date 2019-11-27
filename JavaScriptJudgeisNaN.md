<!--
 * @Author: guoxinggang<guoxinggang@gsaxns.com>
 * @Version: 1.0
 * @Date: 2019-10-31 09:44:39
 * @LastEditTime: 2019-10-31 09:51:27
 * @Description: isNaN()
 -->
# JavaScript中isNaN的判断方法

#### 1、window.isNaN()

```

(1)  window.isNaN(NaN)  // true
(2)  window.isNaN(123)   // false

注意: window.isNaN 只对数值有效，如果传入其他值，会被先转成数值。比如，传入字符串的时候，字符串会被先转成NaN，所以最后返回true，这一点要特别引起注意。也就是说，isNaN为true的值，有可能不是NaN，而是一个字符串。(不是数值会先调用 Number 方法转化为数值)

window.isNaN('Hello')    // true
//相当于
window.isNaN(Number('Hello'))   // true
```

#### 2、先判断是不是数字,然后再使用 window.isNaN()

```
function  judgeNaN (value) {
         return (typeof value) === 'number' && window.isNaN(value);
}

judgeNaN(1)          //false
judgeNaN(NaN)          //true
judgeNaN("我是字符串")          //false
judgeNaN([])          //false
judgeNaN({})          //false
```

#### 3、Number.isNaN(value) ( 1. 首先判断 value 类型是不是 number; 2. 然后判断 value 是不是 NaN)

```
Number.isNaN(NaN);                      // true
Number.isNaN(Number.NaN);          // true
Number.isNaN(0/0);                          // true

// 下面这些使用 window.isNaN() 将会返回 true ,Number.isNaN() 返回 false,
// 因为 window.isNaN 会先把参数转化为数字类型,再判断是不是 NaN; 而 Number.isNaN 会先判断参数是不是数字类型,不是就返回 false, 是数字类型再进入判断是不是 NaN.
Number.isNaN('NaN');                        // false
Number.isNaN(undefined);                  // false
Number.isNaN({});                                // false
Number.isNaN('blabla');                       // false

// 下面这些 window.isNaN() 和 Number.isNaN() 都返回 false
Number.isNaN(true);
Number.isNaN(null);
Number.isNaN(37);
Number.isNaN('37');
Number.isNaN('37.37');
Number.isNaN('');
Number.isNaN(' ')
```

#### 4、不支持 Number.isNaN() 的老浏览器解决办法

```
方法1 :
Number.isNaN = Number.isNaN || function(value {
            return  (typeof value) === 'number' && window. isNaN(value);
}

方法2 :
Number.isNaN = Number.isNaN || function(value) {
            return  value !== value;
}
```

#### 5、利用 NaN 是 JavaScript 之中唯一不等于自身的值 (最简单的办法)

```
function judgeNaN (value) {
         return value !== value;
}

judgeNaN(1)                                //false
judgeNaN(NaN)                          //true
judgeNaN( "我是字符串" )          //false
judgeNaN([])                               //false
judgeNaN({})                              //false
```

#### 6、补充知识: Object.is() 是 ES6 用来比较两个值是否严格相等，与严格比较运算符（===）的行为基本一致。除了对 +0 和 -0 以及 NaN 的判断

```
NaN === NaN                        //false
Object.is(NaN, NaN)              //true

+0 === -0                                //true
Object.is(+0, -0)                      //false
```
