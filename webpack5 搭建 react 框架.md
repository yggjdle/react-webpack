# webpack5 搭建 react 框架

## 初始化项目

### 新建项目 创建package.json

```
npm init -y
```



### 安装webpack（模块打包库）和webpack-cli（命令行工具）

```
npm i -D webpack webpack-cli
```

-` -D`是`--save-dev`的简写，仅在开发环境才用的包，会被注册在package.json里的`devDependencies`里
-` -S`是`--save`的简写，会打包到生成的包里面，是发布内容的一部分，会被注册在package.json里的`dependencies`里

### 创建项目入口文件 src/index.js

## 基础配置

### 创建webpack配置文件 webpack.config.js 

设置entry（入口）& output（出口）

```
const path = require('path');

module.exports = {
    entry: {
        index: path.resolve(__dirname, 'src/index.js'),
    },
    output: {
        path: path.resolve(__dirname, 'dist'),
        filename: '[name].js',
        clean: true, //每次打包前清空目录
    },
};

```

### 添加构建命令，在package.json中的script添加build命令

```
 "scripts": {
    "build": "webpack --config webpack.config.js"
  },
```

运行npm run build，检测是否打包成功。如果生成dist/index.js文件，就说明成功啦！

### html-webpack-plugin（插件引入）

去查看打包后的dist发现其中只有js的文件，为了展示js，还需要有index.html。可以在dist目录下手写index.html，但是开启了clean模式，每次都要要重新写，所以可以引入html-webpack-plugin插件来结局

### 安装

```
npm i html-webpack-plugin -D
```

### 在webpack.config.js中添加plugins

```
plugins: [
    new HtmlWebpackPlugin({
        template: path.resolve(__dirname, './index.html'),
        filename: 'index.html'
    })
]
```

