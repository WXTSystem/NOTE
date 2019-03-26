# 基础语法

1. js不强制要求在每个语句后面加;  浏览器中负责执行js代码的引擎会自动在每个语句的结尾补上;

   + 让js引擎自动加分好在某些情况下会该表程序的语义，导致 运行结果与期望不一样，尽量不省略

2. js不区分整数和浮点数，统一用Number表示

   + 十六进制0x前缀

3. ==与===

   + ==它会自动转换类型再比较
   + ===不会自动转换数据类型，数据类型不一致，直接返回false（推荐使用）

4. NaN这个特殊的Number与所有其他值都不相等，包括他自己

   + NaN===NaN //false
   + 只有isNaN()函数能判断  isNaN(NaN)//true

5. 浮点数比较

   + 浮点数运算过程中会产生误差，比较的时候最好计算他们之差的绝对值，看看是否小于某个阈值

     ```javascript
     Math.abs(1/3-(1-2/3))<0.0000001;//true
     ```

6. nullhe和defined

   + 在判断函数参数是否传递的情况下使用undefined

7. 数组

   + [1,2,3,'hello',null,true]
   + 通过new Array(1,2,3)创建数组

8. 如果一个变量没有通过var申明就被使用，那么该变量就自动被申明为全局变量，es在后续规范中推出了strict模式，在strict模式下运行的js代码，强制通过var申明变量，未使用var申明就使用的，将导致运行错误

   第一行加上‘use strict’


# 字符串

1. 转义字符

   ASCII字符可以以\x##形式的十六进制表示

   console.log('\x41')  //等同于A

2. 多行字符串（ES6）

   反引号表示

   ```javascript
   `这是一个
   多行
   字符串`
   ```

3. 模板字符串（ES6）

   多字符串拼接用+号，es6新增模板字符串

   ```javascript
   var name='小明'
   var age=20
   var message=`你好，${name},你今年${age}岁了！`
   ```

4. 获取指定位置的字符

   var s="hello world"

   s[0] //'h',可以获取，但是s[0]赋值无效，不会改变s

5. toUpperCase()和toLowerCase()

6. indexOf()

7. substring()

   (0,5)从0到5 //（不包括5）

   一个参数(7)  //从7到最后

# 数组

1. 直接给Array的length赋一个新值会导致Array大小的变化

   ```javascript
   var arr=[1,2,3]
   arr.length; //3
   arr.length=6;//
   arr;//[1,2,3,undefined,undefined,undefined]
   arr.length=2
   arr;//[1,2]
   ```

2. 可以通过索引赋值，如果索引超过了范围，也会引起Array大小的变化

   ```javascript
   var arr=[1,2,3]
   arr[5]='x'
   arr.length//6
   ```

3. 常用函数

   1. indexOf

      搜索指定元素的位置

   2. slice

      对应String的substring，截取Array的部分元素，并返回一个新的Array，包括开始不包括结束

   3. push和pop

      push向Array的末尾添加若干元素，返回Array的新长度

      pop把Array的最后一个元素删掉，返回已删除的那个元素，空数组继续pop返回undefined

   4. unshift和shift

      unshift()往Array头部添加若干元素

      shift()把Array的第一个元素删掉

   5. sort()对当前Array进行排序

   6. reverse()把Array反转

   7. splice()是修改Array的‘万能方法’，从指定索引开始删除若干元素，然后从该位置添加若干元素

      ```javascript
      var arr=[1,2,3]
      arr.slice(0,2,'a','b')//返回删除的元素[1,2]
      arr;//['a','b',3]
      ```

   8. concat把当前的Array和另一个Array连接起来，并返回一个新的Array，可以接收任意个元素和Array

   9. join() 把当前Array的每个元素都用指定的字符串连接起来，并返回，不传参用,分隔



# 值类型

undefined, number, string, boolean



# js中的true和false

以下内容会被当成false处理：**"" , false , 0 , null , undefined , NaN**

其他都是true。注意：字符串"false"也会被当做true处理，在未转型的情况下他是字符串，属于一个对象，所以是true。





# typeof和instanceof

**typeof是一个操作符而不是函数**

null==undefined //true

null===undefined//false

js中typeof只有以下类型：

1. undefined
2. number
3. string
4. boolean
5. function
6. object



检测基本数据类型使用typeof

检测引用类型时，使用instanceof





​	