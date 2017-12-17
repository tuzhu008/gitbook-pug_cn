# 条件 Conditional

Pug 的条件判断的一般形式的括号是可选的，所以您可以省略掉开头的 `-`，效果是完全相同的。类似一个常规的 JavaScript 语法形式。

```pug
- var user = { description: 'foo bar baz' }
- var authorised = false
#user
  if user.description
    h2.green 描述
    p.description= user.description
  else if authorised
    h2.blue 描述
    p.description.
      用户没有添加描述。
      不写点什么吗……
  else
    h2.red 描述
    p.description 用户没有描述
```

对应的 HTML:

```html
<div id="user">
  <h2 class="green">描述</h2>
  <p class="description">foo bar baz</p>
</div>
```

Pug 同样也提供了它的反义版本 `unless`（下面示例的效果是等价的）：

```pug
unless user.isAnonymous
  p 您已经以 #{user.name} 的身份登录。
```

等同于:

```pug
if !user.isAnonymous
  p 您已经以 #{user.name} 的身份登录。
```
