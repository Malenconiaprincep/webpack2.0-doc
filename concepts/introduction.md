# 概念

webpack是现代JavaScript应用程序模块打包机。虽然它的配置极其复杂，但无论怎么样在开始之前你应该去理解四个核心的概念。

作为webpack学习旅程的一部分，我们写这个文档的目的是给你一个高度概括的这些概念,同时还提供链接到特定的用例概念。

# 入口

webpack在你的应用依赖里创建了一个图。这张图的起点被称为一个入口点。入口点告诉我们webpack从哪里开始和遵循图知道包的依赖关系。你可以考虑你的应用的入口点作为上下文的根或者第一个启动APP的文件。

在webpack里我们定义了入口点使用 _entry_ 属性在我们的 webpack配置里

下面有个简单的例子

webpack.config.js

```
module.exports = {
entry : './path/to/my/entry/file.js'
};
```

有多种方式去声明你的 _entry_ 属性根据你的应用程序的需求来定。



Learn more!

# 输出

你已经把全部的资源打包了，我们仍然需要告诉webpack打包我们的应用程序。webpack的 _output_ 属性就是告诉webpack怎样去处理打包的代码

webpack.config.js

```
var path = require('path');

module.exports = {
entry: './path/to/my/entry/file.js',
output: {
path: path.resolve(__dirname, 'dist'),
filename: 'my-first-webpack.bundle.js'
}
};
```

在上面的例子中，通过`output.filename` 和 `output.path`属性描述了我们生成文件的包名和路径。

`output` 属性有很多特性，让我们花费时间去理解更多通用的例子。



Learn more!

# 加载器

资源的目标是在你的项目需要webpack关心的而不是浏览器。\(这并不意味着他们不得不全部打包在一起\)。webpack处理每种文（_.css,.html,.scss,.jpg,etc._）作为一个模块，无论如何，webpack仅仅是理解Javascript。

加载器在webpack里转换这些文件是需要通过你所添加的依赖模块。

在高级别上，他们有两个目标在你的webpack配置上。

1.识别这些应该被转换的确定加载器。（_**test**_属性）
2.转换这些文件，以便它可以添加到你的依赖图里（并且最终在你的包里）。\(_**use**_属性\)

webpack.config.js

```
var path = require('path');

const config = {
entry: './path/to/my/entry/file.js',
output: {
path: path.resolve(__dirname, 'dist'),
filename: 'my-first-webpack.bundle.js'
},
module: {
rules: [
{test: /\.(js|jsx)$/, use: 'babel-loader'}
]
}
};
```

在上面的这个配置里我们已经定义了一个 _rules_ 属性代表是一个单一的模块并且需要两个属性：_test_和 _use_。告诉webpack按照这个来编译

_"webpack编译者，当你遇到用_`require/import`_声明后缀为'**.js**'或者'**.jsx**'的文件时，你需要用 _`babel-loader`_ 在打包之前去转换"_。

加载器会有更多具体的属性去定义，我们并没有完全覆盖这些内容。



Learn more!

# 插件

由于加载器只在上面的基础上执行转换, `plugins`是最常用的（但不限于）执行操作和自定义函数在“编译”或者“块”在你的包模块上（更多）。webpack插件系统非常强大和可自定义的。

为了用一个插件，你需要用`require()` 并且增加到`plugins`数组里。更多的插件通过选项可自定义的。你可以多次使用一个插件配置为不同的目的，创建一个新的实例需要用`new`。

webpack.config.js

```
const HtmlWebpackPlugin = require('html-webpack-plugin'); //installed via npm
const webpack = require('webpack'); //to access built-in plugins

const config = {
entry: './path/to/my/entry/file.js',
output: {
filename: 'my-first-webpack.bundle.js',
path: './dist'
},
module: {
rules: [
{test: /\.(js|jsx)$/, use: 'babel-loader'}
]
},
plugins: [
new webpack.optimize.UglifyJsPlugin(),
new HtmlWebpackPlugin({template: './src/index.html'})
]
};

module.exports = config;
```

webpack提供了许多插件！你可以从这里看到我们的插件列表。

在webpack中使用插件配置简单,然而有许多用例值得进一步讨论。



Learn more!