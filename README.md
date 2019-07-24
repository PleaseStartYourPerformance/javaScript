# JavaScript:每日一题，一年后你会感谢今天的自己
 // 7.23:编程题
 
> 第 111 题：编程题，写个程序把 entry 转换成如下对象
>
> ```js
> var entry = {
>   a: {
>     b: {
>       c: {
>         dd: 'abcdd'
>       }
>     },
>     d: {
>       xx: 'adxx'
>     },
>     e: 'ae'
>   }
> }
> 
> // 要求转换成如下对象
>   var output = {
>   'a.b.c.dd': 'abcdd',
>   'a.d.xx': 'adxx',
> 'a.e': 'ae'
> }
# 解析
> ```js
>        function ent(entry,prevKey=null,result = {}) {
>        Object.keys(entry).forEach(item=>{
>            //记录对象的键值
>            prevKey =  prevKey ? `${prevKey}.${item}` : item;
>            if(Object.prototype.toString.call(entry[item]) === '[object Object]'){
>                //递归往下走
>                ent(entry[item],prevKey,result);
 >           }else{
>                //找不到了后赋值操作然后继续循环下一条
>                result[prevKey] = entry[item]
>            }
>        })
 >       return result
 >   }
 >   console.log(ent(entry));