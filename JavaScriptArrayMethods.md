<!--
 * @Author: guoxinggang<guoxinggang@gsaxns.com>
 * @Version: 1.0
 * @Date: 2019-10-31 12:01:15
 * @LastEditTime: 2019-10-31 14:04:19
 * @Description: ArrayMethods
 -->
# JavaScript数组常用的方法

#### push

数组后面追加一个元素,返回添加后的数组的长度，改变原数组

```javascript
let arr = [1,2,3,4,5,6];
console,log(arr.push(7)); //7
console,log(arr); //1,2,3,4,5,6,7
```

#### pop

删除数组末尾的元素，返回删除的元素，改变原数组

```
let arr = [1,2,3,4,5,6];
console,log(arr.pop()); //6
console,log(arr); //1,2,3,4,5
```

#### shift

删除数组第一个元素，返回删除的元素，改变原数组

```
let arr = [1,2,3,4,5,6];
console,log(arr.shift()); //1
console,log(arr); //2,3,4,5,6
```

#### unshift

在数组开头添加一个元素，返回追加后的数组的长度，改变原数组

```
let arr = [1,2,3,4,5,6];
console,log(arr.shift(0)); //7
console,log(arr); //0,1,2,3,4,5,6
```

#### splice(开始位置， 删除的个数，元素)

```
//删除
let arr = [1,2,3,4,5,6];
arr.splice(0,2);  //[1,2]
console.log(arr); //[3,4,5,6]
//替换
let arr = [1,2,3,4,5,6];
arr.splice(0,0,'a','b');
console.log(arr); // ["a", "b", 1, 2, 3, 4, 5, 6]
```

#### join()

数组转为字符串，参数是以此参数作为分隔符，默认不传参是以逗号分隔不改变原数组

```
let arr = [1,2,3,4,5,6];
arr.join(); //"1,2,3,4,5,6"
console.log(arr); // [ 1, 2, 3, 4, 5, 6]
```

这里说下字符串转数组 split

```
let str = '123456';
str.split(''); //[1, 2, 3, 4, 5, 6]
```

#### sort()

对数组中的元素进行排序，改变原数组，默认按照第一个字符进行排序，而不是按照数字的大小进行排序，举个例子：

```
let arr = [1,22,88,9,10];
arr.sort(); //[1, 10, 22, 88, 9]
```

好吧，并不是我们想象的那样，那怎么来改下呢？这时候需要给sort()函数传参，传一个函数。

```
let arr = [1,22,88,9,10];
arr.sort(function(a,b){
    return a-b;
});  //[1, 9, 10, 22, 88]  a-b 代表从小到大的顺序排列

arr.sort(function(a,b){
    return b-a;
});  //[88, 22, 10, 9, 1]   a-b 代表从大到小的顺序排列
```

#### reverse()

数组的顺序进行反转

```
let arr = [1,22,88,9,10];
arr.reverse();  //[10, 9, 88, 22, 1]
```

#### concat()

连接两个数组，返回连接后的数组，不改变原数组

```
let arr = [1,2,3];
let arr2 = [4,5,6];
arr.concat(arr2);   //[1,2,3,4,5,6]
```

#### indexOf()和 lastIndexOf()

查找某个元素的索引值，若有重复的，则返回第一个查到的索引值若不存在，则返回 -1;lastIndexOf()相同，只不过是从数组的末尾开始查找。

```
let arr = [1,2,3,4,5,2]
let arr1 = arr.indexOf(2)
console.log(arr1)  // 1
let arr2 = arr.indexOf(9)
console.log(arr2)  // -1

let arr = [1,2,3,4,5,2]
let arr1 = arr.lastIndexOf(2)
console.log(arr1)  // 5
let arr2 = arr.lastIndexOf(9)
console.log(arr2)  // -1
```

#### Array.from()

将伪数组(类数组)转换成数组，前提是有length 属性

```
let oLi = document.querySelectorAll('li');
Array.from(oLi);
console.log(oLi); //[元素1，元素2，元素3]
```

#### Array.of()

方法是将一组值转变为数组，参数不分类型，只分数量，数量为0返回空数组

```
let arr1 = Array.of(1,2,3);	
let arr2 = Array.of([1,2,3]);
let arr3 = Array.of(undefined);
let arr4 = Array.of();
console.log(arr1); // [1, 2, 3]
console.log(arr2); // [[1, 2, 3]]
console.log(arr3); // [undefined]
console.log(arr4); // []
```

#### Array.forEach(function(item,index,arr){},thisArr)

- item: 必填，当前元素
- index: 可选，当前索引
- arr: 可选，当前元素所属的数组对象。
- thisArr : 数组指向,

遍历数组,没有return返回值,有时可以代替for。

```
let arr = [1,2,3,4,5,6];
arr.forEach(function(item,index){
    console.log(item);
});
```

#### Array.map()

指映射数组(遍历数组)，有返回值，方法返回一个新数组，数组中的元素为原始数组元素调用函数处理后的值

```
var arr = [1,2,3,4];
var arr2 = arr.map(function(item){
    return item*item;
});
console.log(arr2);  // [1, 4, 9, 16]
```

#### Array.filter()

过滤数组，返回新数组，return条件为true 的元素，false的元素过滤掉

```
let arr = [1,2,3,4,5]
let arr1 = arr.filter(function(item,index){
    return item > 1;
})
console.log(arr1); //[2, 3, 4, 5]
```

#### Array.reduce()和Array.reduceRight()

arr.reduce(function(total , cur , index , arr){ }, initialValue) 这两个方法都会迭代数组中的所有项，然后生成一个最终返回值。累加器，reduce从左往右，reduceRight从右往左。

- total 初始值，也是上一次回调函数返回的累加值，或者是提供的初始值。
- cur 数组中当前被处理的数组项。
- index 当前数组项在数组中的索引值。
- array 原数组。
- 默认第一次执行，total代表第一个参数，cur代表第二个参数。如果 initialValue 在调用 reduce() 时被提供，那么第一个 preValue 等于 initialValue ，并且curValue 等于数组中的第一个值；如果initialValue 未被提供，那么preValue 等于数组中的第一个值。

```
let arr = [0,1,2,3,4]
let arr1 = arr.reduce((total, cur) => 
    return total + cur;
)
console.log(arr1)    // 10
```

#### Array.every()

判断数组中每一项都是否满足条件，只有所有项都满足条件，才会返回true。

```
let arr = [1,2,3,4,5]
let arr1 = arr.every( (i, v) => i < 3)
console.log(arr1)    // false
let arr2 = arr.every( (i, v) => i < 10)
console.log(arr2)    // true
```

#### Array.some()

和every方法应该算是兄弟方法了。只要有一项满足条件，就返回true。

```
let arr = [1,2,3,4,5]
let arr1 = arr.some( (i, v) => i < 3)
console.log(arr1)    // true
```

#### find()

方法为数组中的每个元素都调用一次函数执行,返回通过测试（函数内判断）的数组的第一个元素的值。

```
let arr = [1,2,3,4,5,2,4]
let arr1 = arr.find((value, index, array) =>value > 2)
console.log(arr1)   // 3
```

#### findIndex()

```
let arr = [1,2,3,4,5]
let arr1 = arr.findIndex((value, index, array) => value = 1)
console.log(arr1)  // 0
```

#### Array.includes(seachVal,index)

方法用来判断一个数组是否包含一个指定的值，如果是返回 true，否则false。

- search 要查找的值
- index 表示从该下表下开始查找seachVal,如果为负值，则按升序从 array.length + fromIndex 的索引开始搜索。默认为 0。

```
let arr = [1,2,3,4,5]
let arr1 = arr.includes(2)  
console.log(arr1)   // ture
let arr2 = arr.includes(6) 
console.log(arr2)    // false
let arr3 = [1,2,3,NaN].includes(NaN)
console.log(arr3)  // true
let arr4 = ["a","b","c","d"];
let result = arr4.includes("b",-1);
console.log(result);  // false
let arr5 = ["a","b","c","d"];
let result1 = arr5.includes("b",-3);
console.log(result1);  // true
```



