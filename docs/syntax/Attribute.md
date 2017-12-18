# 属性 Attribute

标签属性和 HTML 语法非常相似，但它们的值就是普通的 JavaScript 表达式。您可以用逗号作为属性分隔符，不过不加逗号也是允许的。

```jade
a(href='baidu.com') 百度
= '\n'
a(class='button' href='baidu.com') 百度
= '\n'
a(class='button', href='baidu.com') 百度
```

对应的 HTML:

```html
<a href="baidu.com">百度</a>
<a class="button" href="baidu.com">百度</a>
<a class="button" href="baidu.com">百度</a>
```

所有 JavaScript 表达式都能用：

```jade
//- 已登录
- var authenticated = true
body(class=authenticated ? 'authed' : 'anon')
```

对应的 HTML:

```html
<body class="authed"></body>
```

## 多行属性

如果您有很多属性，您可以把它们分几行写：

```jade
input(
  type='checkbox'
  name='agreement'
  checked
)
```

对应的 HTML:

```html
<input type="checkbox" name="agreement" checked="checked" />
```

如果您有一个很长属性，并且您的 JavaScript 运行时引擎支持 ECMAScript 2015 模板字符串（包括 Node.js 和 io.js v1.0.0 和更新的版本），您可以使用它来写属性值：

```jade
input(data-json=`
  {
    "非常": "长的",
    "数据": true
  }
`)
```

对应的 HTML:

```html
<input data-json="
  {
    &quot;非常&quot;: &quot;长的&quot;,
    &quot;数据&quot;: true
  }
" />
```

## 用引号括起来的属性

如果您的属性名称中含有某些奇怪的字符，并且可能会与 JavaScript 语法产生冲突的话，会抛出语法错误。这种属性的例子有 Angular 2 中经常用到的 `[]` 和 `()`。

```jade
//- 在这种情况下，`(click)` 会被当作函数调用而不是
//- 属性名称，这会导致一些稀奇古怪的错误。
div(class='div-class' (click)='play()')
```

这样会产生错误：

```
index.pug:3:11
    1| //- 在这种情况下，`(click)` 会被当作函数调用而不是
    2| //- 属性名称，这会导致一些稀奇古怪的错误。
  > 3| div(class='div-class' (click)='play()')
-----------------^

Syntax Error: Assigning to rvalue

```
请您将它们使用 `""` 或者 `''` 括起来，还可以使用逗号来分割不同的属性。

```jade
div(class='div-class', (click)='play()')
div(class='div-class' '(click)'='play()')
```


对应的 HTML:

```html
<div class="div-class" (click)="play()"></div>
<div class="div-class" (click)="play()"></div>

```

## 属性嵌入

> **[danger] 注意**
>
> 在 Pug/Jade 的旧版本中支持一种嵌入语法：
> ```jade
> a(href="/#{url}") Link
> ```
> 这种语法 **已经不再被支持！** 它的相关替代可以在本文档的下面部分找到。另外请您参考我们的迁移指南以获取更多 Pug v2 与之前版本的不兼容情形。


如果您想要在您的属性当中使用变量的话，您可以这样做：

1. 直接使用 JavaScript 写那个属性：

    ```jade
    - var url = 'pug-test.html';
    a(href='/' + url) 链接

    = '\n'

    - url = 'https://example.com/'
    a(href=url) 另一个链接
    ```

    对应的 HTML:

    ```html
    <a href="/pug-test.html">链接</a>
    <a href="https://example.com/">另一个链接</a>
    ```
2. 如果您的 JavaScript 运行时支持 ECMAScript 2015 [模板字符串](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Template_strings)(包含在 Node.js/io.js 1.0.0 以及更新的版本当中)，那么您还可以使用这种方式来简化您的属性值：

    ```jade
    - var btnType = 'info'
    - var btnSize = 'lg'
    button(type='button' class='btn btn-' + btnType + ' btn-' + btnSize)
    = '\n'
    button(type='button' class=`btn btn-${btnType} btn-${btnSize}`)
    ```

    对应的 HTML:

    ```html
    <button class="btn btn-info btn-lg" type="button"></button>
    <button class="btn btn-info btn-lg" type="button"></button>
    ```

## 不转义的属性

在默认情况下，所有的属性都经过转义（即把特殊字符转换成转义序列）来防止诸如跨站脚本攻击之类的攻击方式。如果您非要使用特殊符号，您需要使用 `!=` 而不是 `=`。

```jade
div(escaped="<code>")
div(unescaped!="<code>")
```

对应的 HTML:

```html
<div escaped="&lt;code&gt;"></div>
<div unescaped="<code>"></div>
```

> **[danger] 危险**
>
> 未经转义的缓存代码十分危险。您必须正确处理和过滤用户的输入来避免[跨站脚本攻击](https://en.wikipedia.org/wiki/Cross-site_scripting)。


## 布尔值属性 {#boolean-attributes}

在 Pug 中，布尔值属性是经过映射的，这样布尔值（`true` 和 `false`）就能接受了。当没有指定值的时候，默认是 `true`。

```jade
input(type='checkbox' checked)
= '\n'
input(type='checkbox' checked=true)
= '\n'
input(type='checkbox' checked=false)
= '\n'
input(type='checkbox' checked=true.toString())
```

对应的 HTML:

```html
<input type="checkbox" checked="checked" />
<input type="checkbox" checked="checked" />
<input type="checkbox" />
<input type="checkbox" checked="true" />
```

如果 doctype 是 `html` 的话，Pug 就不会去映射属性，而是使用缩写样式（terse style）（所有浏览器都应该支持）。

```jade
doctype html
= '\n'
input(type='checkbox' checked)
= '\n'
input(type='checkbox' checked=true)
= '\n'
input(type='checkbox' checked=false)
= '\n'
input(type='checkbox' checked=true && 'checked')
```

对应的 HTML:

```html
<!DOCTYPE html>
<input type="checkbox" checked>
<input type="checkbox" checked>
<input type="checkbox">
<input type="checkbox" checked="checked">
```


## 样式属性

`style`（样式）属性可以是一个字符串（就像其他普通的属性一样）还可以是一个对象，这在部分样式是由 JavaScript 生成的情况下非常方便。

```jade
a(style={color: 'red', background: 'green'})
```

对应的 HTML:

```html
<a style="color:red;background:green;"></a>
```

## 类属性

`class`（类）属性可以是一个字符串（就像其他普通的属性一样）还可以是一个包含多个类名的数组，这在类是由 JavaScript 生成的情况下非常方便。

```jade
- var classes = ['foo', 'bar', 'baz']
a(class=classes)
= '\n'
//- the class attribute may also be repeated to merge arrays
a.bang(class=classes class=['bing'])
```

对应的 HTML:

```html
<a class="foo bar baz"></a>
<a class="bang foo bar baz bing"></a>
```

它还可以是一个将类名映射为 true 或 false 的对象，这在使用条件性的类的时候非常有用。


```jade
- var currentUrl = '/about'
a(class={active: currentUrl === '/'} href='/') Home
= '\n'
a(class={active: currentUrl === '/about'} href='/about') About
```

对应的 HTML:

```html
<a href="/">Home</a>
<a class="active" href="/about">About</a>
```

## 类的字面值

类可以使用 `.classname` 语法来定义：

```jade
a.button
```

对应的 HTML:

```html
<a class="button"></a>
```

考虑到使用 `div` 作为标签名这种行为实在是太常见了，所以如果您省略掉标签名称的话，它就是默认值：

```jade
.content
```

对应的 HTML:

```html
<div class="content"></div>
```

## ID 的字面值

ID 可以使用 `#idname` 语法来定义：

```jade
a#main-link
```

对应的 HTML:

```html
<a id="main-link"></a>
```

考虑到使用 `div` 作为标签名这种行为实在是太常见了，所以如果您省略掉标签名称的话，它就是默认值：

```jade
#content
```

对应的 HTML:

```html
<div id="content"></div>
```

## &attributes

读作 “and attributes”，`&attributes` 语法可以将一个对象转化为一个元素的属性列表。

```jade
div#foo(data-bar="foo")&attributes({'data-foo': 'bar'})
```

对应的 HTML:

```html
<div id="foo" data-bar="foo" data-foo="bar"></div>
```

这个对象不一定必须是一个字面值，它同样也可以是一个包含值的对象（参见 Mixin 属性）。

```jade
- var attributes = {};
- attributes.class = 'baz';
div#foo(data-bar="foo")&attributes(attributes)
```

对应的 HTML:

```html
<div class="baz" id="foo" data-bar="foo"></div>
```

> **[danger] 危险**
>
> 使用 `&attributes` 赋值的属性并不会经过自动转义过程。您必须正确处理和过滤用户的输入来避免跨站脚本攻击(XSS)。 但是如果您是从一个 mixin 调用中使用 `attributes` 的话，这个过程就是自动的。
