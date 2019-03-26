# let和const

## let

+ let用法类似var，但是声明的变量只在let命令所在的代码块内有效

+ 不存在变量提升，必须先声明后使用，否则会报错

+ ES6规定，如果块区中存在let和const命令，这个区块对这些命令声明的变量，从一开始就形成了封闭作用域。凡是在声明之前就使用这些变量，就会报错

  ```javascript
  //在代码块内，使用let命令声明变量之前，该变量都是不可用的，这在语法上，称为‘暂时性死区TDZ’
  var tmp=123
  if(true)
  {
      tmp='abc'; //ReferenceError
      let tmp;
  }
  
  
  //示例2
  if(true)
  {
      //TDZ开始
      tmp='abc'//ReferenceError
      console.log(tmp)//ReferenceError
      
      let tmp //TDZ结束
      
      console.log(tmp)//undefined
      tmp=123
      console.log(tmp)//123
  }
  //暂时性死区的本质就是，只要一进入当前作用域，所要使用的变量就已经存在了，但是不可获取，只有等到声明变量的那一行代码出现，才可以获取和使用该变量。
  ```

+ 不允许重复声明

  let不允许在相同的作用域内，重复声明同一个变量

  ```javascript
  //报错
  function func(){
      let a=10;
      var a=1;
  }
  ```

  

+ let实际上为js新增了块级作用域

  外层作用域无法读取内层作用域的变量，内层作用域可以定义外层作用域的同名变量

+ ES6 引入了块级作用域，明确允许在块级作用域之中声明函数。ES6 规定，块级作用域之中，函数声明语句的行为类似于`let`，在块级作用域之外不可引用。



## const

const声明一个只读的常量，一旦声明，常量的值就不能改变

const一旦声明变量，就必须立即初始化

const的作用域与let命令相同：只在声明所在的块级作用域内有效

**const命令声明的常量也是不提升，也存在暂时性死区，不可重复声明**



```javascript
////consy保证的是变量指向的那个内存地址所保存的数据不得改动
///对于对象，它指向的数据结构可改变
const foo={}
foo.prop=123 //可以成功
foo={}//指向另一个对象，会报错
```



## 顶层对象的属性

let、const、class声明的全局变量，不属于顶层对象的属性

```javascript
var a=1;
window.a //1

let b=1
window.b //undefined
```





# 变量的解构赋值

ES6允许按照一定模式，从数组和对象中提取值，对变量进行赋值，这被称为解构

```javascript
let [a,b,c]=[1,2,3]//可以从数组中提取值，按照对应位置对变量赋值
//本质上，这种写法属于‘模式匹配’，只要等号两边的模式相同，左边的变量就会被赋予对应的值

let[foo,[[bar],baz]]=[1,[[2],3]]
let[,,third]=['foo','bar','baz']//third='baz'
//结构不成功，变量值为undefined

//不完全匹配也能成功
let[a,[b],d]=[1,[2,3],4]  //a 1 b 2 d 4

//如果等号的右边不是数组（或不是可遍历的结构，会报错）
let[foo]=1 //报错
let[f00]={}//报错
```







