#使用Array.prototype.slice.apply(arguments)转换arguments为数组会造成javascript引擎（例如V8引擎）的优化出现问题

通常在方法内部，习惯性的通过以下代码将arguments转换为数组，因为数组操作更加方便便利，有很多原生的方法可以使用

```javascript

var printParams=(a,b,c)=>{
    var args=Array.prototype.slice.apply(arguments);
    args.map(v=>{
        console.log(v);
    });
}
printParams(1,2,3);

```

今天在[MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/arguments)上查看arguments时，发现上面提到，使用这种方式来转换arguments会使javascript引擎的优化器放弃对当前方法的优化，具体的介绍信息来自这篇文章[Optimization killers](https://github.com/petkaantonov/bluebird/wiki/Optimization-killers#3-managing-arguments)。

一种替代方案的代码如下

```javascript

var printParams=(a,b,c)=>{
    var args = (arguments.length === 1 ? [arguments[0]] : Array.apply(null, arguments));
    args.map(v=>{
        console.log(v);
    });
}
printParams(1,2,3);

```

新技能get:white_check_mark:

在[Optimization killers](https://github.com/petkaantonov/bluebird/wiki/Optimization-killers#3-managing-arguments)里提到的其他一些killers，留待下次学习。

