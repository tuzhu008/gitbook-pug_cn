# 混入 Mixin

混入是一种允许您在 Pug 中重复使用一整个代码块的方法。

```pug
//- 定义
mixin list
  ul
    li foo
    li bar
    li baz
//- 使用
+list
+list
```

对应的 HTML:

```html
<ul>
  <li>foo</li>
  <li>bar</li>
  <li>baz</li>
</ul>
<ul>
  <li>foo</li>
  <li>bar</li>
  <li>baz</li>
</ul>
```

它们会被编译成函数形式，您可以传递一些参数：

```pug
mixin pet(name)
  li.pet= name
ul
  +pet('猫')
  +pet('狗')
  +pet('猪')
```

对应的 HTML:

```html
<ul>
  <li class="pet">猫</li>
  <li class="pet">狗</li>
  <li class="pet">猪</li>
</ul>
```

## 混入的块 

混入也可以把一整个代码块像内容一样传递进来：

```pug
mixin article(title)
  .article
    .article-wrapper
      h1= title
      if block
        block
      else
        p 没有提供任何内容。

+article('Hello world')

+article('Hello world')
  p 这是我
  p 随便写的文章
```

对应的 HTML:

```html
<div class="article">
  <div class="article-wrapper">
    <h1>Hello world</h1>
    <p>没有提供任何内容。</p>
  </div>
</div>
<div class="article">
  <div class="article-wrapper">
    <h1>Hello world</h1>
    <p>这是我</p>
    <p>随便写的文章</p>
  </div>
</div>
```

# 混入的属性 

混入也可以隐式地，从“标签属性”得到一个参数 `attributes`：

```pug
mixin link(href, name)
  //- attributes == {class: "btn"}
  a(class!=attributes.class href=href)= name

+link('/foo', 'foo')(class="btn")
```

对应的 HTML:

```html
<a class="btn" href="/foo">foo</a>
```

> **[info] 注意**
>
> `attributes` 里的值已经被（作为标签属性）转义了，所以您可能需要用 `!=` 的方式赋值以避免发生二次转义（详细解释可以查阅[不转义的属性](https://pug.bootcss.com/language/attributes.html#unescaped-attributes)）。

您也可以直接用 `&attributes` 方法来传递 `attributes` 参数：

```pug
mixin link(href, name)
  a(href=href)&attributes(attributes)= name

+link('/foo', 'foo')(class="btn")
```

对应的 HTML:

```html
<a class="btn" href="/foo">foo</a>
```

> **[info] 注意**
>
> `+link(class="btn")` 这种写法也是允许的，且等价于 `+link()(class="btn")`，因为 Pug 会判断括号内的内容是属性还是参数。但我们鼓励您使用后者的写法，明确地传递空的参数，确保第一对括号内始终都是参数列表。

## 剩余参数

您可以用剩余参数（rest arguments）语法来表示参数列表最后传入若干个长度不定的参数，比如：

```pug
mixin list(id, ...items)
  ul(id=id)
    each item in items
      li= item

+list('my-list', 1, 2, 3, 4)
```

对应的 HTML:

```html
<ul id="my-list">
  <li>1</li>
  <li>2</li>
  <li>3</li>
  <li>4</li>
</ul>
```