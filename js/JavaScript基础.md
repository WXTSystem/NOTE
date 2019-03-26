# 数据类型

简单数据类型

1. Undefined
2. Null
3. Boolean
4. Number
5. String

复杂数据类型

1. Object



## 数据类型检测typeof

undefined、boolean、string、number、object、function



# Boolean和其他类型转换

可以使用Boolean()函数进行转换

```javascript
Boolean("aaa")==true
var message="hello";
//流控制语句（如if）会自动执行相应的Boolean转换
if(message)
{
    
}
```



| 数据类型  | 转换为true的值               | 转换为false的值 |
| --------- | ---------------------------- | --------------- |
| Boolean   | true                         | false           |
| String    | 任何非空字符串               | ""              |
| Number    | 任何非零数字值（包括无穷大） | 0和NaN          |
| Object    | 任何对象                     | null            |
| Undefined |                              | undefined       |



# 执行环境及作用域

1. 如果初始化变量时没有使用var声明，该变量会自动被添加到全局环境
2. 没有块级作用域，if或for中的变量声明会将变量添加到当前的执行环境中

## 管理内存

​	使用具备垃圾收集机制的语言编写程序，开发人员一般不必操心内存管理的问题。但是， JavaScript
在进行内存管理及垃圾收集时面临的问题还是有点与众不同。其中最主要的一个问题，就是分配给 Web
浏览器的可用内存数量通常要比分配给桌面应用程序的少。这样做的目的主要是出于安全方面的考虑，
目的是防止运行 JavaScript 的网页耗尽全部系统内存而导致系统崩溃。内存限制问题不仅会影响给变量
分配内存，同时还会影响调用栈以及在一个线程中能够同时执行的语句数量。
​	因此，确保占用最少的内存可以让页面获得更好的性能。而优化内存占用的最佳方式，就是为执行
中的代码只保存必要的数据。一旦数据不再有用，最好通过将其值设置为 null 来释放其引用——这个
做法叫做解除引用（dereferencing）。这一做法适用于大多数全局变量和全局对象的属性。局部变量会在
它们离开执行环境时自动被解除引用 。





# 函数声明和函数表达式

解析器会率先读取函数声明，并使其在执行任何代码之前可用；至于函数表达式，则必须等到解析器执行到它所在的代码行，才会真正被解释执行

```javascript
alert(sum(10,10));
function sum(num1,num2)
{
    return num1+num2
}
```

以上代码可以正常运行





```javascript
alert(sum(10,10));
var sum=function(num1,,num2)
{
    return num1+num2
}
```

以上代码会在运行期间产生错误

