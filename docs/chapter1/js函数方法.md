### forEach()

forEach方法中的function回调有三个参数：
第一个参数是遍历的数组内容，
第二个参数是对应的数组索引，
第三个参数是数组本身

```js
var arr = [1,2,3,4];
var sum =0;
arr.forEach(function(value,index,array){

 array[index] == value; //结果为true

 sum+=value; 

 });

console.log(sum); //结果为 10

// 对象
var a = {
  name: 'zs',
  sex: '男'
}

var b = Object.keys(a)
b.forEach(element => {
  console.log(element)
  console.log(a[element])
});
// 输出：name zs sex 男
```

### Object.keys()

*Object.keys()* 方法会返回一个由一个给定对象的自身可[枚举](https://so.csdn.net/so/search?q=枚举&spm=1001.2101.3001.7020)属性组成的数组,数组中属性名的排列顺序和使用 for...in 循环遍历该对象时返回的顺序一致 。

 传入对象， 返回 对象key值所组成的数组

```js
var obj = {'name': 'xiaoming', 'age': 18};
console.log(Object.keys(obj)); // ["name","age"]
```

传入字符串，返回索引值

```js
var str = "Beijing"; 
console.log(Object.keys(str));
// ["0", "1", "2", "3", "4", "5", "6"]
```

传入数组，返回索引值

```js
var arr = ["a", "b", "c"];
console.log(Object.keys(arr));
//["0", "1", "2"]
```

构造函数，返回空数组或者属性名

```js
function Demo(name, age) {
  this.name = name;
  this.age = age;
}
console.log(Object.keys(Demo));
// []
```

### Array.filter()

filter用于对数组进行过滤。

filter() 方法创建一个新的数组，新数组中的元素是通过检查指定数组中符合条件的所有元素。

==注意==：filter() 不会对空数组进行检测；不会改变原始数组

```js
array.filter(function(currentValue,index,arr), thisValue)
```

currentValue:必选，当前元素的值

index：可选，当前元素的索引值

arr：可选，当前元素的数组对象

thisValue：可选，对象作为该执行回调时使用，传递给函数，用作‘this’的值。如果省略的thisValue，this的值为undefined

返回值：返回==数组==，包含了符合条件的所有元素。如果没有符合条件的元素则返回空数组。



实例1. 返回数组nums中所有大于5的元素

```js
let nums = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];
 
let res = nums.filter((num) => {
  return num > 5;
});
 
console.log(res);  // [6, 7, 8, 9, 10]
```

实例2.把一个Array中的空字符串删掉

```js
var arr = ['A', '', 'B', null, undefined, 'C', '  '];
var r = arr.filter(function (s) {
    return s && s.trim(); // 注意：IE9以下的版本没有trim()方法
});
r; // ['A', 'B', 'C']
```

实例3. 利用 filter 进行数组去重

```js
function unique(arr) {
  return arr.filter(function(item, index, arr) {
    //当前元素，在原始数组中的第一个索引==当前索引值，否则返回当前元素
    return arr.indexOf(item, 0) === index;
  });
}
var arr = [1,1,'RUNOOB','RUNOOB',true,true,15];
console.log(unique(arr))
// [1, "RUNOOB", true, 15]
```

### Array.indexOf()

返回在数组中可以找到一个给定元素的第一个索引，如果不存在，则返回-1

语法：arr.indexOf(searchElement[, fromIndex])

searchElement：需要查招的元素

fromIndex：开始查找的位置。如果该索引值大于或等于数组长度，意味着不会在数组里查找，返回-1。如果参数中提供的索引值是一个负值，则将其作为数组末尾的一个抵消，即-1表示从最后一个元素开始查找，-2表示从倒数第二个元素开始查找 ，以此类推。 注意：如果参数中提供的索引值是一个负值，并不改变其查找顺序，查找顺序仍然是从前向后查询数组。如果抵消后的索引值仍小于0，则整个数组都将会被查询。其默认值为0.

```js
let arr = [1,2,3,4,5,4,3,2,1];
 
console.log(arr.indexOf(1)); // 没有填fromIndex所以默认从索引为0的位置开始往后查找
// 0
console.log(arr.indexOf(1,1)); // 表示从索引为1的位置开始往后查找
// 8
console.log(arr.indexOf(1,-2)); // 表示从倒数第二个索引的位置开始往后查找
// 8
console.log(arr.indexOf(1,-10));  // 负值大于索引长度，从索引0开始往后查找
// 0
```

### String.indexOf()

方法返回调用它的 String 对象中第一次出现的指定值的索引，如果不存在，则返回-1

语法：str.indexOf(searchElement[, fromIndex])

searchStr：需要查招的字符

fromIndex：同上

```js
let str = 'abcdcba';
 
console.log(str.indexOf('a')); // 没有填fromIndex所以默认从索引为0的位置开始往后查找
// 0
console.log(str.indexOf('a',1)); // 表示从索引为1的位置开始往后查找
// 6
```

str.indexOf有一个奇怪的现象，当searchStr是一个==空字符串==的时候，他会返回fromIndex的值，比如fromIndex不填的时候他默认是0，他返回的结果就是0。

```js
let str = 'abcdcba';
let str_null = '';
 
console.log(str_null.indexOf(''));
// 0
console.log(str.indexOf(''));
// 0
console.log(str.indexOf('',0));
// 0
console.log(str.indexOf('',3));
// 3
console.log(str.indexOf('',str.length));
// 7
console.log(str.indexOf('',100));
// 7
```

案例：屏蔽关键是：wc

```js
let str = 'on tow wc tow wc on';
let k = 'wc';
while (str.indexOf(k) != -1){
    str = str.replace(k,'*');
}
console.log(str);
// on tow * tow * on
```

### String.replace()

replace() 方法用于在字符串中用一些字符替换另一些字符，或替换一个与正则表达式匹配的子串

语法：stringObject.replace(regexp/substr,replacement)

说明：regexp/substr（必须），规定子字符串或要替换的模式的RegExp对象。如果该值是一个字符串，则将它作为要检索的直接量文本模式，而不是首先被转换为RegExp对象。

replacement（必须）： 替换文本或生成替换文本的函数
返回值：一个用replacement替换了regexp的第一次匹配或所有匹配之后得到的新字符串。

基本用法1：

```js
var str="Visit Microsoft!"
console.log(str.replace(/Microsoft/, "W3School")); // Visit W3School!
```

replacement 中的 $ 字符具有特定的含义

- $1、$2、...、$99 表示从左到右，正则子表达式(组)匹配到的文本

```js
// 将把 "Doe, John" 转换为 "John Doe" 的形式
var name = "Doe, John";
name.replace(/(\w+)\s*, \s*(\w+)/, "$2 $1"); // John Doe
 
// 把所有的花引号替换为直引号
var name2 = '"a", "b"';
name2.replace(/"([^"]*)"/g, "'$1'");  // "'a', 'b'"
```

* $& 表示regexp 相匹配的子串

```js
var str = 'Visit Microsoft';
str = str.replace(/Visit Microsoft/g,"$& ,W3School");
console.log(str); // Visit Microsoft ,W3School
```

* $` 位于匹配子串左侧的文本

```js
var str = 'Visit Microsoft xxx';
str = str.replace(/Microsoft/g,'$`');
console.log(str); // Visit Visit xxx
```

* $' 位于匹配子串右侧的文本。

```js
var str = 'Visit Microsoft xxx';
str = str.replace(/Visit/g,"$'");
console.log(str); //  Visit xxx xxx 
```

* $$ 直接量符号 插入一个"$"

```js
var str = "javascript";
str = str.replace(/java/,"$$") 
console.log(str); // $script
```

### Array.sort()

sort() 方法用于对数组的元素进行排序。

排序顺序可以是字母或数字，并按升序或降序。

默认排序顺序为按==字母升序==。

```js
var fruits = ["Banana", "Orange", "Apple", "Mango"];
fruits.sort();
// Apple,Banana,Mango,Orange
```

**注意：**当数字是按字母顺序排列时"40"将排在"5"前面。

```js
function myFunction () {
  var points = [40, 100, 1, 5, 25, 10];
  points.sort();
  console.log(points)
}
myFunction()
//[ 1, 10, 100, 25, 40, 5 ]
```

数字排序（升序）

```js
var points = [40,100,1,5,25,10];
points.sort((a, b) => {return a-b});
// 1,5,10,25,40,100
```

数字排序（降序）

```js
function sortName (a, b) {
  return b - a
}
var points = [40, 100, 1, 5, 25, 10];
points.sort(sortName)
console.log(points);
//[ 100, 40, 25, 10, 5, 1 ]
```

### Array.reduce()

reduce() 方法接收一个函数作为累加器，数组中的每个值（从左到右）开始缩减，最终计算为一个值,

reduceRight()(从右到左),` funcs.reverse().reduce()  = funcs.reduceRight `

reduce() 可以作为一个高阶函数，用于函数的 compose。

**注意:** reduce() 对于空数组是不会执行回调函数的。

语法： array.reduce(callback, initialValue)

callback: function(total, currentValue, currentIndex, arr)

total:必需。*初始值*, 或者计算结束后的返回值。

*currentValue*:必需。当前元素

*currentIndex*:可选。当前元素的索引

*arr*:可选。当前元素所属的数组对象。

*initialValue*:可选。传递给函数的初始值(total)

```js
var arr = [1, 2, 3, 4];
var sum = arr.reduce(function(prev, cur, index, arr) {
    console.log(prev, cur, index);
    return prev + cur;
})
console.log(arr, sum);
// 1 2 1
// 3 3 2
// 6 4 3
// [1, 2, 3, 4] 10

var  arr = [1, 2, 3, 4];
var sum = arr.reduce(function(prev, cur, index, arr) {
    console.log(prev, cur, index);
    return prev + cur;
},0) //注意这里设置了初始值
console.log(arr, sum);
// 0 1 0
// 1 2 1
// 3 3 2
// 6 4 3
// [1, 2, 3, 4] 10
```

结论：`如果没有提供initialValue，reduce 会从索引1的地方开始执行 callback 方法，跳过第一个索引。如果提供initialValue，从索引0开始`

数组求和，求乘积

```js
var  arr = [1, 2, 3, 4];
var sum = arr.reduce((x,y)=>x+y)
var mul = arr.reduce((x,y)=>x*y)
console.log( sum ); //求和，10
console.log( mul ); //求乘积，24
```

计算数组中每个元素出现的次数

```js
let names = ['Alice', 'Bob', 'Tiff', 'Bruce', 'Alice'];
 
let nameNum = names.reduce((pre,cur)=>{
  if(cur in pre){
    pre[cur]++
  }else{
    pre[cur] = 1 
  }
  return pre
},{})
console.log(nameNum); //{Alice: 2, Bob: 1, Tiff: 1, Bruce: 1}
```

数组去重

```js
let arr = [1,2,3,4,4,1]
let newArr = arr.reduce((pre,cur)=>{
    if(!pre.includes(cur)){
      return pre.concat(cur)
    }else{
      return pre
    }
},[])
console.log(newArr);// [1, 2, 3, 4]
```

将二维数组转化为一维

```js
let arr = [[0, 1], [2, 3], [4, 5]]
let newArr = arr.reduce((pre,cur)=>{
    return pre.concat(cur)
},[])
console.log(newArr); // [0, 1, 2, 3, 4, 5]
```

将多维数组转化为一维

```js
let arr = [[0, 1], [2, 3], [4,[5,6,7]]]
const newArr = function(arr){
   return arr.reduce((pre,cur)=>pre.concat(Array.isArray(cur)?newArr(cur):cur),[])
}
console.log(newArr(arr)); //[0, 1, 2, 3, 4, 5, 6, 7]
```

对象里的属性求和

```js
var result = [
    {
        subject: 'math',
        score: 10
    },
    {
        subject: 'chinese',
        score: 20
    },
    {
        subject: 'english',
        score: 30
    }
];
 
var sum = result.reduce(function(prev, cur) {
    return cur.score + prev;
}, 0);
console.log(sum) //60
```

### 自定义compose函数

对于`(fn3(fn2(fn1(1))))`嵌套逻辑利用compose函数`compose(fn3, fn2, fn1)(1)`

```js
function compose(...funcs) {
    //=>funcs:传递的函数集合
    console.log('---funcs---',funcs)
    return function proxy(...args) {
        //=>args:第一次调用函数传递的参数集合
        let len = funcs.length;
        if (len === 0) {
            //=>一个函数都不需要执行,直接返回args
            return args;
        }
        if (len === 1) {
            //=>只需要执行一个函数，把函数执行，把其结果返回即可
            return funcs[0](...args);
        }
        //方式一
        return funcs.reduceRight((x, y) => {
            console.log('--x--',x)
            console.log('--y--',y)
            return typeof x === "function" ? y(x(...args)) : y(x)
        });
        //方式二
         return funcs.reverse().reduce((x, y) => {
            console.log('--x--',x)
            console.log('--y--',y)
            return typeof x === "function" ? y(x(...args)) : y(x)
        });
    };
}
const fn1 = (x) => x + 10;
const fn2 = (x) => x * 10;
const fn3 = (x) => x - 10;
let result = compose(fn3, fn2, fn1)(1);
console.log('--result--',result);

 /*
---funcs--- [ [Function: fn3], [Function: fn2], [Function: fn1] ]
--x-- [Function: fn3]
--y-- [Function: fn2]
--x-- -90
--y-- [Function: fn1]
--result-- -80
*/
```

### Array.join()

join() 方法用于把数组中的所有元素转换一个字符串,元素是通过指定的分隔符进行分隔的。

语法：`array.join(separator)`

*separator*:可选。指定要使用的分隔符。如果省略该参数，则使用逗号作为分隔符

无缝拼接

```js
let s = Array('a', 'p', 'p', 'l', 'e')
console.log(s.join(''))
//apple
```

空格分隔

```js
let s = Array('Apple','is','on','my','table')
console.log(s.join(' '))
//Apple is on my table
```

### Array.includes()

includes() 方法用来判断一个数组是否包含一个指定的值，如果是返回 true，否则false.

语法:`arr.includes(searchElement, fromIndex)`

*searchElement*: 必须。需要查找的元素值。

*fromIndex*:可选。从该索引处开始查找 searchElement。如果为负值，则按升序从 array.length + fromIndex 的索引开始搜索。默认为 0。

```js
[1, 2, 3].includes(2);     // true
[1, 2, 3].includes(4);     // false
[1, 2, 3].includes(3, 3);  // false
[1, 2, 3].includes(3, -1); // true
[1, 2, NaN].includes(NaN); // true

const str = 'do not worry be happy'
console.log(str.includes('do')) // true
console.log(str.includes('don'))  // false
```

如果fromIndex ==大于等于==数组长度 ，则返回 false 。该数组不会被搜索:

```js
var arr = ['a', 'b', 'c'];
arr.includes('c', 3);   //false
arr.includes('c', 100); // false
```

如果 fromIndex 为负值，计算出的索引将作为开始搜索searchElement的位置。如果计算出的索引小于 0，则整个数组都会被搜索。

### Array.concat()

concat() 方法用于连接两个或多个数组。

该方法不会改变现有的数组，而仅仅会返回被连接数组的一个副本。

语法:`array1.concat(array2,array3,...,arrayX)`

```js
var hege = ["Cecilie", "Lone"];
var stale = ["Emil", "Tobias", "Linus"];
var kai = ["Robin"];
var children = hege.concat(stale,kai);
// 
//Cecilie,Lone,Emil,Tobias,Linus,Robin
```

### Array.map()

map() 方法返回一个新数组，数组中的元素为原始数组元素调用函数处理后的值。

map() 方法按照原始数组元素顺序依次处理元素。

**注意：** map() 不会对空数组进行检测。

**注意：** map() 不会改变原始数组。

语法:`array.map(function(currentValue,index,arr), thisValue)`

*currentValue*:必须。当前元素的值

*index*:可选。当前元素的索引值

arr:可选。当前元素属于的数组对象

*thisValue*:可选。对象作为该执行回调时使用，传递给函数，用作 "this" 的值。如果省略了 thisValue，或者传入 null、undefined，那么回调函数的 this 为全局对象。

```js
const arr = [
  [1, 1],
  [2, 2],
  [3, 3],
  [4, 4]
];
const newArr = arr.map(([x, y]) => x + y);
console.log(newArr) // [2,4,6,8]
// 基础写法
var numbers = [4, 9, 16, 25];

function myFunction() {
    x = document.getElementById("demo")
    x.innerHTML = numbers.map(Math.sqrt);
}
// 2,3,4,5
```

### Array.copyWithin()

copyWithin() 方法用于从数组的指定位置拷贝元素到数组的另一个指定位置中。(改变原数组)

语法：`array.copyWithin(target, start, end)`

*target*: 必需。复制到指定目标索引位置。

*start*:可选。元素复制的起始位置。

*end*:可选。停止复制的索引位置 (默认为 *array*.length)。如果为负值，表示倒数

```js
var fruits = ["Banana", "Orange", "Apple", "Mango", "Kiwi", "Papaya"];

console.log(fruits.copyWithin(2, 1, 3))
//[ 'Banana', 'Orange', 'Orange', 'Apple', 'Kiwi', 'Papaya' ]
```

### Array.every()

every() 方法用于检测数组所有元素是否都符合指定条件（通过函数提供）。

every() 方法使用指定函数检测数组中的所有元素：

- 如果数组中检测到有一个元素不满足，则整个表达式返回 *false* ，且剩余的元素不会再进行检测。
- 如果所有元素都满足条件，则返回 true。

**注意：** every() 不会对空数组进行检测。

**注意：** every() 不会改变原始数组。

语法：`array.every(function(currentValue,index,arr), thisValue)`

参数同map

```js
var ages = [32, 33, 16, 40];

console.log(ages.every((age) => age >= 18))
//false
```

### Array.splice() 

splice() 方法用于添加或删除数组中的元素。

**注意：**这种方法会改变原始数组。

返回值:如果删除一个元素，则返回一个元素的数组。 如果未删除任何元素，则返回空数组。

语法：`array.splice(index,howmany*,*item1*,.....,*itemX*)`

*index*:必需。规定从何处添加/删除元素。该参数是开始插入和（或）删除的数组元素的下标，必须是数字。

*howmany*:可选。规定应该删除多少元素。必须是数字，但可以是 "0"。如果==未规定==此参数，则删除从 index 开始到原数组结尾的所有元素。

*item1*, ..., *itemX*:可选。要添加到数组的新元素

返回值Array：如果从 arrayObject 中删除了元素，则返回的是含有被删除的元素的数组。

```js
var fruits = ["Banana", "Orange", "Apple", "Mango"];
var a = fruits.splice(2, 2);
console.log(fruits) //[ 'Banana', 'Orange' ]
console.log(a) //[ 'Apple', 'Mango' ]
fruits.splice(2,0,"Lemon","Kiwi"); //[ 'Banana', 'Orange', 'Lemon', 'Kiwi' ]
```

