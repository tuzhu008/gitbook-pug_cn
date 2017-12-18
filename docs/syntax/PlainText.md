# 纯文本 Plain Text

Pug 提供了三种通常使用的方式来放置纯文本。它们在不同的情况下会派上不同的用途。

## 管道文本

这是最简单的向模板添加纯文本的方法。只需要在每行前面加一个 `|` 字符（这个字符在类 Unix 系统下常用作“管道”功能，因此得名）。

```pug
| 纯文本当然也可以包括 <strong>HTML</strong> 内容。
p
  | 但它必须单独起一行。

```

对应的 HTML:

```html
纯文本当然也可以包括 <strong>HTML</strong> 内容。
<p>但它必须单独起一行。</p>
```

## 标签的行内

这实际上是最常见的情况，文本只需要和标签名隔开一个空格即可。

```pug
p 纯文本当然也可以包括 <strong>HTML</strong> 内容。
```

对应的 HTML:

```html
<p>纯文本当然也可以包括 <strong>HTML</strong> 内容。</p>
```

## 标签中的块

有的时候您可能想要写一个非常大的纯文本块。一个典型的例子就是嵌入 Pug 的脚本或者样式。如果要这么做，只需要在标签后面接上一个 `.`（不要有空格）：

```pug
script.
  if (usingPug)
    console.log('这是明智的选择。')
  else
    console.log('请用 Pug。')
```


对应的 HTML:

```html
<script>
  if (usingPug)
    console.log('这是明智的选择。')
  else
    console.log('请用 Pug。')
</script>
```