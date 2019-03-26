NPM是随同NodeJS一起安装的包管理工具，能解决NodeJS代码部署上的很多问题，常见的使用场景有以下几种：

- 允许用户从NPM服务器下载别人编写的第三方包到本地使用。

- 允许用户从NPM服务器下载并安装别人编写的命令行程序到本地使用。

- 允许用户将自己编写的包或命令行程序上传到NPM服务器供别人使用。

  

# npm init -y

初始化一个项目



# package.json

- **name** - 包名。
- **version** - 包的版本号。
- **description** - 包的描述。
- **homepage** - 包的官网 url 。
- **author** - 包的作者姓名。
- **contributors** - 包的其他贡献者姓名。
- **dependencies** - 依赖包列表。如果依赖包没有安装，npm 会自动将依赖包安装在 node_module 目录下。
- **repository** - 包代码存放的地方的类型，可以是 git 或 svn，git 可在 Github 上。
- **main** - main 字段指定了程序的主入口文件，require('moduleName') 就会加载这个文件。这个字段的默认值是模块根目录下面的 index.js。
- **keywords** - 关键字



# npm install和npm uninstall、npm update

安装模块npm install

卸载模块npm uninstall express

更新模块npm update express

搜索模块npm search express



1. 查看已安装的模块

   npm list -g //查看全局

2. 查看某个模块的版本号

   npm list grunt



## 全局安装

npm install express -g

- 1. 将安装包放在 /usr/local 下或者你 node 的安装目录。
- 2. 可以直接在命令行里使用。

## 本地安装

npm install express

- 1. 将安装包放在 ./node_modules 下（运行 npm 命令时所在的目录），如果没有 node_modules 目录，会在当前执行 npm 命令的目录下生成 node_modules 目录。
- 2. 可以通过 require() 来引入本地安装的包。



# npx

npx 想要解决的主要问题，就是调用项目内部安装的模块

npx 会帮你执行依赖包里的二进制文件



# npm脚本（NPM Scripts）

```json
//在package.json文件里面，使用scripts字段定义脚本命令

{
  "name": "jsdemo",
  "version": "1.0.0",
  "description": "",
  "private": true,
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "build":"webpack"
  },
  "devDependencies": {
    "webpack": "^4.29.6",
    "webpack-cli": "^3.3.0"
  },
  "dependencies": {
    "lodash": "^4.17.11"
  }
}

//添加脚本后，使用npm run命令，就可以执行这段脚本
npm run build
```



# npm install --save和npm install --save-dev

*在安装一个要打包到生产环境的安装包时，你应该使用* `npm install --save`*，如果你在安装一个用于开发环境的安装包（例如，linter, 测试库等），你应该使用* `npm install --save-dev`*。请在* [npm 文档](https://docs.npmjs.com/cli/install) *中查找更多信息。*



