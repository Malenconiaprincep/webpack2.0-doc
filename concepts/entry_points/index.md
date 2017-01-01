# 入口点

像前面我们提到的介绍，有多种方式去定义__entry__属性在你的webpack配置里。我们将把这些方法展现，你可以配置__entry__属性，并额外的解释它为什么对你用。

# 单一入口

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


# 对象

