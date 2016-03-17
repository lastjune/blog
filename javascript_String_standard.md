#javascript String对象

##在javascript中，其实有二种字符串

- primitive类型的字符串.
- String对象类型的字符串实例

这二者有和区别呢？来看以下代码事例:

```javascript

let primitive_string='This is primitive string.'

let string_obj=new String('This is a string object.');

console.log(typeof primitive_string);//Logs 'string'
console.log(typeof string_obj);      //Logs 'object'

```

**可以发现，他们二者类型不同**

```javascript

s1 = '2 + 2';               // creates a string primitive
s2 = new String('2 + 2');   // creates a String object
console.log(eval(s1));      // returns the number 4
console.log(eval(s2));      // returns the string '2 + 2'

```

**primitive类型的字符串在`eval`中会被当成代码直接类,而object类型的string会被当object处理**

上例代码中，如果需要s2也能达到相同的效果，只需要调用`String.prototype.valueOf`方法

```javascript

s1 = '2 + 2';               // creates a string primitive
s2 = new String('2 + 2');   // creates a String object
console.log(eval(s1));      // returns the number 4
console.log(eval(s2.valueOf()));      // returns the number 4

```

##String对象的静态方法

###String.fromCharCode
根据指定的 Unicode 编码中的序号值来返回一个字符串

>语法
`String.fromCharCode(num1, ..., numN)`
__该方法返回一个primitive字符串__

```javascript

var s1=String.fromCharCode(64,65,66); //Logs '@AB'
console.log(typeof s1); //Logs string

```
>尽管绝大部分常用的Unicode值可以用一个16-bit数字表示（正如 JavaScript 标准化过程早期），并且对于绝大部分值`fromCharCode()`返回一个字符（即对于绝大部分字符 UCS-2 值是 UTF-16 的子集），但是为了处理所有的 Unicode 值（至 21 bits），只用`fromCharCode()`是不足的。由于高位编码字符是用两个低位编码（lower value）表示形成的一个字符，因此`String.fromCodePoint()`（ES6 草案的一部分）被用来返回这样一对低位编码，从而可以完全表示这些高位编码字符。

[unicode编码](https://zh.wikipedia.org/zh-sg/Unicode)


###String.fromCodePoint

[参阅鄙人的翻译](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/String/fromCodePoint)

###String.raw
ES6新特性
>语法
`String.raw(callSite, ...substitutions)`

例子：
```javascript

let name = 'Bob';
String.raw `Hi\n${name}!`;// 'Hi\\nBob!'，内插表达式还可以正常运行

```


##String.prototype 方法

###anchor
`str.anchor(name) `
name参数，制定创建的a标签的name

```javascript

var myString = 'Table of Contents';

document.body.innerHTML = myString.anchor('contents_anchor');

```
output:

```javascript

<a name='contents_anchor'>Table of Contents</a>

```

###big
**deprecated**

###blink
**deprecated**

###bold
**deprecated**

###charAt

返回制定位置的字符
>语法
`str.charAt(index)`
index为字符串位置，从0开始

###charCodeAt

与charAt相似，返回为Unicode
>语法
`str.charCodeAt(index)`
index为字符串位置，从0开始

###codePointAt

ES6中新添加的方法，为了支持charCodeAt不支持的Unicode
**该方法由于浏览器支持情况还不好，不建议在生成环境中使用**

###concat

将一个或多个字符串与原字符串连接合并，形成一个新的字符串并返回
>语法
`str.concat(string2, string3[, ..., stringN])`

```javascript

var hello = 'Hello, ';
console.log(hello.concat('Kevin', ' have a nice day.')); /* Hello, Kevin have a nice day. */

```


###endsWith(该特性处于 ECMAScript 6 规范草案中，目前的实现在未来可能会发生微调，请谨慎使用。)

endsWith()方法用来判断当前字符串是否是以另外一个给定的子字符串“结尾”的，根据判断结果返回 true 或 false。
>语法
`str.endsWith(searchString [, position]);`
参数
-searchString:要搜索的子字符串。
-position:在 str 中搜索 searchString 的结束位置，默认值为 str.length，也就是真正的字符串结尾处。

```javascript

var str = 'To be, or not to be, that is the question.';

alert( str.endsWith('question.') );  // true
alert( str.endsWith('question.',5) );  // false
alert( str.endsWith('to be') );      // false
alert( str.endsWith('to be', 19) );  // true
alert( str.endsWith('To be', 5) );   // true

```

###fixed
**deprecated**

###fontcolor
**deprecated**

###fontsize
**deprecated**

###includes(该特性处于 ECMAScript 6 规范草案中，目前的实现在未来可能会发生微调，请谨慎使用。)

判断一个字符串是否被包含在另一个字符串中,如果是返回true,否则返回false.

>语法
`var contained = str.contains(searchString [, position]);`
参数
-searchString: 将要搜寻的子字符串.
-position:从当前字符串的哪个索引位置开始搜寻子字符串,默认为0.

```javascript

var str = 'To be, or not to be, that is the question.';

console.log(str.contains('To be'));    // true
console.log(str.contains('question')); // true
console.log(str.contains('To be', 1)); // false

```
###indexOf

indexOf() 方法返回指定值在字符串对象中首次出现的位置。从 fromIndex 位置开始查找，如果不存在，则返回 -1。
>语法
`str.indexOf(searchValue[, fromIndex])`
参数
-searchValue:一个字符串表示被查找的值。**区分大小写**
-fromIndex:可选 表示调用该方法的字符串中开始查找的位置。可以是任意整数。默认值为 0。如果 fromIndex < 0 则查找整个字符串（如同传进了 0）。如果 fromIndex >= str.length，则该方法返回 -1，除非被查找的字符串是一个空字符串，此时返回 str.length。

###lastIndexOf

与indexOf功能类似，只是lastIndexOf是从末尾开始匹配

###italics
**deprecated**

###link

创建一个a链接，并且会被存储在`document.links`中
>语法
`str.link(url) `

###localCompare

localeCompare() 方法返回一个数字来表明调用该函数的字符串（reference string）的排列顺序是否在某个给定的字符串的前面或者后面，或者是一样的（编码中的位置）。
>语法
`str.localCompare(compareString[,locals[,options]])`
参数
-compareString:用来比较的字符串
-locals:可选 字符集
-options:可选
>[参考](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/String/localeCompare)


###match

当字符串匹配到正则表达式（regular expression）时，match() 方法会提取匹配项。
获取匹配值返回一个包含匹配项的数组，如果没有匹配，则返回null

>语法
`str.match(regexp);`

###normalize(该特性处于 ECMAScript 6 规范草案中，目前的实现在未来可能会发生微调，请谨慎使用。)

normalize() 方法会按照指定的一种 Unicode 正规形式将当前字符串正规化.
>语法
`str.normalize([form]);`
参数
-form:四种 Unicode 正规形式 "NFC", "NFD", "NFKC", 以及 "NFKD" 其中的一个, 默认值为 "NFC".
        NFC - Normalization Form Canonical Composition.
        NFD - Normalization Form Canonical Decomposition.
        NFKC - Normalization Form Compatibility Composition.
        NFKD - Normalization Form Compatibility Decomposition.

###repeat(该特性处于 ECMAScript 6 规范草案中，目前的实现在未来可能会发生微调，请谨慎使用。)

返回重复count次字符串
>语法
`str.repeat(count)`

###replace

字符串替换，支持正则替换
>语法
`str.replace(regexp|substr,newSubStr|function[,flags])`


###search

正则查找，查找到匹配返回字符串位置下表，没找到返回-1
>语法
`str.search(regexp)`

###slice

按参数从开始处到结束处的位置剪切生成一个新的数组并返回
>语法
`str.slice(beginSlice[, endSlice])`

endSlice如果为负数，则等效于str.length+endSlice

###small
**deprecated**

###split

>语法
`str.split([separator[, limit]])`
参数
-separator:分隔符
-limit:一个整数，限定返回的分割片段数量。split 方法仍然分割每一个匹配的 separator，但是返回的数组只会截取最多 limit 个元素。

###startsWith(该特性处于 ECMAScript 6 规范草案中，目前的实现在未来可能会发生微调，请谨慎使用。)

startsWith()方法用来判断当前字符串是否是以另外一个给定的子字符串“开头”的，根据判断结果返回 true 或 false。
>语法
`str.startsWith(searchString [, position]);`
参数
-searchString:要搜索的字符串
-position:在 str 中搜索 searchString 的开始位置，默认值为 0，也就是真正的字符串开头处。

###strike
**deprecated**

###sub
**deprecated**

###substr

substr() 方法返回字符串中从指定位置开始到指定长度的子字符串。
>语法
`str.substr(start[, length])`
参数
-start:开始位置，可以为负数，若为负数等效于`start+str.length`
-length:截取的长度

###substring

substring() 返回字符串两个索引之间（或到字符串末尾）的子串。
>语法
`str.substring(indexStart[, indexEnd])`
参数
-indexStart:必须大于等于0,开始坐标
-indexEnd:可选，结束坐标

###sup
**deprecated**

###toLocaleLowerCase
转换为本地化的小写

###toLocaleUpperCase
转换为本地化的大写

###toLowerCase
转换为小写

###toUpperCase
转换为大写

###toString

String 对象覆盖了Object 对象的 toString 方法；并没有继承 Object.toString()。对于 String 对象，toString 方法返回该对象的字符串形式，和 String.prototype.valueOf() 方法返回值一样。

###trim
trim() 方法并不影响原字符串本身,它返回的是一个新的字符串.

###trimLeft
移除字符串左端的连续空白符.

###trimRight
移除字符串右端的连续空白符.


###valueOf

###[@@iterator]

>语法
`string[Symbol.iterator]`
```javascript

var string = 'A\uD835\uDC68';

var strIter = string[Symbol.iterator]();

console.log(strIter.next().value); // "A"
console.log(strIter.next().value); // "\uD835\uDC68"

```

###toSource
该特性是非标准的，请尽量不要在生产环境中使用它！
