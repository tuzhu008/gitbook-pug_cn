<a href="https://pugjs.org"><img src="assets/images/logo.svg" height="200" align="right"></a>
# Pug

完整的文档在 [pugjs.org](https://pugjs.org/)


 Pug是一个高性能的模板引擎，深受 [Haml](http://haml.info/) 的影响，并为 [Node.js](http://nodejs.org) 实现了浏览器 JavaScript。对于bug报告、特性请求和问题，请[打开一个问题](https://github.com/pugjs/pug/issues/new)。讨论请加入[聊天室](https://gitter.im/pugjs/pug)。

 你可以在[这里](https://pugjs.org/)试驾 Pug。

 [![Build Status](https://img.shields.io/travis/pugjs/pug/master.svg?style=flat)](https://travis-ci.org/pugjs/pug)
 [![Coverage Status](https://img.shields.io/coveralls/pugjs/pug/master.svg?style=flat)](https://coveralls.io/r/pugjs/pug?branch=master)
 [![Dependency Status](https://img.shields.io/david/pugjs/pug.svg?style=flat)](https://david-dm.org/pugjs/pug)
 [![devDependencies Status](https://img.shields.io/david/dev/pugjs/pug.svg?style=flat)](https://david-dm.org/pugjs/pug?type=dev)
 [![NPM version](https://img.shields.io/npm/v/pug.svg?style=flat)](https://www.npmjs.com/package/pug)
 [![Join Gitter Chat](https://img.shields.io/badge/gitter-join%20chat%20%E2%86%92-brightgreen.svg?style=flat)](https://gitter.im/pugjs/pug?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)
[![OpenCollective](https://opencollective.com/pug/backers/badge.svg)](#backers) 
[![OpenCollective](https://opencollective.com/pug/sponsors/badge.svg)](#sponsors)

## 重命名自 "Jade"

这个项目以前被称为“Jade”。然而，它已经向我们透露，“Jade”是一个注册商标，因此需要重命名。在维护人员之间进行了一些讨论之后，**“Pug”** 被选为这个项目的新名称。下一个主要版本将把“pug” 作为包名。

如果您的包或应用程序目前使用的是 `jade`，请不要担心:我们已经获得了继续使用这个包名的权限，尽管所有的新版本都将在 `pug` 下发布。

在重命名之前，我们已经开始研究一个不兼容的 Jade 2.0.0。我们这样做了，所以这个新的主要版本 bump 将与重命名为 Pug 一致。因此，从 Jade 升级到 Pug，将与升级任何其他带有主要版本的包的过程一样。目前，Pug 2.0.0 还处于测试阶段，我们已经弃用了一些语法差异。这些差异在 [#2305](https://github.com/pugjs/pug/issues/2305) 被记录下来。

Pug的网站和文档还在更新中，但是如果你是 Pug 的新手，你应该开始使用新的语法，并在 npm 上安装 Pug 包。

## 安装

### 包

via npm:

```bash
$ npm install pug
```

### 命令行

在安装了最新版本的 [Node.js](http://nodejs.org/) 后，使用以下指令安装命令行接口：

```bash
$ npm install pug-cli -g
```

运行：

```bash
$ pug --help
```

## 语法

Pug是一种干净的、空白敏感的语法，用于编写 html。这里有一个简单的例子:

```jade
doctype html
html(lang="en")
  head
    title= pageTitle
    script(type='text/javascript').
      if (foo) bar(1 + 5)
  body
    h1 Pug - node template engine
    #container.col
      if youAreUsingPug
        p You are amazing
      else
        p Get on it!
      p.
        Pug is a terse and simple templating language with a
        strong focus on performance and powerful features.
```

对应的 HTML：


```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <title>Pug</title>
    <script type="text/javascript">
      if (foo) bar(1 + 5)
    </script>
  </head>
  <body>
    <h1>Pug - node template engine</h1>
    <div id="container" class="col">
      <p>You are amazing</p>
      <p>Pug is a terse and simple templating language with a strong focus on performance and powerful features.</p>
    </div>
  </body>
</html>
```

## API

完整的 API，请参见 [API英文文档](https://pugjs.org/api/reference.html)。
。也可以查看  [Pug API 中文文档](https://tuzhu008.github.io/gitbook-pug_cn/)。

```js
var pug = require('pug');

// 编译
var fn = pug.compile('string of pug', options);
var html = fn(locals);

// 渲染
var html = pug.render('string of pug', merge(options, locals));

// 渲染文件
var html = pug.renderFile('filename.pug', merge(options, locals));
```

### 选项

 - `filename`  用于异常信息以及（使用相对路径的）包含（include）和扩展（extends）操作。
 - `compileDebug`  当设置为 `false` 时，源代码不会被包含在编译出来的模板函数中，
 - `pretty`    在输出中添加空白缩进 _(默认为：`false`)_

## 浏览器支持

最新版本的 pug 可以从[这里](https://pugjs.org/js/pug.js)下载到浏览器中。它只支持最新的浏览器，而且是一个大文件。建议您预编译您的 pug 模板到JavaScript。

要在客户端上使用命令行编译模板，这样做：


```bash
$ pug --client --no-debug filename.pug
```

这将生成一个包含被编译模板的 `filename.js` 文件。

## 额外的资源

教程:

  - cssdeck interactive [Pug syntax tutorial](http://cssdeck.com/labs/learning-the-jade-templating-engine-syntax)
  - cssdeck interactive [Pug logic tutorial](http://cssdeck.com/labs/jade-templating-tutorial-codecast-part-2)
  - [Pug について。](https://gist.github.com/japboy/5402844) (A Japanese Tutorial)

在其他语言中实现:

  - [Larpug - Pug for Laravel](https://github.com/acidjazz/larpug)
  - [php](https://github.com/pug-php/pug)
  - [scala](https://scalate.github.io/scalate/documentation/scaml-reference.html)
  - [ruby](https://github.com/slim-template/slim)
  - [python](https://github.com/matannoam/pypugjs)
  - [java](https://github.com/neuland/jade4j)
  - [C# ASP.NET Core](https://github.com/AspNetMonsters/pugzor)

其他:

  - [Emacs Mode](https://github.com/brianc/jade-mode)
  - [Vim Syntax](https://github.com/digitaltoad/vim-pug)
  - [TextMate Bundle](http://github.com/miksago/jade-tmbundle)
  - [Coda/SubEtha syntax Mode](https://github.com/aaronmccall/jade.mode)
  - [html2pug](https://github.com/donpark/html2jade) converter
  - [pug2php](https://github.com/SE7ENSKY/jade2php) converter
  - [Pug Server](https://github.com/ded/jade-server)  Ideal for building local prototypes apart from any application
  - [pug-ruby](https://github.com/yivo/pug-ruby) gem: Allows to invoke Pug and Jade from Ruby
  - [pug-rails](https://github.com/yivo/pug-rails) gem: Integrates Pug and Jade into your Rails application
  - [cache-pug-templates](https://github.com/ladjs/cache-pug-templates) Cache Pug templates for [Lad](https://github.com/ladjs/lad)/[Koa](https://github.com/koajs/koa)/[Express](https://github.com/expressjs/express)/[Connect](https://github.com/senchalabs/connect) with [Redis](https://redis.io/)


## 支持者
每月的捐款支持我们，并帮助我们继续我们的活动。 [称为支持者](https://opencollective.com/pug#backer)]

<a href="https://opencollective.com/pug/backer/0/website" target="_blank"><img src="https://opencollective.com/pug/backer/0/avatar.svg"></a>
<a href="https://opencollective.com/pug/backer/1/website" target="_blank"><img src="https://opencollective.com/pug/backer/1/avatar.svg"></a>
<a href="https://opencollective.com/pug/backer/2/website" target="_blank"><img src="https://opencollective.com/pug/backer/2/avatar.svg"></a>
<a href="https://opencollective.com/pug/backer/3/website" target="_blank"><img src="https://opencollective.com/pug/backer/3/avatar.svg"></a>
<a href="https://opencollective.com/pug/backer/4/website" target="_blank"><img src="https://opencollective.com/pug/backer/4/avatar.svg"></a>
<a href="https://opencollective.com/pug/backer/5/website" target="_blank"><img src="https://opencollective.com/pug/backer/5/avatar.svg"></a>
<a href="https://opencollective.com/pug/backer/6/website" target="_blank"><img src="https://opencollective.com/pug/backer/6/avatar.svg"></a>
<a href="https://opencollective.com/pug/backer/7/website" target="_blank"><img src="https://opencollective.com/pug/backer/7/avatar.svg"></a>
<a href="https://opencollective.com/pug/backer/8/website" target="_blank"><img src="https://opencollective.com/pug/backer/8/avatar.svg"></a>
<a href="https://opencollective.com/pug/backer/9/website" target="_blank"><img src="https://opencollective.com/pug/backer/9/avatar.svg"></a>
<a href="https://opencollective.com/pug/backer/10/website" target="_blank"><img src="https://opencollective.com/pug/backer/10/avatar.svg"></a>
<a href="https://opencollective.com/pug/backer/11/website" target="_blank"><img src="https://opencollective.com/pug/backer/11/avatar.svg"></a>
<a href="https://opencollective.com/pug/backer/12/website" target="_blank"><img src="https://opencollective.com/pug/backer/12/avatar.svg"></a>
<a href="https://opencollective.com/pug/backer/13/website" target="_blank"><img src="https://opencollective.com/pug/backer/13/avatar.svg"></a>
<a href="https://opencollective.com/pug/backer/14/website" target="_blank"><img src="https://opencollective.com/pug/backer/14/avatar.svg"></a>
<a href="https://opencollective.com/pug/backer/15/website" target="_blank"><img src="https://opencollective.com/pug/backer/15/avatar.svg"></a>
<a href="https://opencollective.com/pug/backer/16/website" target="_blank"><img src="https://opencollective.com/pug/backer/16/avatar.svg"></a>
<a href="https://opencollective.com/pug/backer/17/website" target="_blank"><img src="https://opencollective.com/pug/backer/17/avatar.svg"></a>
<a href="https://opencollective.com/pug/backer/18/website" target="_blank"><img src="https://opencollective.com/pug/backer/18/avatar.svg"></a>
<a href="https://opencollective.com/pug/backer/19/website" target="_blank"><img src="https://opencollective.com/pug/backer/19/avatar.svg"></a>
<a href="https://opencollective.com/pug/backer/20/website" target="_blank"><img src="https://opencollective.com/pug/backer/20/avatar.svg"></a>
<a href="https://opencollective.com/pug/backer/21/website" target="_blank"><img src="https://opencollective.com/pug/backer/21/avatar.svg"></a>
<a href="https://opencollective.com/pug/backer/22/website" target="_blank"><img src="https://opencollective.com/pug/backer/22/avatar.svg"></a>
<a href="https://opencollective.com/pug/backer/23/website" target="_blank"><img src="https://opencollective.com/pug/backer/23/avatar.svg"></a>
<a href="https://opencollective.com/pug/backer/24/website" target="_blank"><img src="https://opencollective.com/pug/backer/24/avatar.svg"></a>
<a href="https://opencollective.com/pug/backer/25/website" target="_blank"><img src="https://opencollective.com/pug/backer/25/avatar.svg"></a>
<a href="https://opencollective.com/pug/backer/26/website" target="_blank"><img src="https://opencollective.com/pug/backer/26/avatar.svg"></a>
<a href="https://opencollective.com/pug/backer/27/website" target="_blank"><img src="https://opencollective.com/pug/backer/27/avatar.svg"></a>
<a href="https://opencollective.com/pug/backer/28/website" target="_blank"><img src="https://opencollective.com/pug/backer/28/avatar.svg"></a>
<a href="https://opencollective.com/pug/backer/29/website" target="_blank"><img src="https://opencollective.com/pug/backer/29/avatar.svg"></a>

## 赞助商

成为一个赞助商，并在 Github 的 README 中看到你的标志，链接到你的网站上。
[[称为赞助商](https://opencollective.com/pug#sponsor)]

<a href="https://opencollective.com/pug/sponsor/0/website" target="_blank"><img src="https://opencollective.com/pug/sponsor/0/avatar.svg"></a>
<a href="https://opencollective.com/pug/sponsor/1/website" target="_blank"><img src="https://opencollective.com/pug/sponsor/1/avatar.svg"></a>
<a href="https://opencollective.com/pug/sponsor/2/website" target="_blank"><img src="https://opencollective.com/pug/sponsor/2/avatar.svg"></a>
<a href="https://opencollective.com/pug/sponsor/3/website" target="_blank"><img src="https://opencollective.com/pug/sponsor/3/avatar.svg"></a>
<a href="https://opencollective.com/pug/sponsor/4/website" target="_blank"><img src="https://opencollective.com/pug/sponsor/4/avatar.svg"></a>
<a href="https://opencollective.com/pug/sponsor/5/website" target="_blank"><img src="https://opencollective.com/pug/sponsor/5/avatar.svg"></a>
<a href="https://opencollective.com/pug/sponsor/6/website" target="_blank"><img src="https://opencollective.com/pug/sponsor/6/avatar.svg"></a>
<a href="https://opencollective.com/pug/sponsor/7/website" target="_blank"><img src="https://opencollective.com/pug/sponsor/7/avatar.svg"></a>
<a href="https://opencollective.com/pug/sponsor/8/website" target="_blank"><img src="https://opencollective.com/pug/sponsor/8/avatar.svg"></a>
<a href="https://opencollective.com/pug/sponsor/9/website" target="_blank"><img src="https://opencollective.com/pug/sponsor/9/avatar.svg"></a>
<a href="https://opencollective.com/pug/sponsor/10/website" target="_blank"><img src="https://opencollective.com/pug/sponsor/10/avatar.svg"></a>
<a href="https://opencollective.com/pug/sponsor/11/website" target="_blank"><img src="https://opencollective.com/pug/sponsor/11/avatar.svg"></a>
<a href="https://opencollective.com/pug/sponsor/12/website" target="_blank"><img src="https://opencollective.com/pug/sponsor/12/avatar.svg"></a>
<a href="https://opencollective.com/pug/sponsor/13/website" target="_blank"><img src="https://opencollective.com/pug/sponsor/13/avatar.svg"></a>
<a href="https://opencollective.com/pug/sponsor/14/website" target="_blank"><img src="https://opencollective.com/pug/sponsor/14/avatar.svg"></a>
<a href="https://opencollective.com/pug/sponsor/15/website" target="_blank"><img src="https://opencollective.com/pug/sponsor/15/avatar.svg"></a>
<a href="https://opencollective.com/pug/sponsor/16/website" target="_blank"><img src="https://opencollective.com/pug/sponsor/16/avatar.svg"></a>
<a href="https://opencollective.com/pug/sponsor/17/website" target="_blank"><img src="https://opencollective.com/pug/sponsor/17/avatar.svg"></a>
<a href="https://opencollective.com/pug/sponsor/18/website" target="_blank"><img src="https://opencollective.com/pug/sponsor/18/avatar.svg"></a>
<a href="https://opencollective.com/pug/sponsor/19/website" target="_blank"><img src="https://opencollective.com/pug/sponsor/19/avatar.svg"></a>
<a href="https://opencollective.com/pug/sponsor/20/website" target="_blank"><img src="https://opencollective.com/pug/sponsor/20/avatar.svg"></a>
<a href="https://opencollective.com/pug/sponsor/21/website" target="_blank"><img src="https://opencollective.com/pug/sponsor/21/avatar.svg"></a>
<a href="https://opencollective.com/pug/sponsor/22/website" target="_blank"><img src="https://opencollective.com/pug/sponsor/22/avatar.svg"></a>
<a href="https://opencollective.com/pug/sponsor/23/website" target="_blank"><img src="https://opencollective.com/pug/sponsor/23/avatar.svg"></a>
<a href="https://opencollective.com/pug/sponsor/24/website" target="_blank"><img src="https://opencollective.com/pug/sponsor/24/avatar.svg"></a>
<a href="https://opencollective.com/pug/sponsor/25/website" target="_blank"><img src="https://opencollective.com/pug/sponsor/25/avatar.svg"></a>
<a href="https://opencollective.com/pug/sponsor/26/website" target="_blank"><img src="https://opencollective.com/pug/sponsor/26/avatar.svg"></a>
<a href="https://opencollective.com/pug/sponsor/27/website" target="_blank"><img src="https://opencollective.com/pug/sponsor/27/avatar.svg"></a>
<a href="https://opencollective.com/pug/sponsor/28/website" target="_blank"><img src="https://opencollective.com/pug/sponsor/28/avatar.svg"></a>
<a href="https://opencollective.com/pug/sponsor/29/website" target="_blank"><img src="https://opencollective.com/pug/sponsor/29/avatar.svg"></a>

## License

MIT
