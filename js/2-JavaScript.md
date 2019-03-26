# 对象

1. 访问属性是通过.操作符完成的，如果属性名包含特殊字符，就必须用''括起来

   ```javascript
   var xiaohong={
       name:'xx',
       'middile-school':'123'
   }
   ```

   middile-school不是一个有效的变量名，必须用''包含，访问时，通过xiaohong['middile-school']访问

2. 访问不存在的属性返回undefined

3. 添加和删除属性

   ```javascript
   var stu={
       name:'a'
   }
   str.age=18//新增age属性
   delete stu.name //删除name属性
   ```

4. 检测是否拥有属性

   'name' in stu //检测stu对象是否有name属性，也有可能是stu继承的，也会返回true

5. 判断属性是自身拥有而不是继承得到的，用hasOwnProperty

   stu.hasOwnProperty('name')

6. 获取所有属性

   数组也是对象，针对数组遍历是，key为索引，且key是String而不是Number

   ```javascript
   var o={
       name:'a',
       age:10
   }
   for(vae key in o)
   {
    console.log(key) //name,age   
   }
   ```



# Map和Set（ES6）

## Map



Map引入主要为了解决键值必须是字符串的问题，其他数据类型其实也可以作为键

初始化Map需要一个二维数组，或者直接初始化一个空Map

```javascript
var m=new Map()
var map=new Map([["A",100],["B",200],["C",300]])
map.get("A")//100
map.set("A",10)
map.delete("A")
```

多次set，后面的值会替换之前的

## Set

Set是一组key的集合，不存储value，没有重复的key

```javascript
var s1=new Set()
var s2=new Set([1,2,3])
var s3=new Set([1,2,3,3,'3'])//重复元素会自动被过滤变为[1,2,3,'3']
s3.delete(1)
```



# Iterable类型（ES6）

Array可以采用下标循环，Map和Set无法使用下标，为了统一集合类型，ES6引入Iterable类型

**Array、Map、Set都属于iterable类型**

iterable类型的集合可以通过for ...of（ES6引入）循环来遍历

for x of Iterable

Array 是元素

Set是key

Map是一维数组 [key,value]



更好的方式是使用iterable内置的forEach方法

```javascript
var a=['A','B','C']
a.forEach(function(element,index,array){
    // element: 指向当前元素的值
    // index: 指向当前索引
    // array: 指向Array对象本身
    console.log(element + ', index = ' + index);
})
//Map参数依次为value、key和map本身
//Set参数依次为key，key和Set本身
```







# for in 和for of

`for ... in`循环由于历史遗留问题，它遍历的实际上是对象的属性名称。一个`Array`数组实际上也是一个对象，它的每个元素的索引被视为一个属性。

Map使用for in时 

var key in map //获取不到值

当我们手动给`Array`对象添加了额外的属性后，`for ... in`循环将带来意想不到的意外效果：

```javascript
var a = ['A', 'B', 'C'];
a.name = 'Hello';
for (var x in a) {
    console.log(x); // '0', '1', '2', 'name'
}
```

`for ... in`循环将把`name`包括在内，但`Array`的`length`属性却不包括在内。

`for ... of`循环则完全修复了这些问题，它只循环集合本身的元素：

```javascript
var a = ['A', 'B', 'C'];
a.name = 'Hello';
for (var x of a) {
    console.log(x); // 'A', 'B', 'C'
}
```



# 函数

js允许传入任意个参数而不影响调用，可以比定义多或者少，少时，未传的参数为undefined

在向参数传递基本类型的值时，被传递的值会被复制给一个局部变量；在向参数传递引用类型的值时，会把这个值在内存中的地址，复制给一个局部变量。

## arguments

只在函数内部起作用，永远指向当前函数调用者传入的所有参数，类似Array但不是Array，可以for循环遍历

## rest参数（ES6）

```javascript
function foo(a,b,...rest)
{
    //rest用来接收a、b以为的所有参数，数组
}
```

rest参数只能写在最后，前面用...标识，没传入时为空数组



## 变量作用域与解构赋值

由于js的函数可以嵌套，此时，内部函数可以访问外部函数定义的变量，反过来则不行



js的函数在查找变量时从自身函数定义开始。如果重名，按自身定义的变量为准

```javascript
function foo()
{
    var x=1;
    function bar()
    {
        var x='A'
        console.log('x in bar='+x)
    }
    console.log('x in foo='+x)
    bar();
}

foo();
//x in foo=1
//x in bar=A
```



## 变量提升

js的函数定义有个特点，它会先扫描整个函数体的语句，把所有申明的变量“提升‘到函数顶部''

```javascript
'use strict'
function foo()
{
    var x='Hello' + y;
    console(x)
    var y='World'
}
foo()
//不会报错，输出Hello Undefined
//因为js引擎自动提升了变量y的声明，但是不会提升变量y的赋值
```

## 全局作用域

js默认有一个全局对象window，全局变量实际上被绑定到window的一个属性

```javascript
var course='Js'
course===window.course//true
//一些全局函数也是
alert===window.alert//true
```

不同的js文件使用了相同的全局变量，会引起冲突，最好的办法是把自己所有变量和函数绑定到一个全局变量中

js文件中只定义一个全局变量（jquery，YUI，underscore）



## 局部作用域

js变量作用域是函数内部，for循环等语句块中无法定义具有局部作用域的变量

```javascript
function foo()
{
    for(var i=0;i<100;i++)
    {
        
    }
    i+=100;//仍然有用
}
```

### 块级作用域let（ES6）

用let替代var可以申明一个块级作用域的变量

```javascript
function foo()
{
    var sum=0;
    for(let i=0;i<100;i++)
    {
        sum+=i
    }
    //SyntaxError,i is undefined
    i+=1;
}
```

## 常量const（ES6）

```javascript
const PI=3.14
PI=3//有的会报错，有的不报错但是无效
```

## 解构赋值（ES6）

对一组变量进行赋值

```javascript
var [x,y,z]=['1','2','3']//x,y,z分别被赋值为数组对应元素
let [x,[y,z]]=['1',['2','3']]//x,y,z分别为'1' '2' '3'
let [,,z]=['1','2','3'] //只赋值z
//从对象中取若干属性
'use strict';
var person = {
    name: '小明',
    age: 20,
    gender: 'male',
    passport: 'G-12345678',
    school: 'No.4 middle school'
};
var {name, age, passport} = person; 
//嵌套的对象
var person = {
    name: '小明',
    age: 20,
    gender: 'male',
    passport: 'G-12345678',
    school: 'No.4 middle school',
    address: {
        city: 'Beijing',
        street: 'No.1 Road',
        zipcode: '100001'
    }
};
var {name,address: {city, zip}} = person;
name; // '小明'
city; // 'Beijing'
zip; // undefined, 因为属性名是zipcode而不是zip
// 注意: address不是变量，而是为了让city和zip获得嵌套的address对象的属性:
address; // Uncaught ReferenceError: address is not defined
//要获取address var {name,address,address:{city,zip}}

//使用的变量名和属性名不一致
var {name,passport:id}=person//passport不是变量，引用会报错，只是为了让变量id获得paaport属性

//使用默认值
//single属性不存在时防止默认为undefined
var {name,school='123',single=true}=person

//如果变量已经被声明，再次赋值的时候，正确的写法也会报错
var x,y;
{x,y}={name:'11',x:100,y:200}//报错，因为js引擎把{开头的语句当做了块处理，=不再合法，应使用（）括起来
({x,y}={name:'',x:1,y:})
```

如果一个函数接收一个对象作为参数，那么，可以使用解构直接把对象的属性绑定到变量中



##  this

```javascript
function getAge()
{
    var y=new Date().getFullYear();
    return y-this.birth;
}
var xiaoming={
    name:'小明',
    birth:1990,
    age:getAge
};
xiaoming.age();//25正常
getAge();//NaN
```

this指向视情况而定

1. xiaoming.age(),this定义在age内部

   this指向被调用的对象，也就是xiaoming

2. 单独调用getAge()

   该函数的this指向全局对象，也就是window

   strict模式下为undefined

3. var fn=xiaoming.age();

   fn();

   this也不是指向xiaoming对象，指向window

   strict模式下this为undefined

4. 在函数内部定义的函数

   this指向window

   strict模式下为undefined



要保证this指向正确，必须用obj.xxx()的形式调用



## apply和call

### 控制this指向

函数本身都有个apply方法，接收两个参数，第一个参数就是需要绑定的this变量，第二个参数是Array，表示函数本身的参数

```javascript
function getAge() {
    var y = new Date().getFullYear();
    return y - this.birth;
}

var xiaoming = {
    name: '小明',
    birth: 1990,
    age: getAge
};

xiaoming.age(); // 25
getAge.apply(xiaoming, []); // 25, this指向xiaoming, 参数为空
```

call和apply类似，唯一的区别是apply把参数打包成Array再传入，call把参数按顺序传入

```javascript
Math.max.apply(null, [3, 5, 4]); // 5
Math.max.call(null, 3, 5, 4); // 5
```

对于普通函数调用，我们通常把this绑定为null



### 装饰器，动态改变函数的行为

js所有的对象都是动态的，即使内置的函数，我们可以将内置函数重新指向新的函数



```javascript
//我们想统计一共调用了多少次parseInt()
var count=0;
var oldParseInt=parseInt;
window.parseInt=function()
{
    count+=1;
    return oldParseInt.apply(null,arguments);
}
```

## 高阶函数

一个函数可以接收另一个函数作为参数，这种函数就称之为高阶函数

```javascript
//示例
function add(x,y,f)
{
    return f(x)+f(y)
}
```

### map和reduce(Array的方法)

Array的方法map

map传入我们定义的方法，作用于数组每一个成员并将新的数组返回





```javascript
function pow(x)
{
    return x*x
}
var arr=[1,2,3]
var results=arr.map(pow) //[1,4,9]
```

```javascript
['1', '2', '3'].map(parseInt);
// While one could expect [1, 2, 3]
// The actual result is [1, NaN, NaN]
```

**标准情况下，会给map中函数传递3个参数item,index,array本身
parseInt平常使用都传递一个参数，实际上他可以接收两个参数
string: 需要转化的字符，如果不是字符串会被转换，忽视空格符。
radix：数字2-36之前的整型。默认使用10，表示十进制。这个参数的意义是指把前面的字符看作是多少进制的数字，所谓的基数。在2-36之外返回NaN
如下所示：
 // 将'123'看作5进制数，返回十进制数38 => 1*5^2 + 2*5^1 + 3*5^0 = 38
parseInt('123', 5)**



Array的方法reduce

传入的函数必须接收两个参数，reduce把结果继续和序列的下一个元素做累积计算

数组只有一个元素直接返回该元素

```javascript
var arr=[1,3,5,7,9]
//求和示例
arr.reduce(function(x,y)
{
    return x+y;
})
```



### filter

filter也是一个常用的操作，它用于把`Array`的某些元素过滤掉，然后返回剩下的元素。

和`map()`类似，`Array`的`filter()`也接收一个函数。和`map()`不同的是，`filter()`把传入的函数依次作用于每个元素，然后根据返回值是`true`还是`false`决定保留还是丢弃该元素。

```javascript
//删掉Array的偶数
var arr = [1, 2, 4, 5, 6, 9, 10, 15];
var r = arr.filter(function (x) {
    return x % 2 !== 0;
});
r; // [1, 5, 9, 15]
```

**传入的回调其实有三个参数，item，index，arr本身**



### sort

直接对当前Array进行修改

正序就是x>y return 1

倒序就是x>y return -1

```javascript
var arr=[10,20,1,2]
arr.sort(function(x,y)
{
    if(x<y)return -1;
    if(x>y)return 1;
    return 0;
})
```



## 闭包

函数作为返回值

**闭包是指有权访问另一个函数作用域中的变量的函数 **

创建闭包的常见方式：在一个函数内部创建另一个函数。

[具体可参考](http://www.cnblogs.com/wangfupeng1988/p/3977924.html)





# Promise

https://www.bilibili.com/video/av27670326/?p=90









> 函数每被调用一次，都会产生一个新的执行上下文环境
>
> 函数在定义的时候（不是调用的时候），就已经确定了函数体内部自由变量的作用域
>
> 作用域中变量的值是在执行过程中产生的确定的，而作用域却是在函数创建时就确定了
>
> 变量取值，要到创建这个函数的那个作用域中取值——是“创建”，而不是“调用”，切记切记



**执行环境、作用域链、活动对象、变量对象**

1. 函数被调用时，会创建一个执行环境以及相应的作用域链，然后使用arguments和其他命名参数的值来初始化函数的活动对象
2. 后台的每个执行环境都有一个表示变量的对象--变量对象；全局环境的变量对象始终存在，函数这样的局部环境的变量对象，只在函数执行的过程中存在









https://www.liaoxuefeng.com/wiki/001434446689867b27157e896e74d51a89c25cc8b43bdb3000/0014351219769203e3fbe1ed611475db3d439393add8997000




