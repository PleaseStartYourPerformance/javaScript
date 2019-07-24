# JavaScript:一年后你会感谢今天的自己
#7.17:考虑到性能问题，如何快速从一个巨大的数组中随机获取部分元素 比如有个数组有100K个元素，从中不重复随机选取10K个元素。
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
数组转set new Set(arr)  set转数组 Array.from(set)<br>
es6 Set(); 
似于数组，但它的一大特性就是所有元素都是唯一的，没有重复。<br>
我们可以利用这一唯一特性进行数组的去重工作。<br>
let list=new Set([1,1,2,3,4])<br>
(1)添加元素 add<br>
let list=new Set();<br>
list.add="1"<br>
list.add="2"<br>
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
#7.18:请写出下列代码的返回值
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
#7.19 扩展上一题
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


#7.23:编程题
 
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
#7.24:编程题写个程序把 entry 转换成如下对象（跟昨日题目相反）
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
