#   rem布局

##  rem布局原理

rem是根据html的font-size大小来变化，正是基于这个出发，我们可以在每一个设备下根据设备的宽度设置对应的html字号，从而实现自适应布局。

##  rem的值

目前有两种方法，一种是根据js来调整html的字号，另一种则是通过媒体查询来调整字号。

*   使用js

```
(function(){
	toSize();
	function toSize(){
		var html = document.documentElement;//获取html
		var width = html.clientWidth; //获取到html的宽度
		var nub = 10;//把rem的基准值(也就是html的字体大小)，设置成屏幕宽度的多少分之一
		html.style.fontSize = width / nub + "px";//设置html的字体大小 
	}
})();
```

*   媒体查询

```

```
