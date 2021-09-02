# JS逆向实战

本章节针对的重点是JS加密网站的实战破解，目标是提升爬虫的防JS反爬能力。

## JS逆向简介

### 大势所趋

随着爬虫技术的普及，其产生的经济效益也是不容小觑，例如，公司通过爬虫获取数据再以付费的形式提供给需要数据服务的人。但任何技术都是有两面性的，各大权威数据发布网站对于爬虫就不是那么友好了，因为爬虫会给他们网站服务器造成格外的压力和虚假的流量，例如，有的网站访问量达到了90亿次，但其中几乎90%的访问量都是爬虫带来。

因此，许多被爬的网站针对爬虫设置了许多的反爬措施，例如，请求头必须是浏览器，一个ip不能高频率访问，各式各样的验证码等。其中JS加密成为了许多网站反爬的选择，原因是：

- JS在所有浏览器中都通用；
- JS有改变网页内容的能力；
- JS是在浏览器进行加载和解析，不会消耗服务器资源；
- 爬虫想要获取JS加密前的网站内容，那么爬虫开发者必须熟练JS，并且通过逆向还原；

综上所述，学会了JS逆向，我们有相当于又多了一条解决JS加密的道路，而且优势巨大，找爬虫类的工作也是轻而易举。

### 逆向流程

**JS逆向简单说，就是对JS加密后的内容（POST参数、Cookie、网页内容等）进行JS解密的一个过程。**这个解密的过程大体上都是相似的：

1. 访问网站，抓取数据包，并进行分析；
2. 找出加密内容，定位到JS代码加密的节点；
3. 分析JS加密过程，在能运行JS环境的工具中进行逆向还原；
4. JS调试成功后，让爬虫运行过程中加载JS，成功获取网页内容。

## 准备工作

### 安装JS环境

首先需要安装一个能执行Js的环境，推荐 [**Node.js**](https://nodejs.org/en/download/)，**一个基于 Chrome V8 引擎的 JavaScript 运行环境**。

解压下载的文件，拷贝解压路径，添加到环境变量。命令行中输入：`node --version` ，检查Node.js版本。

![QQ截图20200323224413](image/QQ截图20200323224413.png)

### 安装JS插件

如果你觉得没有必要安装一个完整的JS环境，我们可以选择安装小而精的JS插件，同样能够运行JS代码。

打开PyCharm——选择”File“——选择”Settings“

![QQ截图20210902175259](image/QQ截图20210902175259.png)

选择”Plugins“——选择”Marketplace“——输入”Node“——点击”Install“（已经安装显示”Installed“）

![QQ截图20210902180439](image/QQ截图20210902180439.png)

安装好了以后，我们你就可以直接在PyCharm中运行js代码文件了：

![QQ截图20210902182519](image/QQ截图20210902182519.png)

### 安装PyExecJS

**PyExecJS 是一个可以使用 Python 来模拟运行 JavaScript 的库。**大家可能听说过 PyV8，它也是用来模拟执行 JavaScript 的库，可是由于这个项目已经不维护了，而且对 Python3 的支持不好，而且安装出现各种问题，所以这里选用了 PyExecJS 库。

接下来我们安装第三方库PyExecJS：

```
pip install -i https://pypi.douban.com/simple PyExecJS
```

运行代码检查一下运行环境：

```python
# 注意：在导入的时候是execjs不是PyExecJS
import execjs
print(execjs.get().name)

'''
# 解释：js运行环境为Node.js
Node.js (V8)
'''
```

开发爬虫过程中，也通常使用PyExecJS库对js文件当中的方法进行调用：

```python
import execjs

def read_js_file():
    with open("md5.js", 'r', encoding = 'utf-8') as f: # 打开JS文件
        content = f.read()
        return content

jsstr = read_js_file()
JsObj = execjs.compile(jsstr) #加载JS文件
# 调用js方法，第一个参数是JS的方法名，后面则是js方法的参数
ret = JsObj.call('md5', '123456')
print(ret)
```

这里运行的结果和上面插件运行出来的结果一模一样：

![QQ截图20210902183417](image/QQ截图20210902183417.png)