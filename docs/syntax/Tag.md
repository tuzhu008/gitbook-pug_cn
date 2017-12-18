# 标签 Tag

在默认情况下，在每行文本的开头（或者紧跟白字符的部分）书写这个 HTML 标签的名称。使用缩进来表示标签间的嵌套关系，这样可以构建一个 HTML 代码的树状结构。

```pug
ul
  li Item A
  li Item B
  li Item C
```

对应的 HTML:

```html
<ul>
  <li>Item A</li>
  <li>Item B</li>
  <li>Item C</li>
</ul>
```


Pug 还知道哪个元素是自闭合的：

```pug
img
```

对应的 HTML:

```html
<img/>
```

## 块展开

为了节省空间， Pug 为嵌套标签提供了一种内联式语法。

```pug
a: img
```

对应的 HTML:

```html
<a><img/></a>
```

## 自闭合标签

诸如 `img`, `meta`, 和 `link` 之类的标签都是自动闭合的（除非您使用 XML 类型的 doctype）。 您也可以通过在标签后加上 `/` 来明确声明此标签是自闭合的，但请您仅在明确清楚这是在做什么的情况下使用。

```pug
foo/
foo(bar='baz')/
```

对应的 HTML:

```html
<foo/>
<foo bar="baz" />
```