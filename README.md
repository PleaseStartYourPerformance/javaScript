# JavaScript:一年后你会感谢今天的自己
## 7.17:考虑到性能问题，如何快速从一个巨大的数组中随机获取部分元素 比如有个数组有100K个元素，从中不重复随机选取10K个元素。
```js
const arrRadom = function (len,arrlen) {
  let set = new Set();
  let result = []
  let arr = Array.from({length:arrlen},(v,i)=>i);
  while(set.size < len){
    let index  = Math.floor(Math.random() * arrlen);
    set.add(index);
  }
  for(let i of set.values()) {
    result.push(arr[i]);
  }
  return result;
}
```
扩展：
>数组转set new Set(arr)  
set转数组 Array.from(set)<br>
es6 Set(); 
似于数组，但它的一大特性就是所有元素都是唯一的，没有重复。<br>
我们可以利用这一唯一特性进行数组的去重工作。<br>
let list=new Set([1,1,2,3,4])<br>

set中数组长度 list.size
(1)添加元素 add<br>
let list=new Set();<br>
list.add="1"<br>
list.add="2"<br>
list.add(2)//类似数组push<br>
(2)删除元素 delete<br>
let list=new Set([1,2,3,4])<br>
list.delete(2)<br>
(3).判断某元素是否存在 has<br>
let list=new Set([1,2,3,4])<br>
list.has(2)//true<br>
(4)清除所有元素 clear<br>
let list=new Set([1,2,3,4])<br>
list.clear()<br>
(5)遍历 keys()<br>
let list=new Set(['a','b','c'])<br>
for(let key of Set.keys()){<br>
console.log(key)//a,b,c<br>
}<br>
(6)遍历 values()<br>
let list=new Set(['a','b','c'])<br>
for(let value of Set.values()){<br>
console.log(value)//a,b,c<br>
}<br>
(7)遍历 entries()<br>
let list=new Set(['4','5','hello'])<br>
for(let item of Set.entries()){<br>
console.log(item )//[ 4, 4 ][ 5, 5 ][ 'hello', 'hello' ]<br>
}<br>
(8)遍历 forEach()<br>
let list=new Set(['4','5','hello'])<br>
list.forEach(function((item){<br>
console.log(item)<br>
})<br>
(8)数组转Set<br>
let set2 = new Set([4,5,6])<br>
let set3 = new Set(new Array(7, 8, 9))<br>
(9)Set转数组<br>
let set4 = new Set([4, 5, 6])<br>
console.log('set to array 1:', [...set4])<br>
console.log('set to array 2:', Array.from(set4))<br>
## 7.18:请写出下列代码的返回值
```js
var name = 'Tom';
(function() {
    if (typeof name == 'undefined') {
        var name = 'Jack';
        console.log('Goodbye ' + name);
    } else {
        console.log('Hello ' + name);
    }
})();
```
解析:<br>
其实这个面试题说到底 就是考了一句话  函数在执行的时候会会先进行变量提升<br> 
 如果没有 var name = 'Jack' 那么就不会存在变量提升  
 打印的就是hello Tom 但是存在var name = 'Jack' 
 立即执行函数的var name会提升到最前面  name = undefined  
## 7.19 扩展上一题
```js
var name = 'Tom';
(function() {
    if (typeof name == 'undefined') {
        name = 'Jack';
        console.log('Goodbye ' + name);
    } else {
        console.log('Hello ' + name);
    }
})();
```
解析：<br>
1、首先在进入函数作用域当中，获取name属性<br>
2、在当前作用域没有找到name<br>
3、通过作用域链找到最外层，得到name属性<br>
4、执行else的内容，得到Hello Tom<br>

## 7.23:编程题
 
> 第 111 题：编程题，写个程序把 entry 转换成如下对象
 ```js
 var entry = {
   a: {
     b: {
       c: {
        dd: 'abcdd'
      }
     },
     d: {
       xx: 'adxx'
    },
    e: 'ae'
   }
 }
// 要求转换成如下对象
  var output = {
   'a.b.c.dd': 'abcdd',
  'a.d.xx': 'adxx',
 'a.e': 'ae'
 }
  ```
解析:
 ```js
        function ent(entry,prevKey=null,result = {}) {
        Object.keys(entry).forEach(item=>{
           //记录对象的键值
            prevKey =  prevKey ? `${prevKey}.${item}` : item;
           if(Object.prototype.toString.call(entry[item]) === '[object Object]'){
               //递归往下走
               ent(entry[item],prevKey,result);
          }else{
                //找不到了后赋值操作然后继续循环下一条
              result[prevKey] = entry[item]
            }
       })
      return result
   }
   console.log(ent(entry));
 ```
## 7.24:编程题写个程序把 entry 转换成如下对象（跟昨日题目相反）
```js
var entry = {
  'a.b.c.dd': 'abcdd',
  'a.d.xx': 'adxx',
  'a.e': 'ae'
}
// 要求转换成如下对象
var output = {
  a: {
   b: {
     c: {
       dd: 'abcdd'
     }
   },
   d: {
     xx: 'adxx'
   },
   e: 'ae'
  }
}
```
解析：
## 7.26:编程题，找出字符串中连续出现最多的字符和个数（蘑菇街）
>'abcaakjbb' => {'a':2,'b':2}<br>
>'abbkejsbcccwqaa' => {'c':3}<br>

解析:
```js
//大佬
const arr = str.match(/(\w)\1*/g);
const maxLen = Math.max(...arr.map(s => s.length));
const result = arr.reduce((pre, curr) => {
  if (curr.length === maxLen) {
    pre[curr[0]] = curr.length;
  }
  return pre;
}, {});
//我---只能筛选出全部。。。
 function typefilter(str) {
        let obj = {}
        str.split('').forEach(item=>{
            obj[item] === undefined ?  obj[item] = 1 : obj[item]++
        })
        return obj
    }
    console.log(typefilter(b));
console.log(result);
```
## 7.30:输出以下代码运行结果
>1 + "1"<br>
>2 * "2"<br>
>[1, 2] + [2, 1]<br>
>"a" + + "b"

解析：
```js
'11'
 4
'1,22,1'
'aNaN'
```
## 8.1:编程题--递归
>1.创建一个长度为5得数据arr<br>
>2.生成一个（min,max）之间得随机整数 rand<br>
>3.把随机数rand插入到数组arr中，如果数组arr内存在于rand相同的数字，则重新生成
>随机数边插入arr中（需要使用递归不能使用for和while等遍历器）<br>
>4.最终输出一个长度为5，内容不重复的arr
```js
    function filter(max,min,arr,index) {
        var random = () => Math.floor(Math.random()*(max-min)+min)
        var item = random()
        if(index === 5){
            return arr
        }
        if(arr.includes(item)){
            item = random()
        }
        arr[index] = item;
        filter(max,min,arr,++index)
        return arr
    }
    console.log(filter(100, 1,[], 0));
```
## 8.5:为什么for循环嵌套顺序会影响性能
```js
var t1 = new Date().getTime()
for (let i = 0; i < 100; i++) {
  for (let j = 0; j < 1000; j++) {
    for (let k = 0; k < 10000; k++) {
    }
  }
}
var t2 = new Date().getTime()
console.log('first time', t2 - t1)
//first time 280
for (let i = 0; i < 10000; i++) {
  for (let j = 0; j < 1000; j++) {
    for (let k = 0; k < 100; k++) {

    }
  }
}
var t3 = new Date().getTime()
console.log('two time', t3 - t2)  
//two time 359
```
解析：
```js
两个循环的次数的是一样的，但是 j 与 k 的初始化次数是不一样的
第一个循环的 j 的初始化次数是 100 次，k 的初始化次数是 10w 次
第二个循环的 j 的初始化次数是 1w 次， k 的初始化次数是 1000w 次
所以相同循环次数，外层越大，越影响性能
```
## 10.9: 手写call apply bind义及实现原理详见201910.9.html
```js
Function.prototype.myCall = function (context) {
    if (typeof context === 'undefined' || context === null) {
        context = window
    }
    //context是传入的this也就是food函数  this是product函数this也是指向这个函数
    context.fn = this
    //获取传入除了this的参数 也是product的参数 也就是 args=['chese',5]
    let args = [...arguments].slice(1);
    //content.fn 为product这个函数  ...args为解构传参也就是此时相当于在product函数中进行传参
    let result = context.fn(...args)
    delete context.fn
    return result
}
```
```js
Function.prototype.myApply = function(context) {
    if (typeof context === 'undefined' || context === null) {
        context = window
    }
    context.fn = this
    //与call的区别就是 后面的参数使用了数组 那么arguments[1]才是我们想要的参数
    let args = arguments[1]
    let result
    args ? result = context.fn(...args) : result = context.fn()
    delete context.fn
    return result
}
```
```js
  Function.prototype.myBind = function(context) {
        if (typeof this !== 'function') {
            throw new TypeError('Error')
        }
        let _this = this
        let args = [...arguments].slice(1)
        return function F() {
            // 判断是否被当做构造函数使用
            if (this instanceof F) {
                return _this.apply(this, args.concat([...arguments]))
            }
            return _this.apply(context, args.concat([...arguments]))
        }
    }
```
```js
function product(name,price) {
    this.name = name
    this.price = price
}
function Food(name, price) {
    product.myApply(this, [name, price]);
    product.myCall(this, [name, price]);
}
console.log(new Food('cheese', 5).name);
```
