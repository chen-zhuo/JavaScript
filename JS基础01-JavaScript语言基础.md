# JavaScript语言基础

**JavaScript，简称js，是一种面向 Web 的编程语言，所有网页浏览器的支持js运行，是目前使用最广泛的脚本编程语言之一，也是网页设计和 Web 应用必须掌握的基本工具。**

## JavaScript 历史

1995 年 2 月，Netscape 公司发布 Netscape Navigator 2 浏览器，并在这个浏览器中免费提供了一个开发工具——LiveScript。由于当时 Java 比较流行，Netscape 便把 LiveScript 改名为 JavaScript，这也是最初的 JavaScript 1.0 版本。

由于 JavaScript 1.0 很受欢迎，Netscape 在 Netscape Navigator 3 中又发布了 JavaScript 1.1 版本。不久，微软在 Internet Explorer 3 中也加入了脚本编程功能。为了避免与 Netscape 的 JavaScript 产生纠纷，微软特意将其命名为 JScript。

1997 年，欧洲计算机制造商协会（ECMA）以 JavaScript 1.1 为基础制订了脚本语言标准——ECMA-262，这个版本就是 ECMAScript 1.0 版，并将这种语言命名为 ECMAScript。之所以不叫 JavaScript，主要有以下两个原因：

- 商标限制。Java 是 Sun 公司的商标，根据授权协议，只有 Netscape 公司可以合法使用 JavaScript 这个名字，而且 JavaScript 己经被 Netscape 公司注册为商标。
- 体现公益性。该标准的制订者是 ECMA 组织，而不是 Netscape 公司，这样有利于确保规范的开放性和中立性。

1998 年，国际标准化组织和国际电工委员会（ISO/IEC）采用了 ECMAScript 标准（即 ISO/IEC-16262）。自此，浏览器厂商就以 ECMAScript 作为各自 JavaScript 实现的规范标准。JavaScript 正式从各自为政走向了规范统一。

**简单概括，ECMAScript 是 JavaScript 语言的规范标准，JavaScript 是 ECMAScript 的一种实现。注意，这两个词在一般语境中是可以互换的。**

## EECMAScript 版本

1998 年 6 月，ECMAScript 2.0 版发布。

1999 年 12 月，ECMAScript 3.0 版发布，并成为 JavaScript 的通用标准，获得广泛支持。

2007 年 10 月，ECMAScript 4.0 版草案发布，对 3.0 版做了大幅升级。由于 4.0 版的目标过于激进，各方对于是否通过这个标准产生了严重分歧。

2008 年 7月，ECMA 中止 ECMAScript 4.0 的开发，将其中涉及现有功能改善的一小部分发布为 ECMAScript 3.1。不久，ECMAScript 3.1 改名为 ECMAScript 5。

2009 年 12 月，ECMAScript 5.0 版正式发布。

2011 年 6 月，ECMAScript 5.1 版发布，并且成为 ISO 国际标准（ISO/IEC 16262:2011）。

2013 年 12 月，ECMAScript 6 版草案发布。

2015 年 6 月，ECMAScript 6 发布正式版本，并更名为 ECMAScript 2015 。Mozilla 在这个标准的基础上推出了 JavaScript 2.0。

从此以后，JavaScript 开始以年份命名，新版本将按照 “ECMAScript+年份” 的形式发布。目前最新 版本为 ECMAScript 2018，于 2018 年 7 月正式发布。

## 浏览器支持

目前 5 大主流浏览器都支持 ECMAScript 5，具体说明如下：

- Opera 11.60+
- IE 9+
- Firefox 4+
- Safari 5.1+
- Chrome 13+


详细信息可以访问 http://kangax.github.io/compat-table/es5/ 了解。

ECMAScript 6 的支持情况可以访问 http://kangax.github.io/compat-table/es6/ 了解。

IE9 不支持严格模式，直到 IE 10 才开始；Safari 5.1 仍不支持 Function.prototype.bind，尽管 Function.prototype.bind 已经被 Webkit 所支持。

对于旧版浏览器的支持信息，可以查看 Juriy Zaytsev 的 ECMAScript 5 兼容性列表（[http:// kangax.github.io/compat-table/es5/](http://kangax.github.io/compat-table/es5/)）。

## JavaScript 构成

ECMAScript 是 JavaScript 的标准，但它并不等同于 JavaScript，也不是唯一被标准化的规范。

实际上，一个完整的 JavaScript 实现由以下 3 个不同部分组成：

- **核心（ECMAScript）：语言核心部分。**
- **文档对象模型（Document Object Model，DOM）：网页文档操作标准。**
- **浏览器对象模型（BOM）：客户端和浏览器窗口操作基础。**


Web 浏览器只是 ECMAScript 实现的宿主环境之一。宿主环境不仅提供基本的 ECMAScript 实现，同时也会提供各种扩展功能。

文档对象模型是 HTML 的应用程序编程接口（API）。DOM 把整个文档映射为一个树形节点结构，以方便 JavaScript 脚本快速访问和操作。

IE3.0 和 Netscape Navigator 3.0 提供了一种新特性，即 BOM（浏览器对象模型）。使用 BOM 可以对浏览器窗口进行访问和操作，如移动窗口、访问历史记录、动态导航等。与 DOM 不同，BOM 只是 JavaScript 的一个部分，并没有形成规范性标准，但是所有浏览器都默认支持。