# 常见问题 {#faq}

* <strong class="question"><span class='q-icon'><i class="fa fa-question" aria-hidden="true"></i></span>问：</strong>
  如何将父模板的参数传递到子模板？

  <strong class="answer">答：</strong> 在 `include` 时，被包含进来的部分是可以访问父模板作用域中的参数的。

  ```jade
  h2 Recent Article

  -var articles=recentArticles
  include ../articles/list
  ```
  上面的代码中，子模板 `list` 被 `include` 进来，因为在 `include` 之前声明了一个变量 `articles`，所以在子模板中可以访问这个变量。
