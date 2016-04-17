##先讲讲历史，我跟webpack的渊源

从最开始接触grunt到熟练上手gulp，我经历了差不多有6-9月的时间，这之后就一直熟练的使用gulp做构建，打包等自动化的事情。
中间webpack火起来，当时觉得跟gulp做的是一类的事情，而且gulp满足了自己的工作及学习等使用需求，所以一直没有花时间去仔细了解webpack。
直到。。。

面试各种被问到webpack，巴拉巴拉的，而且确实目前webpack的占有率超级高，所以准备开始拾起webpack来。

**直到目前为止，我还是以为webpack与gulp是差不多的东西，希望能给我惊喜**

1.从官网入手   
[webpack主页](http://webpack.github.io/)

![webpack图解](https://webpack.github.io/assets/what-is-webpack.png)

webpack module bundle,跟这个相似的叫bundle的，之前一直在使用的是browserify。
这么看来，应该说webpack跟browserify更像是一类东西。

- 丰富的Plugin接口，可以支持非常多的插件
- 使用Loaders可以做很多的静态资源预处理
- 代码分块（Code Splitting/chunks），按需加载
- 开发者工具，支持sourceUrl和sourceMap，方便调试
- 性能好，使用异步I/O
- 支持AMD与CommonJs，支持绝大多数现存的类库
- 优化
- 支持除Web外的其他目标环境，如webworkers，node等

##webpack的Code Splitting

webpack的依赖树有两种，同步异步
`require.ensure(deps,callback)`
`require(deps,callback)`
webpack不支持es6 modules


这是到目前为止，看到的webpack最大的亮点，以往使用browserify时，总是将所有的js打包成一个非常大的文件，即使我自己写的功能代码量可能只有几行，倘若我引用了第三方的类库，那么browserify会将所有的直接依赖，以及这些依赖所产生的间接依赖全部打包在一起，就会造成一个源文件几行的代码，打包出来会有超过万行的代码，而且是压缩过后的万行。

如下事例：
```javascript
var webpack = require("webpack");

module.exports = {
  entry: {
    app: "./app.js",
    vendor: ["jquery", "underscore", ...],
  },
  output: {
    filename: "bundle.js"
  },
  plugins: [
    new webpack.optimize.CommonsChunkPlugin(/* chunkName= */"vendor", /* filename= */"vendor.bundle.js")
  ]
};
```
这段配置会产生2个js文件，一个bundle.js包含了app.js的内容，一个vendor.bundle.js包含了所有的vendor

在html页面中引用这两个js文件，注意vendor需要在bundle之前引用。

```html
<script src="vendor.bundle.js"></script>
<script src="bundle.js"></script>
```

看到这里，我觉得官方文档中的这个例子还不是非常的让我信服，怎么说呢，其实在使用gulp+browserify的时候，通过bower管理的第三方的依赖，最终也可以通过gulp的task将所有的依赖提前引用到html当中，其实这个效果应该来说是一样的。

```html
<script src="bower_components/jquery.js"></script>
<script src="bower_components/underscore.js"></script>
<script src="bundle.js"></script>
```


