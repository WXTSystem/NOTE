# 基本概念





# webpack-dev-server

设置好之后，可以实现修改代码之后不需要重新运行webpack打包，直接自动重新生成



1. --open

   运行后，自动打开浏览器

2. --port

   指定端口

3. --contentBase

   默认打开文件路径

4. --hot

   + 更新局部代码之后不会全部重新生成，只会生成修改部分代码，相当于打个补丁
   + 添加后，更改样式页面无需刷新即可看出改变之后的样式



## 配置方式1

在package.json对应script之后直接加上参数

```json
{
  "name": "day01",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "dev":"webpack-dev-server --open --port 8080 --contentBase dist --hot"
  },
  "keywords": [],
  "author": "",
  "license": "ISC",
  "devDependencies": {
    "webpack": "^4.29.6",
    "webpack-cli": "^3.3.0",
    "webpack-dev-server": "^3.2.1"
  },
  "dependencies": {
    "jquery": "^3.3.1"
  }
}

```

## 配置方式2

在webpack.config.js中添加devServer节点

```javascript
const path=require('path')

module.exports={
    entry:'./src/index.js',
    output:
    {
        path:path.join(__dirname,'./dist'),
        filename:'bundle.js'
    },
    devServer:
    {
        open:true,
        port:8080,
        contentBase:'dist',
        hot:true
    }

}
```



# html-webpack-plugin

会根据配置的template在内存中生成自动引用script css的html文件

```javascript
const path=require('path')

const htmlWebpackPlugin=require('html-webpack-plugin')

module.exports={
    entry:'./src/index.js',
    output:
    {
        path:path.join(__dirname,'./dist'),
        filename:'bundle.js'
    },
    plugins:[
        new htmlWebpackPlugin({
            template:path.join(__dirname+'./dist/index.html'), //根据哪个文件生成html
            filename:'index123.html' //生成的文件名
        })
    ]

}
```



# loader

通过配置module下的rules，添加针对不同文件类型处理的loader

loader是从右往左开始解析的

css-loader style-loader  

还有less-loader（要先装less）

sass-loader（需要安装node-sass）

file-loader（图片等资源） url-loader

npm i url-loader file-loader -D

   **url-loader和file-loader是什么关系呢？简答地说，url-loader封装了file-loader。url-loader不依赖于file-loader，即使用url-loader时，只需要安装url-loader即可，不需要安装file-loader，因为url-loader内置了file-loader。通过上面的介绍，我们可以看到，url-loader工作分两种情况：1.文件大小小于limit参数，url-loader将会把文件转为DataURL；2.文件大小大于limit，url-loader会调用file-loader进行处理，参数也会直接传给file-loader。因此我们只需要安装url-loader即可。**





```javascript
const path=require('path')

module.exports={
    entry:'./src/index.js',
    output:
    {
        path:path.join(__dirname,'./dist'),
        filename:'bundle.js'
    },
    module:{
        rules:[
            {
                test:/\.css$/,
                use:['style-loader','css-loader']
            },
           {
                test:/\.png$/,
                use:['url-loader?limit=7631&name=[hash:8]-[name].[ext]'] //通过设置limit指定图片小于多少时会被转为base64编码，name指定生成图片名称
            }
        ]
    }

}
```



# 转换高级ES6语法，Babel

**Babel 是一个 JavaScript 编译器**

https://www.babeljs.cn/

1. 安装babel-core babel-loader babel-plugin-transform-runtime

2. 安装babel-preset-env babel-preset-stage-0

3. webpack配置文件中添加rule解析js文件，并排除node_modules中的文件

   ```javascript
   {test:/\.js$/,use:'babel-loader',exclude:/node_modules/}
   ```

4. 在项目根目录下新建.babelrc配置文件，内容满足json格式

   ```json
   {
       "presets":["env","stage-0"],
       "plugins":["transform-runtime"]
   }
   ```

   

   ## 示例

   ```javascript
   //要解析如下ES6语法，实际开发及配置如下
   class Person
   {
       static info = { name:'wj',age:1 }
   }
   
   console.log(Person.info)
   ```

   

   实际开发如下配置，具体参考https://webpack.js.org/loaders/babel-loader#repo-httpsgithubcombabelbabel-loader

   加百度

   ```javascript
   //安装所需 npm install -D babel-loader @babel/core @babel/preset-env 
   "devDependencies": {
       "@babel/core": "^7.4.0",
       "@babel/plugin-proposal-class-properties": "^7.4.0",
       "@babel/preset-env": "^7.4.2",
       "babel-loader": "^8.0.5",
    }
   //安装ES6新语法支持Class plugin-proposal-class-properties
   //npm install -D plugin-proposal-class-properties
   //在webpack配置文件中module中配置如下
   {
                   test:/\.js$/,
                   exclude:/node_modules/,
                   use:{
                       loader:'babel-loader',
                       options:{
                           plugins: [
                               [
                                 "@babel/plugin-proposal-class-properties",
                                 {
                                   "legacy": true
                                 }
                               ]
                             ],
                           presets: ['@babel/preset-env']
                       }
                   }
   }
       
   ```

   

https://www.bilibili.com/video/av36650577/?p=106