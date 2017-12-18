# 包含 Include

包含（include）功能允许您把另外的文件内容插入进来。

```pug
//- includes/head.pug
head
  title 我的网站
  script(src='/javascripts/jquery.js')
  script(src='/javascripts/app.js')
```

```pug
//- includes/foot.pug
footer#footer
  p Copyright (c) foobar
```

```pug
//- index.pug
doctype html
html
  include includes/head.pug
  body
    h1 我的网站
    p 欢迎来到我这简陋得不能再简陋的网站。
    include includes/foot.pug
```

对应的 HTML:

```html
<!DOCTYPE html>
<html>

<head>
  <title>我的网站</title>
  <script src="/javascripts/jquery.js"></script>
  <script src="/javascripts/app.js"></script>
</head>

<body>
  <h1>我的网站</h1>
  <p>欢迎来到我这简陋得不能再简陋的网站。</p>
  <footer id="footer">
    <p>Copyright (c) foobar</p>
  </footer>
</body>

</html>
```

被包含的文件的路径，如果是一个绝对路径（如 `include /root.pug`），那么前面会加上 `options.basedir` 选项属性来进行解析。否则，路径应该相对于正在被编译的当前文件。

在 Pug v1 里，如果没有给出文件扩展名，会自动加上 `.pug`。但是这个特性在 Pug v2 中这是不赞成使用的。


## 包含纯文本

被包含的如果不是 Pug 文件，那么就只会当作文本内容来引入。

```css
/* style.css */
h1 {
  color: red;
}
```

```js
// script.js
console.log('真了不起！');
```

```pug
//- index.pug
doctype html
html
  head
    style
      include style.css
  body
    h1 我的网站
    p 欢迎来到我这简陋得不能再简陋的网站。
    script
      include script.js
```

对应的 HTML:

```html
<!DOCTYPE html>
<html>

<head>
  <style>
    /* style.css */

    h1 {
      color: red;
    }
  </style>
</head>

<body>
  <h1>我的网站</h1>
  <p>欢迎来到我这简陋得不能再简陋的网站。</p>
  <script>
    // script.js
    console.log('真了不起！');
  </script>
</body>

</html>
```

## 使用过滤器包含文本

您可以合并过滤器和包含语句，从而做到引入文件内容并直接用过滤器处理它们。


```md
# article.md

这是一篇用 Markdown 写的文章。
```

```pug
//- index.pug
doctype html
html
  head
    title 一篇文章
  body
    include:markdown-it article.md
```

对应的 HTML:

```html
<!DOCTYPE html>
<html>
  <head>
    <title>一篇文章</title>
  </head>
  <body>
    <h1>article.md</h1>
    <p>这是一篇用 Markdown 写的文章。</p>
  </body>
</html>
```