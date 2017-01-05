# 入口点

像前面我们提到的介绍，有多种方式去定义__entry__属性在你的webpack配置里。我们将把这些方法展现，你可以配置__entry__属性，并额外的解释它为什么对你用。

# <span id="single">单一入口</span>

用法：```entry: string|Array<string>```

webpack.config.js

```
const config = {
  entry: './path/to/my/entry/file.js'
};

module.exports = config;
```

这就是单个入口的语法通过 __entry__ 属性

```
const config = {
  entry: {
    main: './path/to/my/entry/file.js'
  }
};
```

那我们什么时候entry是传一个数组呢？传一个数组文件路径给__entry__属性被称为__multi-main entry__。当你去注入多个依赖文件在一起并且把它们的依赖变成一个块。

这是一个很好的选择,当你想快速设置webpack配置为应用程序或工具有一个入口点。无论怎么样，这不是一个很好扩展你配置的语法。


# <span id="object">对象</span>

用法: entry: {[entryChunkName: string]: string|Array<string>}

webpack.config.js

```
const config = {
  entry: {
    app: './src/app.js',
    vendors: './src/vendors.js'
  }
};
```

对象语法更加冗长，但是却能更好的扩展去定义入口在你的配置里



**可伸缩的webpack配置是可以被复用和结合其它的配置。这是一个受欢迎的技术用于分离问题的环境中,构建和执行。通常用webpack-merge 来进行合并。**


# <span id="scenarios">场景</span>

下面是一些真实的实际使用例子：

#### App与Vendor入口文件分离：

webpack.config.js

```
const config = {
  entry: {
    app: './src/app.js',
    vendors: './src/vendors.js'
  }
};
```

这是做什么？这里告诉我们webpack创建依赖图标是需要 app.js 和 vendor.js的。这些图是完全独立的,相互独立的（它们每个将被打包）。这里通常被看成单页应用的一个入口文件（不包括vendors）。

为什么呢？这一步允许你去利用 `CommonsChunkPlugin` 并且抽出任何vendor引用从你的app包到你的vendor包，用`__webpack_require__()`。如果没有vendor代码在你的应用代码里，然后你可以获取一个通用模式在webpack被叫做**long-term vendor-caching**。


#### 多个页面应用：

webpack.config.js

```
const config = {
  entry: {
    pageOne: './src/pageOne/index.js',
    pageTwo: './src/pageTwo/index.js',
    pageThree: './src/pageThree/index.js'
  }
};
```

这是做什么？我们正告诉你像这样去分离3个图标。

为什么呢？在多个页面应用，服务端正去获取新的HTML文档。这些页面重新加载新的文档和资源会被重新下载。无论如何，这些给了我们唯一的机会去这些：

· 用 `CommonsChunkPlugin` 使每个页面中共享的代码去打包。多页面应用程序/模块重用很多代码入口点之间可以大大受益于这些技术,作为入口点的数量增加。




