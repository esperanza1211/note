#   防止重复发送AJAX请求

1.  独占型提交

只允许同时存在一次提交，并且直到本次提交完成才能进行下一次提交。

```
module.submit = function() {
  if (this.promise_.state() === 'pending') {
    return
  }
  return this.promise_ = $.post('/api/save')
}
```
