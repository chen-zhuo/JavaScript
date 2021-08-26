# JavaScript常用元素

## 变量

变量相当于容器，值相当于容器内装的东西，而变量名就是容器上贴着的标签，通过标签可以找到 变量，以便读、写它存储的值。

JavaScript 是弱类型语言，对于变量类型的规范比较松散。具体表现如下：

- 变量的类型分类不严谨、不明确，带来使用的随意性。
- 声明变量时，不要求指定类型。
- 使用过程不严格，可以根据需要自动转换变量类型。
- 变量的转换和类型检查没有一套统一、规范的方法，导致开发效率低下。

由此带来的优缺点如下： 

- 优点：使用灵活，简化了代码编写。
- 缺点：执行效率低，在开发大型应用时，程序性能会受到影响。

### 声明变量

**在 JavaScript 中，声明变量使用 `var` 语句。**

**在一个 `var` 语句中，可以声明一个或多个变量，未赋值的变量初始化为 `undefined（未定义）` 值。当声明多个变量时，应使用逗号运算符分隔。**

```javascript
var a;  //声明一个变量
var a,b,c;  //声明多个变量
document.write(a);  //返回 undefined
```

**在变量声明的过程当中也可以使用等号 `=` 运算符为其赋值，等号左侧为变量，右侧为被赋的值。**

```javascript
var b = 1; //声明并赋值
document.write(b);  //返回 1
var a = 1;
var a = 2; //重复赋值
var a = 3; //重复赋值
document.write(a);  //返回 3
```

!> 在非严格模式下，JavaScript 允许不声明变量就直接为其赋值，这是因为 JavaScript 解释器能够自动隐式声明变量。隐式声明的变量总是作为全局变量使用。

### 变量提升

**JavaScript 引擎的解析方式是：先解析代码，获取所有被声明的变量，然后再一行一行地运行。 这样，所有声明的变量都会被提升到代码的头部，这就叫作变量提升（Hoisting）。简单说，JavaScript 在预编译期会先预处理声明的变量，但是变量的赋值操作发生在 JavaScript 执行期，而不是预编译期。**

```javascript
document.write(a); //显示undefined
a =1;
document.write(a); //显示 1
var a;
```

声明变量放在最后，赋值操作放在前面。由于 JavaScript 在预编译期已经对变量声明语句进行了预解析，所以第一行代码读取变量值时不会抛出异常，而是返回未初始化的值 undefined。第三行代码是在赋值操作之后读取，故显示为数字 1。

### 变量作用域

**变量作用域（Scope）是指变量在程序中可以访问的有效范围，也称为变量的可见性。**

JavaScript 变量可以分为全局变量和局部变量：

- **全局变量：变量在整个页面脚本中都是可见的，可以被自由访问。**
- **局部变量：变量仅能在声明的函数内部可见，函数外是不允许访问的。**

```javascript
var a = 1;  //声明并初始化全局变量
function f(){  //声明函数
    document.write(a);  //显示undefined
    var a = 2;  //声明并初始化局部变量
    document.write(a);  //显示 2
}
f(); //调用函数
```

由于在函数内部声明了一个同名局部变量 a，所以在预编译期，JavaScript 使用该变量覆盖掉全局变量在函数内部的影响。而在执行初期，局部变量 a 未赋值，所以在函数内第 1 行代码读取局部变量 a 的值也就是 `undefined` 了。当执行到函数第 2 行代码时，为局部变量赋值 2，所以在第 3 行中就显示为 2。

### 变量污染

定义全局变量有 3 种方式：

- 在任何函数体外直接使用 var 语句声明。

  ```javascript
  var f = 'value1';

- **直接添加属性到全局对象上。在 Web 浏览器中，全局作用域对象为 window。**

  ```javascript
  window.f = 'value';
  ```

- 直接使用未经声明的变量，以这种方式定义的全局变量被称为隐式的全局变量。

  ```javascript
  f = 'value' ;
  ```

**全局变量在全局作用域内都是可见的，因此具有污染性。大量使用全局变量会降低程序的可靠性，用户应该避免使用全局变量。**

为了减少使用全局变量，使用函数体封装应用程序，这是最常用的一种方法。

在脚本中创建一个全局变量，作为当前应用的唯一接口，然后通过对象直接量的形式包含所有应用程序变量。把应用程序的所有变量都追加在该唯一名称空间下，降低与其他应用程序相互冲突的概率，应用程序也会变得更容易阅读。

**在 JavaScript 函数体内，所有声明的私有变量、参数、内部函数对外都是不可见的，如果不主动开放，外界是无法访问内部数据的，因此使用函数体封装应用程序是最佳实践。**

```javascript
(function(window){
    var MyAPP = {};  //定义 APP 访问接口
    MyAPP.name = {  //定义APP配置变量
        "id" : "应用程序的ID编号"
    };
    MyAPP.work = {
        num : 123,  //APP计数器等内部属性
        sub : { name : "sub_id"},  //APP 应用分支
        doing : function(){  //具体方法
            //执行代码
        }
    };
    window.MyAPP;  //对外开放应用程序接口
})(window)
```

## 基本数据类型

JavaScript 的数据类型分为两种：

- **简单的值（原始值）：包含字符串、数字和布尔值，此外，还有两个特殊值——null（空值）和 undefined（为定义）。**
- **复杂的数据结构（泛指对象）：包括狭义的对象、数组和函数。**

### 基本类型

JavaScript 定义了 6 种基本数据类型，如表所示：

| 数据类型  | 说明                             |
| --------- | -------------------------------- |
| null      | 空值，表示非对象                 |
| undefined | 未定义的值，表示未赋值的初始化值 |
| number    | 数字，数学运算的值               |
| string    | 字符串，表示信息流               |
| boolean   | 布尔值，逻辑运算的值             |
| object    | 对象，表示复合结构的数据集       |

?> 在 JavaScript 中，函数是一种比较特殊的结构。它可以是一段代码集合，也可以是一种数据类型；可以作为对象来使用，还可以作为构造函数创建类型。JavaScript 函数的用法比较灵活，这也是 JavaScript 语言敏捷的一种表现（函数式编程）。

### 布尔型

**布尔型（Boolean）仅包含两个固定的值：`true` 和 `false`。其中，`true` 代表"真”，而 `false` 代表“假”。**

**在 JavaScript 中，`undefined`、`null`、`""`、`0`、`NaN` 和 `false` 这 6 个特殊值转换为布尔值时为 `false`，被称为假值。除了假值以外，其他任何类型的数据转换为布尔值时都是 `true`。**

```javascript
//使用 Boolean() 函数可以强制转换值为布尔值。
console.log(Boolean(0));  //返回 false
console.log(Boolean(NaN)); //返回 false
console.log(Boolean(null)); //返回 false
console.log(Boolean("")); //返回 false
console.log(Boolean(undefined)); //返回 false
```

### Null

**Null 类型只有一个值，即 null，它表示空值，定义一个空对象指针。**

### 字符串

**JavaScript 字符串（String）就是由零个或多个 Unicode 字符组成的字符序列。零个字符表示空字符串。**

#### 字符串直接量

**字符串必须包含在单引号或双引号中。**

1) **如果字符串包含在双引号中，则字符串内可以包含单引号；反之，也可以在单引号中包含双引号。**例如，定义 HTML 字符串时，习惯使用单引号表示字符串，HTML 中包含的属性值使用双引号表示， 这样不容易出现错误。

```javascript
console.log('<meta charset="UTF-8">');
```

2) **在 ECMAScript 3 中，字符串必须在一行内表示，换行表示是不允许的。例如，下面字符串直接量的写法是错误的。**

```javascript
console.log("字符串
直接量"); //抛出异常
```

如果要换行显示字符串，可以在字符串中添加换行符`\n`。例如：

```javascript
console.log("字符串\n直接量");  //在字符串中添加换行符
```

3) **在 ECMAScript 5 中，字符串允许多行表示。实现方法：在换行结尾处添加反斜杠`\`。反斜杠和换行符不作为字符串直接量的内容。**例如：

```javascript
console.log("字符串\
直接量");  //显示“字符串直接量”
```

4) **在字符串中插入特殊字符，需要使用转义字符，如单引号、双引号等。**例如，英文中常用单引号表示撇号，此时如果使用单引号定义字符串，就应该添加反斜杠转义字符，单引号就不再被解析为字符串标识符，而是作为撇号使用。

```javascript
console.log('I can\'t read.');  //显示"I can't read."
```

#### 字符串操作

借助 String 类型的原型方法，可以灵活操作字符串。再配合正则表达式，还可以完成复杂的字符串处理任务。

**在 JavaScript 中，可以使用加号+运算符连接两个字符串，使用字符串的 length 属性获取字符串的字符个数（长度）。**下面代码先合并两个字符串，然后计算它们的长度：

```javascript
var str1 = "学而不思则罔",
    str2 = "思而不学则殆",
    string = str1 + "，" + str2;
document.write(string);  //显示“学而不思则罔，思而不学则殆”
document.write(string.length);  //显示 13
```

#### 字符序列

**JavaScript 字符串是固定不变的字符序列，虽然可以使用各种方法对字符串执行操作，但是返回的都是新的字符串，原字符串保持固定不变。此外，也不能使用 delete 运算符删除字符串中指定位置的字符。**

**在 ECMAScript 5 中，字符串可以作为只读数组使用。除了使用 charAt() 访问其中的字符外，还可以使用中括号运算符来访问。字符串中每个字符都有固定的位置。第 1 个字符的下标位置为 0，第 2 个字符的下标位置为 1…… 以此类推，最后一个字符的下标位置是字符串长度减1。**下面代码使用 for 语句逐个读取字符串中每个字符并显示出来。

```javascript
var str = "学而不思则罔，思而不学则殆";
for(var i=0; i<str.length; i++){
  console.log(str[i]);
}
```

!> 注意：字符串中的字符不能被 `for/in` 语句循环枚举。

### 数字

**数字（Number）也称为数值或数。**

#### 数值直接量

**在 JavaScript 程序中，当数字直接出现在程序中时，被称为数值直接量。**

**数值直接量可以细分为整型直接量和浮点型直接量。浮点数就是带有小数点的数值，而整数是不带小数点的数值。**

```javascript
var int = 1;  //整型数值
var float = 1.0;  //浮点型数值
```

**JavaScript 中的所有数字都是以 64 位浮点数形式存储，包括整数。例如，2 与 2.0 是同一个数。**

浮点数可以使用科学计数法来表示。其中 e （或 E）表示底数，其值为 10，而 e 后面跟随的是 10 的指数。指数是一个整型数值，可以取正负值。

```javascript
var float = 1.2e3;
```

上述代码等价于：

```javascript
var float = 1.2*10*10*10;
var float = 1200;
```

科学计数法表示的浮点数也可以转换为普通的浮点数。

```javascript
var float = 1.2e-3;

等价于：

```javascript
var float = 0.0012;
```

但不等于：

```javascript
var float = 1.2*1/10*1/10*1/10;  //返回 0.0012000000000000001
var float = 1.2/10/10/10;  //返回 0.0012000000000000001
```

#### 浮点数溢出

执行数值计算时，要防止浮点数溢出。例如，0.1+0.2 并不等于 0.3。

```javascript
num = 0.1+0.2;   //0.30000000000000004
```

**这是因为 JavaScript 遵循二进制浮点数算术标准（IEEE 754）而导致的问题。这个标准适合很多应用，但它违背了数字基本常识。**

**解决方法：浮点数中的整数运算是精确的，所以小数表现出来的问题可以通过指定精度来避免。**例如，针对上面的相加可以这样进行处理。

```javascript
a = (1+2)/10;   //0.3
```

?> 这种处理经常在货币计算中用到。例如，元可以通过乘以 100 而转成分，然后就可以准确地将每项相加，求和后的结果可以除以 100 再转换回元。

#### 特殊数值

JavaScript 定义了几个特殊的数值常量，说明如表所示。

| 特殊值                   | 说明                                                         |
| ------------------------ | ------------------------------------------------------------ |
| Infinity                 | 无穷大。当数值超过浮点型所能够表示的范围；反之，负无穷大为-Infinity |
| NaN                      | 非数值。不等于任何数值，包括自己。如当0除以0时会返回这个特殊值 |
| Number.MAX_VALUE         | 表示最大数值                                                 |
| Number.MIN_VALUE         | 表示最小数值，一个接近0的值                                  |
| Number.NaN               | 非数值，与NaN常量相同                                        |
| Number.POSITIVE_INFINITY | 表示正无穷大的数值                                           |
| Number.NEGATIVE_INFINITY | 表示负无穷大的数值                                           |

#### NaN

**NaN（Not a Number，非数字值）是在 IEEE 754 中定义的一个特殊的数值。**

当试图将非数字形式的字符串转换为数字时，就会生成 NaN。

```javascript
+ '0'  //0
+ 'oops'  //NaN
```

当 NaN 参与数学运算时，运算结果也是 NaN。因此，如果表达式的运算值为 NaN，那么可以推断其中至少一个运算数是 NaN。

```javascript
NaN === NaN //false
NaN !== NaN //true
```

#### 数值运算

使用算数运算符，数值可以参与各种计算，如加、减、乘、除等运算操作。

为了解决复杂数学运算，JavaScript 提供了大量的数值运算函数，这些函数作为 Math 对象的方法可以直接调用。

```javascript
var a = Math.floor(20.5);  //调用数学函数，向下舍入
var b = Math.round(20.5);  //调用数学函数，四舍五入
document.write(a);  //返回20
document.write(b);  //返回21
```

### Undefined

**undefined 是 Undefined 类型的唯一值，它表示未定义的值。当声明变量未赋值时，或者定义属性未设置值时，默认值都为 undefined。**

undefined 派生自 null，null 和 undefined 都表示空缺的值，转化为布尔值时都是假值，可以相等。

```javascript
console.log(null == undefined);  //返回 true
```

**null 和 undefined 属于两种不同类型，使用全等运算符（===）或 typeof 运算符可以进行检测。**

```javascript
console.log(null === undefined);  //false
console.log(typeof null);  //返回"object"
console.log(typeof undefined);  //返回"undefined"
```

检测一个变量是否初始化，可以使用 undefined 快速检测。

```javascript
var a; //声明变量
console.log(a);  //返回变量默认值为 undefined
(a == undefined) && (a = 0);  //检测变量是否初始化，否则为其赋值
console.log(a);  //返回初始值 0
```

在下面代码中，声明了变量 a，但没有声明变量 b，然后使用 `typeof` 运算符检测它们的类型，返回的值都是字符串 `"undefined"`。说明不管是声明的变量，还是未声明的变量，都可以通过 `typeof` 运算符检测变量是否初始化。

```javascript
var a;
console.log(typeof a);  //返回"undefined”
console.log(typeof b);  //返回"undefined"
```

对于未声明的变量 b 来说，如果直接在表达式中使用，会引发异常。

```javascript
console.log(b == undefined); //提75未定义的错误信息
```

对于函数来说，如果没有明确的返回值，则默认返回值也为

```javascript
function f(){}
console.log(f());  //返回"undefined"
```

!> undefined 隐含着意外的空值，而 null 隐含着意料之中的空值。因此，设置一个变量、参数为空值时，建议使用 null，而不是 undefined。

## 判断类型

### 使用 `typeof` 

使用 `typeof` 可以检测数据的基本类型，类似于 Python 当中的 `type` 方法：

```javascript
console.log(typeof 1);  //返回字符串"number"
console.log(typeof "1");  //返回字符串"string"
console.log(typeof true);  //返回字符串"boolean"
console.log(typeof {});  //返回字符串"object"
console.log(typeof []);  //返回字符串"object"
console.log(typeof function(){});  //返回字符串"function"
console.log(typeof null);  //返回字符串"object"
console.log(typeof undefined) ;  //返回字符串"undefined"
```

`typeof` 运算符以字符串的形式返回 6 种基本类型之一，不过通过比较可以发现，`typeof` 返回值与上表存在两点差异，简单说明如下：

- 把 `null` 归为 Object 类型，而不是作为一种特殊类型（Null）的值。
- 把 `function(,){}` 归为 Function 类型。即把函数视为一种独立的基本数据类型，而不是 Object 类型的一种特殊子类。

由于 null 值返回类型为 Object，使用下面自定义函数可以避开因为 null 值影响基本类型检测。

```javascript
//如果是 null 值，则先返回字符串 "null" 否则返回（typeof o）的值
function typeOf(o){
    return (o === null) ? "null" : (typeof o);
}
console.log(typeOf(null));  //返回字符串"null"
```

**`typeof` 不能分辨数字和 NaN，并且 NaN 不等同于它自己。**

### 使用 `isNaN()`

使用 `isNaN()` 全局函数可以判断 NaN。

```javascript
isNaN(NaN) //true
isNaN(0) //false
isNaN('oops') //true
isNaN('0') //false
```

### 使用 `isFinite()`

使用 `isFinite()` 全局函数可以判断 NaN 和 Infinity。因此，可以使用它来检测 NaN、正负无穷大。如果是有限数值，或者可以转换为有限数值，那么将返回 `true`。如果只是 NaN、正负无穷大的数值，则返回 `false`。

`isFinite()` 会试图把检测到的值转换为一个数字。如果值不是一个数字，那么使用 `isFinite()` 直接检测就不是有效的方法。通过自定义 isNumber 函数可以避免 `isFinite()` 的缺陷。下面自定义函数先判断值是否为数值类型，如果是数值类型，再使用 `isFinite()` 过滤出有效数字。

```javascript
var isNumber = function isNumber(value){
    return typeof value === 'number' && isFinite(value);
}
```



## 进制转换

JavaScript 支持把十进制数值转换为二进制、八进制和十六进制等不同进制的数值。

十六进制数值以“0X”或“0x”作为前缀，后面跟随十六进制的数值直接量。十六进制的数值是 0~9 和 a~f 的数字或字母任意组合，用来表示 0~15 之间的某个字。

```javascript
var num = 0x1F4;  //十六进制数值
document.write(num);  //返回 500
```

八进制数值以数字 0 为前缀，其后跟随一个八进制的数值直接量。

```javascript
var num = 0764;  //八进制数值
document.write(num);  //返回 500
```

二进制数值以“0B”或“0b”作为前缀，后面跟随二进制的数值直接量。例如：

```javascript
0b11  //等于十进制的 3
```

`toString()` 方法可以根据所传递的参数把数值转换为对应进制的数字字符串。参数范围为 2~36 之间的任意整数。

```javascript
var a = 32;
document.writeln(a.toString(2));  //返回字符串100000
document.writeln(a.toString(4));  //返回字符串200
document.writeln(a.toString(16));  //返回字符串20
document.writeln(a.toString(30));  //返回字符串12
document.writeln(a.toString(32));  //返回字符串10
```

数值直接量不能直接调用 `toString()` 方法，必须先使用小括号或其他方法强制把数字转换为对象。

```javascript
document.writeln(32.toString(16));  //抛出语法错误
document.writeln((32).toString(16));   //返回20
```

## 严格模式

ECMAscript5 新增了严格运行模式。推出严格模式的目的如下：

- 消除 JavaScript 语法中不合理、不严谨的用法。
- 消除代码运行的一些安全隐患。
- 提高编译器效率，提升程序运行速度。
- 为未来新版本的规范化做好铺垫。

### 启用严格模式

在代码首部添加以下一行字符串,即可启用严格模式。

```javascript
"use strict"
```

**不支持严格模式的浏览器会把它作为字符串直接量忽略掉。**

**首部就是指其前面没有任何有效的 JavaScript 代码。**例如，以下用法都不会触发严格模式。

1) "use strict" 前有可执行的代码：

```javascript
var width = 10;
'use strict';  /*无效的严格模式*/
globalVar = 100;
```

2) "use strict" 前有空语句：

```javascript
;
'use strict';  /*无效的严格模式*/
globalVar = 100;
```

或者：

```javascript
;'use strict1';  /*无效的严格模式*/
globalVar = 100;
```

注释语句不作为有效的 JavaScript 代码。例如，下面用法会触发严格模式。

```javascript
//严格模式
'use strict';  /*有效的严格模式*/
globalVar = 100;
```

**因此，只要前面没有会产生实际运行结果的语句，"use strict" 就可以不在第一行。**

### 应用场景

严格模式有两种应用场景，简单说明如下。

**全局模式：将 "use strict" 放在脚本文件的第一行，则整个脚本都将以严格模式运行。如果不在第一行，则整个脚本将以正常模式运行。**

下面示例在页面中添加两个 JavaScript 代码块，第一个代码块将开启严格模式，第二个代码块将按正常模式解析。

```html
<script>
    "use strict";
    console.log("这是严格模式。");
</script>
<script>
    console.log("这是正常模式。");
</script>
```

**局部模式：将 "use strict" 放在函数内首部，则整个函数将以严格模式运行。**

下面示例定义了两个函数，其中第一个函数开启了严格模式，第二个函数按正常模式运行。

```javascript
function strict(){
    "use strict";
    return "这是严格模式。";
}
function notStrict(){
    return "这是正常模式。";
}
```

全局模式不利于 JavaScript 文件合并。例如，如果一个开启了严格模式的 JavaScript 库，被导入到一个正常模式的网页脚本中，由于无法确保 "use strict" 位于脚本的首部位置，容易导致严格模式失效。**因此，推荐的最佳实践是使用局部模式，将整个 JavaScript 文件脚本放在一个立即执行的匿名函数中，在匿名函数内启动严格模式。当 JavaScript 库文件被导入到不同模式的网页中，就不用担心严格模式失效了。**

```javascript
(function(){
    "use strict";
    // JavaScript库文件 代码
}) ();
```

### 执行限制

严格模式对 JavaScript 的语法和行为有着严格的限制。对于初学 JavaScript 语言的读者来说，应该养成好的习惯。例如，变量必须先声明后使用，否则会抛出语法错误。

执行下面代码，将会提示语法错误。因此，必须先用 var 语句声明，然后再使用。

```javascript
"use strict";  //开启严格模式
v = 1;  //报错，v未声明
```

