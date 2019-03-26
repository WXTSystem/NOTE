# 执行环境

每个执行环境都有一个与之关联的变量对象，环境中定义的所有变量和函数都保存在这个对象中。



# 面向对象

## 数据属性

数据属性有4个描述其行为的特性：

1. configurable：表示能否通过delete删除属性从而重新定义属性，默认true
2. enumerable：表示能否通过for-in循环返回属性，默认为true
3. writable：表示能否修改属性的值，默认true
4. value：包含这个属性的数据值，value特性被设置为指定的值

**要修改默认的特性，必须使用Object.defineProperty()方法，接收三个参数，属性所在对象，属性名字和一个描述符对象（configurable，enumerable，writable，value）**



```javascript
var person={}
Object.defineProperty(person,"name",{
    configurable:false,
    value:"XT"
})
alert(person.name) //XT
delete person.name //返回false，删除属性失败
alert(person.name) //XT
```

<font style='color:red'>注意：1、可以多次调用Object.defineProperty()方法修改同一个属性，但是在把configurable特性设置为false之后就会有限制了，第二次修改该属性就会有限制了，一旦属性定义为不可配置的就不能把它再变回可配置了，再调用Object.defineProperty()方法修改除writable之外的特性，都会导致错误 </font>

<font style='color:red'>2、再调用Object.defineProperty()方法时，如果不指定，configrable、enumerable和writable特性的默认值都是false</font>



## 访问器属性

不包含数据值，包含一对getter和setter函数，可以定义在设置一个值时改变另一个值



读取属性的特性

Object.getOwnPropertyDescriptor()



# 创建对象

## 工厂模式

用函数封装创建对象的细节

```javascript
function createPerson(name,age)
{
    var o=new Object()
    o.name=name
    o.age=age
    return o;
}
```

## 构造函数模式

Object和Array原生构造函数

也可以创建自定义的构造函数，从而定义自定义对象类型的属性和方法

```javascript
//按照惯例，构造函数始终都应该以一个大写字母开头
//而费构造函数则应该以一个小写字母开头
function Person(name,age)
{
    this.name=name;
    this.age=age;
    this.sayName=function()
    {
        alert(this.name)
    }
}
var p1=new Person('wj',1)
```

要创建Person新实例，必须使用new操作符，以这种方式调用构造函数会经历以下4个步骤

1. 创建一个新对象
2. 将构造函数的作用域赋给新对象（this就指向这个新对象）
3. 执行构造函数中的代码
4. 返回新对象

**通过构造函数创建的对象都有一个constructor（构造函数）属性，该属性指向Person**

创建自定义的构造函数意味着将来可以将它的实例标识为一种特定的类型

```javascript
p1 instanceof Object //true,因为所有的对象继承自Object
p1 instanceof Person //true
```



**缺点：每个方法都要在每个实例上重新创建一边，比如上面的sayName()方法，每个对象的该方法都是不同的Function实例**

对上述构造函数改进(会破坏封装性)：

```javascript
function Person(name,age)
{
    this.name=name
    this.age=age
    this.sayName=sayName
}
function sayName()
{
    alert(this.name)
}
```

## 原型模式

每个函数都有一个prototype（原型）属性，指向一个对象

这个对象的用途是包含可以由特定类型的所有实例共享的属性和方法

使用原型对象的好处是可以让所有对象实例共享它所包含的属性和方法



![1548817897164](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1548817897164.png)



Person.prototype指向原型对象，Person.prototype.constructor指回Person。

所有创建的对象内部属性（____proto____）,该属性指向Person.prototype



**hasOwnProperty()只在给定属性存在于对象实例而不是原型中时才会返回true**

### 原型与in操作符

“name” in person1 //不管name属性是实例的还是原型中的，都是true

### 组合使用构造函数模式和原型模式

最常用的

```javascript
function Person(name,age)
{
    this.name=name
    this.age=age
}
Person.prototype=
{
    constructor:Person,
    sayName:function()
    {
        alert(this.name);
    }
}
```

### 动态原型模式

```javascript
function Person(name,age)
{
    this.name=name
    this.age=age
    if(typeof this.sayName!="function")
    {
        Person.prototype.sayName=function()
        {
            alert(this.name)
        }
}
```



# 继承

