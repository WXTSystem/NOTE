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



