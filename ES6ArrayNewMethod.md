<!--
 * @Author: guoxinggang<guoxinggang@gsaxns.com>
 * @Version: 1.0
 * @Date: 2019-10-16 14:25:25
 * @LastEditTime: 2019-10-16 15:43:37
 * @Description: es6
 -->
# ES6数组新增的方法

#### 一、forEach()

forEach() 遍历数组，无返回值，不改变原数组，仅仅只是遍历、常用于注册组件、指令等等。
参数：
- 1. item：必需参数，当前元素。
- 2. index: 可选，当前元素的索引。
- 3. arr：可选，当前元素所属的数组对象。
```
// test1
var arr = [1,2,3,4];
arr.forEach((item,index,arr) => {
    console.log(item) //结果为1,2,3,4
})

// test2
var arr1=["red","blue","yellow","green"];
arr1.forEach(function(color){
    console.log(color);//"red","blue","yellow","green"
})
```

#### 二、map()

map() 遍历数组，返回一个新数组，不改变原数组的值。
参数：
- 1. item：必需参数，当前元素。
- 2. index: 可选，当前元素的索引。
- 3. arr：可选，当前元素所属的数组对象。

注意：
- 1. map() 不会对空数组进行检测。
- 2. map() 不会改变原始数组。

```
// test1
var arr = [1,2,3,4];
arr.map((item,index,arr) => {
    return item*10 //新数组为10,20,30,40
})

// test2 
// 有一个数值数组(A),将A数组中的值以双倍的形式放到B数组
var arr2=[1,2,3,4];
var doub=arr2.map(function(num){
    return num*2;
})
console.log(doub);//2,4,6,8

// test4
// 有一个对象数组(A),将A数组中对象某个属性的值存储到B数组中
var cars=[
    {model:'Buick',price:'cheap'},
    {model:'BMW',price:'expensive'}
]
var cas=cars.map(function(cass){
    return cass.price=="cheap";
})
console.log(cas);//{true,false}
```

#### 三、filter()

filter() 过滤掉数组中不满足条件的值，返回一个新数组，不改变原数组的值。
参数：
- 1. item：必需参数，当前元素。
- 2. index: 可选，当前元素的索引。
- 3. arr：可选，当前元素所属的数组对象。

注意：
- 1. filter() 不会对空数组进行检测。
- 2. filter() 不会改变原始数组。
```
// test1
var arr = [1,2,3,4];
arr.filter((item,index,arr) => {
    return item > 2 //新数组为[3,4]
})

// test2
// 有一个数组A,获取数组中指定类型的对象放到B数组中
var products=[
        {name:'cucumber',type:'vegetable'},
        {name:'banana',type:'fruit'},
        {name:'celery',type:'vegetable'},
        {name:'orange',type:'fruit'}
    ];
var filt=products.filter(function(pro){
    return pro.type=="fruit";
})
console.log(filt);//{name:'banana',type:'fruit'},{name:'orange',type:'fruit'}

// test3
// 有一个对象数组A,过滤掉不满足以下条件的对象  蔬菜  数量大于0,价格小于10
var products1=[
    {name:'cucumber',type:'vegetable',quantity:10,price:6},
    {name:'banana',type:'fruit',quantity:16,price:16},
    {name:'celery',type:'vegetable',quantity:30,price:36},
    {name:'orange',type:'fruit',quantity:6,price:6}
]
var pord=products1.filter(function(pro){
    return (pro.type=="vegetable")&&(pro.price>0&&pro.price<10)
})
console.log(pord);//{name:'cucumber',type:'vegetable',quantity:10,price:6}
```

#### 四、find()

find()方法返回通过测试（函数内判断）的数组的第一个元素的值。

- 当数组中的元素在测试条件时返回 true 时, find() 返回符合条件的元素，之后的值不会再调用执行函数。
- 如果没有符合条件的元素返回 undefined。

参数：
- 1. item：必需参数，当前元素。
- 2. index: 可选，当前元素的索引。
- 3. arr：可选，当前元素所属的数组对象。

注意: 
- 1. find() 对于空数组，函数是不会执行的。
- 2. find() 并没有改变数组的原始值。

```
// test1
// 有一个对象数组,找到符合条件的对象
var users=[
    {name:'Jill'},
    {name:'Alex',id:2},
    {name:'Bill'},
    {name:'Alex'}
    ]
var user=users.find(function(names){
    return names.name=="Alex";
})
console.log(user);//{name:'Alex',id:2}

//test2
// 有一个对象数组A,根据指定对象的条件找到数组中符合条件的对象
var posts=[
    {id:3,title:"Node.js"},
    {id:2,title:"React.js"}
]
var comment={postid:2,content:'Hello'};
comment=posts.find(function(pos){
    return pos.id==comment.postid;
})
console.log(comment);//{id:2,title:"React.js"}
```

#### 五、reduce()

reduce() 让数组的前后两项进行某种计算。然后返回其值，并继续计算。不改变原数组，返回计算的最终结果，从数组的第二项开始遍历。

参数：
- 1. total：必需。初始值, 或者计算结束后的返回值。
- 2. item：必需参数，当前元素。
- 3. index: 可选，当前元素的索引。
- 4. arr：可选，当前元素所属的数组对象。

注意: 
- reduce() 对于空数组是不会执行回调函数的。
```
var arr = [1,2,3,4];
arr.reduce((result,item,index,arr) => {
    console.log(result) // 1  3  6  result为上次一计算的结果
    console.log(item)  // 2  3  4
    console.log(index) // 1  2  3
    return result+item //最终结果为10
})
```

#### 六、some()

some() 遍历数组每一项，只要有一项满足条件就返回true,则停止遍历，结果返回true。不改变原数组。
- some：有一个真则为真。
- 如果有一个元素满足条件，则表达式返回true , 剩余的元素不会再执行检测。
- 如果没有满足条件的元素，则返回false。

参数：
- 1. item：必需参数，当前元素。
- 2. index: 可选，当前元素的索引。
- 3. arr：可选，当前元素所属的数组对象。

注意： 
- 1. some() 不会对空数组进行检测。
- 2. some() 不会改变原始数组。
```
var arr = [1,2,3,4];
arr.some((item,index,arr) => {
    return item > 3 //结果为true
})
```

#### 七、every()

every() 遍历数组每一项，每一项返回true,则最终结果为true。当任何一项返回false时，停止遍历，返回false。不改变原数组。

- Every：条件都为真才为真,有一假则为假。
- 如果数组中检测到有一个元素不满足，则整个表达式返回 false ，且剩余的元素不会再进行检测。
- 如果所有元素都满足条件，则返回 true。

参数：
- 1. item：必需参数，当前元素。
- 2. index: 可选，当前元素的索引。
- 3. arr：可选，当前元素所属的数组对象。

注意：
- 1. every() 不会对空数组进行检测。
- 2. every() 不会改变原始数组。
```
var arr = [1,2,3,4];
arr.every((item,index,arr) => {
    return item > 1 //结果为false
})
```

以上7个方法均为ES6语法，IE9及以上才支持。不过可以通过babel转意支持IE低版本。
以上均不改变原数组。
some、every返回true、false。
map、filter返回一个新数组。
reduce让数组的前后两项进行某种计算，返回最终操作的结果。
forEach 无返回值。
