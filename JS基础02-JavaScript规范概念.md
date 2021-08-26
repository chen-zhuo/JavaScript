# JavaScript规范概念

## JavaScript规范

**JavaScript 遵循 ECMA-262 规范，目前其最新版是 ECMAScript 2018，而获得所有主流浏览器完全支持的则是 ECMAScript 5。**以ECMAScript 5版本为基础，兼顾 ECMAScript 6 版本中获得较大支持的新特性进行介绍。

### 基本词法

JavaScript 语法就是指构成合法的 JavaScript 程序的所有规则和特征的集合，包括词法和句法。简单描述如下：

- **词法定义了 JavaScript的基本名词规范，包括字符编码、命名规则、标识符、关键字、注释规则、 运算符和分隔符等。**
- **句法定义了 JavaScript的基本运算逻辑和程序结构，包括短语、句子和代码段的基本规则，如表达式、语句和程序结构等。**

### 区分大小写

**JavaScript 严格区分大小写。为了避免输入混乱和语法错误，建议采用小写字符编写代码**。在以下特殊情况下可以使用大写形式：

**1) 构造函数的首字母建议大写。**下面调用预定义的构造函数 Date()，创建一个时间对象，然后把时间对象转换为字符串显示出来。

```javascript
d = new Date();  //获取当前日期和时间
document.write(d.toString());  // 显示日期
```

**2) 标识符由多个单词组成可以使用骆驼命名法——除首个单词外，后面单词的首字母大写。**

```javascript
typeOf();
printEmployeePaychecks();
```

提示：
上述都是约定俗成的一般习惯，不构成强制性要求，用户可以根据个人习惯进行命名。

### 直接量

**直接量（Literal）就是具体的值，即能够直接参与运算或显示的值，如字符串、数值、布尔值、正则表达式、对象直接量、数组直接量、函数直接量等。**
下面示例分别定义不同类型的直接量：字符串、数值、布尔值、正则表达式、特殊值、对象、数组和函数。

```javascript
//空字符串直接量
1  //数值直接量
true  //布尔值直接量
/a/g  //正则表达式直接量
null  //特殊值直接量
{}  //空对象直接量
[]  //空数组直接量
function(){}  //空函数直接量，也就是函数表达式
```

### 转义序列

**转义序列就是字符的一种表示方式（映射）**。由于各种原因，很多字符无法直接在代码中输入或输出，只能通过转义序列间接表示。

- Unicode 转义序列方法：\u + 4位十六进制数字。
- Latin-1 转义序列方法：\x + 2位十六进制数字。

对于字符“©” , Unicode 转义为 \u00A9，ASCII 转义为 \xA9。

```javascript
document.write("\xa9");  //显示字符©
document.write("\u00a9");  //显示字符©
```

### 字符编码

**JavaScript 遵循 Unicode 字符编码规则。Unicode 字符集中每个字符使用 2 个字节来表示，这意味着用户可以使用中文来命名 JavaScript 变量。**

**Unicode 是 Latin-1 字符集的超集，编码数目达到百万级；Latin-1是 ASCII 字符集的扩展，包含 256 个拉丁字母； ASCII 字符集包含 128 个基本字符，即常用英文字母和符号。**

!> 考虑到 JavaScript 版本的兼容性以及开发习惯，不建议使用双字节的中文字符命名变量或函数名。

?> 由于 JavaScript 脚本一般都嵌入在网页中，并最终由浏览器来解释，因此在考虑到 JavaScript 字符编码的同时， 还要兼顾 HTML 文档的字符编码，以及浏览器支持的编码。一般建议保持 HTML 文档的字符编码与 JavaScript 字符编码一致，以免出现乱码。

## JavaScript概念

### 标识符

**JavaScript 标识符包括变量名、函数名、参数名和属性名。**合法的标识符应该注意以下强制规则：

- 第一个字符必须是字母、下划线（_）或美元符号（$）。
- 除了第一个字符外，其他位置可以使用 Unicode 字符。一般建议仅使用 ASCII 编码的字母，不建议使用双字节的字符。
- 不能与 JavaScript 关键字、保留字重名。
- 可以使用 Unicode 转义序列。例如，字符 a 可以使用“\u0061”表示。

在下面示例中，定义变量 a，使用 Unicode 转义序列表示变量名：

```javascript
var \u0061 = "字符 a 的 Unicode 转义序列是 \\0061";
document.write(\u0061);
```

?> 使用转义序列不是很方便，一般常用转义序列表示特殊字符或名称，如 JavaScript 关键字、程序脚本等。

### 关键字

**关键字**就是 ECMA-262 规定的 JavaScript 语言内部使用的一组名称（或称为命令）。这些名称具有特定的用途，用户不能自定义同名的标识符。具体说明如表所示。

| 关键字   | 关键字   | 关键字     | 关键字 | 关键字 |
| -------- | -------- | ---------- | ------ | ------ |
| break    | delete   | if         | this   | while  |
| case     | do       | in         | throw  | with   |
| catch    | else     | instanceof | try    |        |
| continue | finally  | new        | typeof |        |
| debugger | for      | return     | var    |        |
| default  | function | switch     | void   |        |

### 保留字

**保留字**就是 ECMA-262 规定的 JavaScript 语言内部预备使用的一组名称（或称为命令）。这些名称目前还没有具体的用途，是为 JavaScript 升级版本预留备用的，建议用户不要使用。具体说明如表所示。

| 关键字   | 关键字  | 关键字     | 关键字    | 关键字       |
| -------- | ------- | ---------- | --------- | ------------ |
| abstract | double  | goto       | native    | static       |
| boolean  | enum    | implements | package   | super        |
| byte     | export  | import     | private   | synchronized |
| char     | extends | int        | protected | throws       |
| class    | final   | interface  | public    | transient    |
| const    | float   | long       | short     | volatile     |

在非严格模式下，仅规定 class、const、enums、export、extends、import、super 为保留字，其他 ECMAScript 3 保留字可以自由使用；在严格模式下，ECMAScript 5 变得更加谨慎，严格限制 implements、interface、let、package、private、protected、public、static、yield、eval（非保留字）、arguments（非保留字）的使用。

JavaScript 预定义了很多全局变量和函数，用户也应该避免使用它们。具体说明如表所示。

| 预定义             | 预定义             | 预定义   | 预定义         | 预定义      |
| ------------------ | ------------------ | -------- | -------------- | ----------- |
| arguments          | encodeURL          | Infinity | Number         | RegExp      |
| Array              | encodeURLComponent | isFinite | Object         | String      |
| Boolean            | Error              | isNaN    | parseFloat     | SyntaxError |
| Date               | eval               | JSON     | parseInt       | TypeError   |
| decodeURL          | EvalError          | Math     | RangeError     | undefined   |
| decodeURLComponent | Function           | NaN      | ReferenceError | URLError    |

不同的 JavaScript 运行环境都会预定义一些全局变量和函数，上表列出的仅针对 Web 浏览器运行环境。

### 分隔符

**分隔符（空白符）就是各种不可见字符的集合，如空格（\u0020）**、水平制表符（\u0009）、垂直制表符（\u000B）、换页符（\u000C）、不中断空白（\u00A0）、字节序标记（\uFEFF）、换行符（\u000A）、 回车符（\u000D）、行分隔符（\u2028）、段分隔符（\u2029）等。

**在 JavaScript 中，分隔符不被解析，主要用来分隔各种记号，如标识符、关键字、直接量等信息。 在 JavaScript 脚本中，常用分隔符来格式化代码，以方便阅读。**

对于下面一行代码：

```javascript
function toStr(a){return a.toString();}
```

可以使用分隔符格式化显示：

```javascript
function toStr(a){
  return a.toString();
}
```

?> 一般 JavaScript 编辑器都会提供代码格式化的功能。

分隔符使用时需要注意以下几点：

**1) 分隔符虽然无实际意义，但是在脚本中却不能缺少。如果在标识符与关键字之间不使用分隔符分隔，JavaScript 就会抛出异常。**

在下面代码中，把关键字 function 与标识符 toStr 连在一起，以及把关键字 return 与 toString 标识符连在一起都是错误的。

```javascript
functiontoStr(a){returna.toString();}  //错误写法
function toStr(a){return a.toString();}  //正确写法
```

**2) JavaScript 解析器一般采用最长行匹配原则，不恰当地换行显示一句代码，容易引发异常或错误。**

```javascript
function toStr(a){
    return 
    a.toString();  //错误的换行
}
document.write(toStr("abc"));  //实际返回 undefined,应该返回"abc"
```

**这是因为 return 作为一条独立语句，它后面没有分号，JavaScript解析器在正确解析的前提下会自动为其补加一个分号，以表示该句已经结束。这样换行显示的 `a.toString();` 就是下一句待执行的命令，而不是被返回的值。**

**3) 不能在标识符、关键字等内部使用分隔符。**

在函数中使用空格把 `toString()` 分为两部分，JavaScript 会因无法识别而抛出异常。

```javascript
function toStr(a){
  return a.to String();  //错误分隔符
}
```

**4) 在字符串或者正则表达式内，分隔符是有意义的，不能够随意省略或替换。**

在下面代码中，变量 a 和 b 被赋予相同的字符串，但是变量 b 中插入了空格，则比较结果是不相等的。

```javascript
var a = "空格";
var b = "空格 ";
document.write((a==b));  //返回 false,说明不相同
```

### 注释符

注释就是不被解析的一串字符。JavaScript 注释有以下两种方法：

- 单行注释：`//单行注释信息`
- 多行注释：`/*多行注释信*/`

使用单行注释时，在 `//` 后面的同一行内的任何字符或代码都会被忽视，不再解析。

```javascript
//程序描述
function toStr(a){  //块描述
  //代码段描述
  return a.toString();  //语句描述
}
```

在多行注释中，包含在 `/*` 和 `*/` 符号之间的任何字符都视被为注释文本而忽略掉。

```javascript
/*
* jQuery JavaScript Library v3.3.1
* https://jquery.com/
* Includes Sizzle.js
* https://sizzlejs.com/
* Copyright JS Foundation and other contributors
* Released under the MIT license
* https://jquery.org/license
* Date: 2019-08-21 T 17:24 Z
*/
```

### 转义字符

转义字符是字符的一种间接表示方式。在特殊语境中，无法直接使用字符自身。例如，在字符串中包含说话内容：

```
"子曰："学而不思则罔，思而不学则殆。""
```

由于 JavaScript 已经赋予了双引号为字符串直接量的标识符，如果在字符串中包含双引号，就必须使用转义字符表示：

```
"子曰：\"学而不思则罔，思而不学则殆。\""
```

JavaScript 定义反斜杠加上字符可以表示字符自身。在一个正常字符前添加反斜杠，JavaScript 会忽略该反斜杠。例如：

```javascript
document.write ("子曰：\"学\而\不\思\则\罔\, \思\而\不\学\则\殆\。\"")
```

等价于：

```javascript
document.write("子曰：\"学而不思则罔，思而不学则殆。\"")
```

注意，一些字符加上反斜杠后会表示特殊字符，而不是原字符本身，这些特殊转义字符被称为转义序列，具体说明如表所示：

| 序列   | 代表字符                                                     |
| ------ | ------------------------------------------------------------ |
| \0     | Null字符（\u0000）                                           |
| \b     | 退格符（\u0008）                                             |
| \t     | 水平制表符（\u0009）                                         |
| \n     | 换行符（\u000A）                                             |
| \v     | 垂直制表符（\u000B）                                         |
| \f     | 换页符（\u000C）                                             |
| \r     | 回车符（\u000D）                                             |
| \"     | 双引号（\u0022）                                             |
| \'     | 撇号或单引号（\u0027）                                       |
| \\     | 反斜杠（\u005C）                                             |
| \xXX   | 由 2 位十六进制数值 XX 指定的 Latin-1 字符                   |
| \uXXXX | 由 4 位十六进制数值 XXXX 指定的 Unicode 字符                 |
| \XXX   | 由 1~3 位八进制数值（000 到 377）指定的 Latin-1 字符，可表示 256个 字符。如 \251 表示版本符号。注意，ECMAScript 3.0 不支持，考虑到兼容性不建议使用。 |

