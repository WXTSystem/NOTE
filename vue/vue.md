### v-cloak

### v-text

### v-html

### v-bind:和：，绑定属性的，v-bind中可以放合法的js表达式，单向绑定m->v

### v-on，v-on:可以用@替换

### 事件修饰符

> stop
>
> prevent
>
> capture
>
> self
>
> once

### v-model双向绑定,v-model 只能用在表单元素中，双向绑定

### vue使用样式

thin\italic为style内定义的类样式

*  v-bind: <h1 :class="['thin','italic']">
* 在数组里使用三元表达式:class="['thin','italic',flag?:'active':'']"//flag为data里的数据
* 在数组里使用三元表达式:class="['thin','italic',{'active':flag}]"
* class直接绑定对象 :class="{red:true,thin:true}"

内联样式

- :style="{}"//直接写样式内容，或者绑定一个样式对象
- :style="[obj1,obj2]"//使用数组绑定多个样式对象

### v-for和key

遍历数组v-for <p v-for="(user,i) in list">i:{{user.id}}</p>

+ 遍历数组

+ 遍历对象

+ v-for="count int 10"     第{{count}}次循环

  

  ### v-if和v-show

v-if每次都会创建或者删除元素 v-show每次隐藏或者显示元素

### 过滤器

用作一些常见的文本格式化，只能用在mustach和v-bind

+ 定义全局过滤器Vue.filter('filtername',funtion(data){})
+ 定义私有过滤器 在Vue对象中data同级添加filters:{dataFormat:function(data){}}

调用的时候{{name|filtername}}

接收多个参数

**可以调用多个过滤器{{name | filter1 | fileter2}}**

### 按键事件

+ 回车@keyup.enter="add()"

+ 其他按键修饰符tab，delete,esc,space,up,down,left,right

+ 其他的通过键盘码 @keyup.113="add()" //f2按键对应113

+ [键盘码]:https://www.cnblogs.com/cnblogs-jcy/p/6409672.html

+ 自定义按键修饰符Vue.config.keyCodes.f2=113;  就可以使用@keyup.f2

### 定义全局指令

```javascript
//在定义时不要加v-，在使用时使用v-focus
Vue.directive('focus',{
    bind:function(el){},//每当指令绑定到元素上的时候，会立即执行bind函数，只执行一次，注意对el操作时，必须在dom加载完毕之后才能起作用
    inserted:function(el){},//el被插入到dom中的时候执行，触发一次
    updated:function(el){}//VNode更新的时候执行
    //第一个参数都是原生dom对象
});

/////////////样式相关的写在bind中，行为相关的写在inserted中
```

### 定义私有指令

在Vue对象下添加directives:

```javascript
Vue({
    //...
    directives:{
        'fontdirec':{
            bind:function(el,binding){
                //el.style.....
            },
            'fontsize':function(el,binding){
                //简写，相当于把代码写到bind和update中去了
                
            }
        }
    }
})
```

### Vue实例生命周期

1. beforeCreate,在beforeCreate执行的时候，data和methods对象均还没有初始化
2. created,data和methods均已被初始化
3. beforeMount 表示模板已经编译完成，但尚未渲染到页面DOM中
4. mounted表示内存中的模板已经真实的挂载到了页面中
5. data改变
   + beforeUpdate
   + updated
6. beforeDestroy //执行销毁过程时，beforeDestroy中实例身上的所有data、methods、filter等都处于可用状态
7. destroyed

```javascript
var vm=new Vue({
    data:{},
    methods:{},
    brforeCreate(){},
    created(){}
})
```

### ajax请求

**现在都用axios了**

vue-resource和axios

get post 和jsonp请求（http://www.cnblogs.com/lijinblogs/p/5782502.html）

this.$http.get(url,{options})

this.$http.post(url,{body},{options})

this.$http.jsonp(url,{options})

### 动画

分为进入和离开

v-enter v-enter-to v-enter-active

v-leave v-leave-to v-leave-active

+ 使用transition把需要被动画控制的元素包裹起来
+ 建立两组样式v-enter,v-leave-to和v-enter-active,v-leave-active

可以给transition加name，对应动画样式就是name-enter...

**使用animate.css第三方类库实现动画样式**

半程动画查看transition钩子函数

动画参考https://www.bilibili.com/video/av36650577/?p=53

### 组件

```javascript
//注意 template只能有一个根元素

//Vue.extend创建组件
var com1=Vue.extend({
    template:'<h1>这是组件模板</h1>'
})
Vue.component('myCom1',com1)//第一个参数为组件名

//如果组件名使用驼峰格式aaBcc  则html中用<aa-bcc>调用
//如果没有使用驼峰 aabbc 则直接<aabbc>
//在页面中直接使用<my-com1></my-com1>引用自定义的组件


//第二种创建方式
Vue.component('mycon1',{template:'<h1>组件模板</h1>'})

//第三种 template内容写在template标签之内，template标签必须写在被Vue控制的元素之外
//<template><div><h1>12345</h1></div></template>
Vue.component('mycom1',{template:"#temp1"})

//可以定义私有组件
var vm=new Vue({
    el:"#app",
    data:{},
    methods:{},
    components:{
        login:{template:'<h1>私有h1组件</h1>'}
    }
})
 

/////组件可以有methods，组件也可以有data，但是data必须是一个function且返回一个Object
Vue.component('mycom3',{
    template:"#tmpl1",
    data:function(){
        return {msg:'Hello World'}
    }
})


//定义组件代码要写在new Vue上面？？？？？？
//而且使用时要写在Vue控制的元素内
```

Vue提供了component元素，放置指定组件

```html
<component :is="comname"></component>
<!--vue会用is绑定的组件名称对应组件去替换component-->
```

### Vue提供的元素总结template component transition transitionGroup



### 父子组件传值关系

子组件默认不能读取父组件的数据

```javascript
var vm=new Vue({
    el:"#app",
    data:{msg:'hello world'},
    components:{
        hello:{
            template:'<h1>11{{parentmsg}}</h1>',
            data:function(){
                return {a:'1'}
            }
            props:['parentmsg']
        }
    }
});
//<hello :parentmsg="msg"></hello>

//子组件必须在自身props数组中添加属性名字符串，在<hello>标签中通过绑定值
//:属性名="父组件中的数据"传值



//获取父组件的function
var vm=new Vue({
    
    el:"#app",
    methods:{
        show(data){
            console.log('parent log'+data)
        }
    },
    components:{
        hello:{
            template:'#child',
            methods:{
                callparent(){
                    this.$emit('func','123')
                }
            }
        }
    }
})

//通过事件绑定传递show到fun，在子组件方法中通过this.$emit('func')调用父组件方法
//<hello @func='show'></show>
////////通过调用父组件方法可以把子组件数据传递给父组件
```



### vue获取dom对象

Vue对象上有个$refs属性，当在html中将制定元素使用ref='refname'标记之后，就可以使用$refs.refname获取到指定dom元素

this.$refs.refname

**自定义组件也可以通过ref来引用，进而可以访问子组件的data和方法**

### 路由

参考：http://www.cnblogs.com/joyho/articles/4430148.html

前端路由，hash路径 #，不会发送http请求

引入vue-router必须在引入vue之后

```javascript
var login={
    template:'<h1>登录</h1>'
}
var register={
    template:'<h1>注册</h1>'
}

var routerObj=new VueRouter({
    routes:[
        {path:'/',redirect:'/login'},
        {path:'/login',component:login},
        {path:'register',component:register}
    ]
});
var vm=new Vue({
    //....
    router:routerObj
})

//<router-view></router-view>页面中使用该标签作为占位符，url变化时，使用指定组件替换router-view

//<a href="#/login"></a>
//或者使用<router-link to='/login'>登录</router-link>
//vue默认会将它渲染为a标签
//加tag='span'最终会渲染为sapn标签

///////设置router-link-active类样式来改变选中时router-link样式


//在组件内部可以通过 path  query为参数
传参方式1
    <router-link to='/login?id=1'>  this.$route.query.id

传参方式2，在path中定义参数格式
{path:'/login/:id'}
<router-link to='/login/1'>
    this.$route.params.id路由
```



### 路由的嵌套

```javascript
var router=new VueRouter({
    routes:[
        {
            path:'/',
            component:account,
            children:[
                {path:'login',component:login}
            ]
        }
    ]
})
//通过children添加路由嵌套
```



### 路由通过name对应组件



```javascript
//<router-view name='left'><router-view>
//<router-view name='main'><router-view>
//请求路径为/根路径时，name为left的router-view区域填充left组件
var router=new VueRouter({
    routes:[
        {
            path:'/',
            components:{
                'header':header,
                'left':left,
                'main':main
            }
        }
    ]
})
```



### watch

使用这个属性，可以监视data中指定数据的变化，然后触发这个watch

中对应的function函数

```javascript
var vm=new Vue({
    el:"#app",
    data:{
        firstname:''
    },
    watch:
    {
        //firstname变化时就会触发该事件，属性名有-时必须加'' 
        firstname:function(newVal,oldVal)
        {
            
        }
    }
})
```

### 监听路由的变化

```javascript
watch:{
    '$route.path':function(newVal,oldVal){
        
    }
}
```



### computed

```javascript
computed:{
    //在computed中，可以定义一些属性，这些属性，叫做计算属性，本质是一个方法，只不过我们在使用这些计算属性的时候，是把他们的名称，直接当做属性来使用的，并不会把计算属性当做方法去调用
    'fullname':function()
    {
        return this.name+"-"
    }
}

//注意1：计算属性，引用的时候，不要加()去调用，直接把它当做普通属性去使用
//注意2：只要计算属性这个function内部，所用到的任何data中的数据发生了变化，就会立即重新计算这个计算属性的值
//注意3：计算属性的求值结果，会被缓存起来，方便下次直接使用；如果计算属性方法中，所引用的任何数据都没有发生变化，则不会重新计算
```





### nrm

安装nrm  npm i nrm -g

nrm ls查看镜像列表

nrm use npm选择镜像地址





# WebPack















https://www.bilibili.com/video/av36650577/?p=97