# 迭代 Iteration

Pug 目前支持两种主要的迭代方式： `each` 和 `while`。


## each

这是 Pug 的头等迭代方式，让您在模板中迭代数组和对象更为简便：

```pug
ul
  each val in [1, 2, 3, 4, 5]
    li= val
```

对应的 HTML:

```html
<ul>
  <li>1</li>
  <li>2</li>
  <li>3</li>
  <li>4</li>
  <li>5</li>
</ul>
```

您还可以在迭代时获得索引值：

```pug
ul
  each val, index in ['〇', '一', '二']
    li= index + ': ' + val
```

对应的 HTML:

```html
<ul>
  <li>0: 〇</li>
  <li>1: 一</li>
  <li>2: 二</li>
</ul>
```

Pug 还让您能够迭代对象中的键值：

```pug
ul
  each val, index in {1:'一',2:'二',3:'三'}
    li= index + ': ' + val
```

对应的 HTML:

```html
<ul>
  <li>1: 一</li>
  <li>2: 二</li>
  <li>3: 三</li>
</ul>
```

用于迭代的对象或数组仅仅是个 JavaScript 表达式，因此它可以是变量、函数调用的结果，又或者其他的什么东西。

```pug
- var values = [];
ul
  each val in values.length ? values : ['没有内容']
    li= val
```

对应的 HTML:

```html
<ul>
  <li>没有内容</li>
</ul>
```

您还能添加一个 `else` 块，这个语句块将会在数组与对象没有可供迭代的值时被执行。下面这个例子和上面的例子的作用是等价的：

```pug
- var values = [];
ul
  each val in values
    li= val
  else
    li 没有内容
```

对应的 HTML:

```html
<ul>
  <li>没有内容</li>
</ul>
```

您也可以使用 `for` 作为 `each` 的别称。


## while

您也可以使用 `while` 来创建一个循环：

```pug
- var n = 0;
ul
  while n < 4
    li= n++
```

对应的 HTML:

```html
<ul>
  <li>0</li>
  <li>1</li>
  <li>2</li>
  <li>3</li>
</ul>
```