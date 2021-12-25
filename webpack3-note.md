# 课程准备

## 模块化

### JS 模块化

- 命名空间

  - 库名.类别名.方法名

- CommonJS

  - module.exports
  - require

- AMD / CMD / UMD

  - Async Module Definition
    - 使用 `define` 定义模块
    - 使用 `require` 加载模块
    - 有个著名的库：`RequireJS`
    - 依赖前置，提前执行
    - ![](https://gitee.com/gainmore/imglib/raw/master/img/20210621234642.png)
    - ![](https://gitee.com/gainmore/imglib/raw/master/img/20210621234739.png)
  - Common Module Definition
  - 一个文件为一个模块
  - 使用 `define` 定义一个模块
  - 使用 `require` 加载一个模块
  - 代表作：`SeaJS`
  - 尽可能懒执行
  - ![](https://gitee.com/gainmore/imglib/raw/master/img/20210621235115.png)

- Universal Module Definition

  - 通用解决方案

  - 三个步骤

    - 判断是否支持 AMD
    - 判断是否支持 CommonJS
    - 如果都不支持，使用全局变量
    - ![](https://gitee.com/gainmore/imglib/raw/master/img/20210621235538.png)

    

- ES6 Module

  - 一个文件一个模块
  - 使用 export / import
  - ![](https://gitee.com/gainmore/imglib/raw/master/img/20210622203807.png)
  - ![](https://gitee.com/gainmore/imglib/raw/master/img/20210622204052.png)
  - ![](https://gitee.com/gainmore/imglib/raw/master/img/20210622204103.png)
  - ![](https://gitee.com/gainmore/imglib/raw/master/img/20210622204151.png)

- Webpack 支持

  - AMD( RequireJS )
  - ES Modules（推荐）
  - CommonJS

### CSS 模块化

- CSS 设计模式
  - OOCSS
  - SMACSS
  - Atomic CSS
  - MCSS
  - AMCSS
  - BEM
- CSS Modules

## Webpack 简介

### Webpack 概述

官网：https://webpack.js.org/

中文官网：https://doc.webpack-china.org/

### 大版本变化

![](https://gitee.com/gainmore/imglib/raw/master/img/20210622231436.png)

### 功能进化

![](https://gitee.com/gainmore/imglib/raw/master/img/20210622231517.png)

![](https://gitee.com/gainmore/imglib/raw/master/img/20210622231542.png)

![](https://gitee.com/gainmore/imglib/raw/master/img/20210622231614.png)

### 版本迁移

![](https://gitee.com/gainmore/imglib/raw/master/img/20210622231749.png)

### 参与投票

https://webpack.js.org/vote/

## 核心概念

### Entry

- 代码的入口

- 打包的入口

- 单个或多个

- ```javascript
  module.exports = {
      // 1.写成数组（扩展性差）
      entry: ['index.js', 'vendor.js'],
      // 2.写成对象(推荐)
      entry: {
        index: ['index.js', 'app.js'],
        vendor: 'vendor.js'
  	},
  }
  ```

### Output

- 打包成的文件（bundle）

- 一个或多个

- 自定义规则

- 配合CDN

- ```javascript
  module.exports = {
      entry: {
          index: 'index.js',
          vendor: 'vendor.js'
      },
      output: {
          fileName: '[name].min.[hash:5].js'
      }
  }
  ```

### Loaders

- 处理文件

- 转化为模块

- ```javascript
  module.exports = {
      module: {
          rules: [
              {
                  test: /\.css$/,
                  use: 'css-loader'
              }
          ]
      }
  }
  ```

- 常用 Loader

  - 编译相关
    - babel-loader、ts-loader
  - 样式相关
    - style-loader、css-loader、less-loader、postcss-loader
  - 文件相关
    - file-loader、url-loader

### Plugins

- 参与打包整个过程
- 打包优化和压缩
- 配置编译时的变量
- 非常灵活

### 相关名词

- Chunk
  - 块，代码块
- Bundle
  - 打包
- Module
  - 模块

## 使用Webpack

### 使用Webpack的三种方式

1. Webpack命令
   - `webpack -h` 查看使用命令
   - `webpack -v` 查看版本号
   - `webpack <entry> [<entry>] <output>`  打包
   - 脚手架 `webpack-cli`
     - 交互式的初始化一个项目
     - 迁移项目，低版本 --> 高版本
2. Webpack配置
   - 写好配置文件，直接使用 `webpack` 命令
   - `webpack --config webpack.conf.dev.js`
3. 第三方脚手架
   - Vue-cli
   - Angular-cli
   - React-starter

### 打包JS

打包JS有两种方式：

- 通过命令行：`webpack entry <entry> output`
  - 可以指定多个入口文件
- 通过配置文件
  - `webpack`
    - 此时，配置文件是 `webpack.config.js`，不需要加参数
  - `webpack --config webpack.conf.js`
    - 如果配置文件是其他名称，就需要使用以上命令，指定配置文件

### 编译ES6

#### Babel

- 使用`Babel-loader`编译 `ES6` 语法
- 官方文档：http://babeljs.io
- 安装`Babel`
  - 普通安装：`npm install babel-loader babel-core --save-dev`
  - 安装最新版本：`npm install babel-loader@xxx @babel/core`
  - **这里默认安装的是高版本的babel-loader，所以安装@babel/core（注意名称要一致，否则会报错）：`npm install babel-loader @babel/core --save-dev`**

#### Babel-presets

安装完 `babel`，要使用它，将代码打包成什么样，还需要一套使用的规范，这就需要用到 `bable-presets`了，

`babel-presets` 有很多种，比如：

- es2015
- es2016
- es2017
- env
- babel-preset-react
- babel-preset-stage 0 - 3

这里，使用的是 `env` ，因为这个版本包含了之前的几个版本

**安装：**

- 普通安装：`npm install babel-preset-env --save-dev`
- 高版本安装：`npm install @babel/preset-env --save-dev`
- **由于安装的是高版本babel-loader，所以安装`@babel/preset-env`（注意格式）**

**targets参数：**

- `targets.browsers: "last 2 versions"`
- `targets.browsers: "> 1%"`
- 数据来自 `browserList`，来自 `Can I use`

#### Babel-plugins

不难发现，上面的 `babel-presets`只能转换一些语法，像一些函数和方法根本不会转换，比如：

- `Generator`
- `Set`
- `Map`
- `Array.from`
- `Array.prototype.includes`

所以，为了转换函数和方法，就需要用到两个插件：`Babel Polyfill`和`Babel Runtime Transform`

1. `Babel Polyfill`

   - `polyfill`意为 “垫片”
   - 它可以看作是**全局垫片**，专门为应用准备，会额外创建全局变量导致污染全局
   - 安装：`npm install babel-polyfill --save`
   - 使用：`import 'babel-polyfill'`

2. `Babel Runtime Transform`

   - **局部垫片**，专门为开发框架准备，创建局部变量，不会污染全局环境

   - 安装：`npm install @babel/plugin-transform-runtime --save-dev`

     ​			`npm install @babel/runtime --save`

   - 使用：根目录下创建 `.babelrc` 文件，写入 `json` 格式的配置信息

### 编译typescript

。。。

### 提取公共代码

#### 作用

- 减少代码冗余
- 提高加载速度

利用`webpack`自带的插件`CommonChunkPlugin`，通过`webpack.optimize.CommonsChunkPlugin`调用

#### 配置

```javascript
// webpack.config.js
{
    plugins: [
        new webpack.optimize.CommonsChunkPlugin(o)
    ]
}
```

