# Doctype


```jade
doctype html
```

对应的 HTML:

```html
<!DOCTYPE html>
```

## Doctype 缩写

以下是一些常用的 doctype 的缩写：

1. `doctype html`

    ```html
    <!DOCTYPE html>
    ```
2. `doctype xml`

    ```html
    <?xml version="1.0" encoding="utf-8" ?>
    ```
3. `doctype transitional`

    ```html
    <!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
    ```
4. `doctype strict`

    ```html
    <!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Strict//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-strict.dtd">
    ```
5. `doctype frameset`

    ```html
    <!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Frameset//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-frameset.dtd">
    ```
6. `doctype 1.1`

    ```html
    <!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.1//EN" "http://www.w3.org/TR/xhtml11/DTD/xhtml11.dtd">
    ```
7. `doctype basic`

    ```html
    <!DOCTYPE html PUBLIC "-//W3C//DTD XHTML Basic 1.1//EN" "http://www.w3.org/TR/xhtml-basic/xhtml-basic11.dtd">
    ```
8. `doctype mobile`

    ```html
    <!DOCTYPE html PUBLIC "-//WAPFORUM//DTD XHTML Mobile 1.2//EN" "http://www.openmobilealliance.org/tech/DTD/xhtml-mobile12.dtd">
    ```
9. `doctype plist`

    ```html
    <!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
    ```

## 自定义 doctype

您也可以自定义一个 doctype 字面值：

```jade
doctype html PUBLIC "-//W3C//DTD XHTML Basic 1.1//EN"
```

对应的 HTML

```HTML
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML Basic 1.1//EN">
```

## Doctype 选项

Doctype 会影响 Pug 的编译结果。比如自闭合的标签是以 `/>` 还是以 `>` 结束，这取决于指定了是 HTML 还是 XML。[布尔值属性](//docs/syntax/Attribute.md#boolean-attributes)也同样会受到影响。

如果因为某些原因，不能在模板里使用 doctype 关键字（比如需要渲染的是 HTML 的一个片段），但您依然需要指定 doctype 的时候，您就可以通过 [doctype 选项](//docs/API.md#options)来设置了。

```jade
var pug = require('./');

var source = 'img(src="foo.png")';

pug.render(source);
// => '<img src="foo.png"/>'

pug.render(source, {doctype: 'xml'});
// => '<img src="foo.png"></img>'

pug.render(source, {doctype: 'html'});
// => '<img src="foo.png">'
```