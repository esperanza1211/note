#   JS闭包

##  什么是闭包？

1.  函数嵌套函数

2.  函数嵌套函数，子函数的可以访问父级的作用域中的数据,父级不能访问子级

函数的每次执行，都相当于把函数中的代码，重新写了一遍，它的每次执行之间 没有任何的关联

##  闭包的作用

1.  保护函数内的变量，不会变量名污染

2.  保存变量的值，不会被垃圾回收机制回收

##  闭包的缺点

1.  由于闭包会使得函数中的变量都被保存在内存中，内存消耗很大，所以不能滥用闭包，否则会造成网页的性能问题，在IE中可能导致内存泄露。解决方法是，在退出函数之前，将不使用的局部变量全部删除。

2.  闭包会在父函数外部，改变父函数内部变量的值。所以，如果你把父函数当作对象（object）使用，把闭包当作它的公用方法（Public Method），把内部变量当作它的私有属性（private value），这时一定要小心，不要随便改变父函数内部变量的值。

##  闭包对页面的影响

通过使用闭包，我们可以做很多事情。比如模拟面向对象的代码风格；更优雅、更简洁的表达出代码；在某些方面提升代码的执行效率。

##  闭包的应用场景

*   匿名函数自执行
```
(function(){
    alert(1);
})();
!function(){
    alert(2);
}();
-function(){
    alert(3);
}();
+function(){
    alert(4);
}();
~function(){
    alert(5);
}();
```

 *  应用
```
(function(){
    var li = document.querySelectorAll('.list li');
    for(var i = 0; i < li.length; i++){
        fn(i);
    }
    function fn(index){
        li[index].onclick = function(){
            alert(index);
        };
    }
})();
```

```
(function(){
    var li = document.querySelectorAll('.list li');
    for(var i = 0; i < li.length; i++){
        (function(index){
            li[index].onclick = function(){
                alert(index);
            };
        })(i);
    }
})();
```

```
(function(){
    var li = document.querySelectorAll('.list li');

    var fn = (function(index){
            return function(){
                alert(index);
            }
        })(0);
    fn();
})();
```

```
(function(){
    var li = document.querySelectorAll('.list li');
    for(var i = 0; i < li.length; i++){
        li[i].onclick = (function(index){
            return function(){
                alert(index);
            }
        })(i);
    }
})();
```
