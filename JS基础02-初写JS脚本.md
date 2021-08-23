# 初写JS脚本

**JavaScript 程序不能够独立运行，只能在宿主环境中执行。一般情况下可以把 JavaScript 代码放在网页中，借助浏览器环境来运行。**

## 第一个程序

新建 HTML 文档，在 HTML 代码中的 \<head> 标签内嵌入 JavaScript 脚本需要使用 \<script> 标签，并设置标签属性 `type="text/javascript"`，用户可以在 \<script> 标签中直接编写 JavaScript 代码：`document.write("<h1>Hi,JavaScript!</h1>")；`。

```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="UTF-8">
    <title>第一个JavaScript程序</title>
    <script type="text/javascript">
        document.write("<h1>Hi,JavaScript!</h1>");
    </script>
</head>
<body></body>
</html>
```

保存 HTML 文档，在浏览器中预览，显示效果如图所示：

![1-1ZR2211T9150](image/1-1ZR2211T9150.gif)

**在 JavaScript 脚本中，`document` 表示网页文档对象；`document.write()` 表示调用 Document 对象的 `write()` 方法，在当前网页源代码中写入 HTML 字符串`"<h1>Hi,JavaScript!</h1>"`。**

?> 现代浏览器默认 \<script> 标签的脚本类型为 JavaScript，因此可以省略 type 属性；如果考虑到兼容早期版本浏览器，则需要设置 type 属性。