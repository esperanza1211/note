#   JS

*   JS  闭包是什么，有什么特性，对页面有什么影响？

>   [JS闭包](https://github.com/esperanza1211/note/blob/master/doc/JS/JS%E9%97%AD%E5%8C%85.md)

*   JS  事件委托是什么？

>   事件委托就是利用冒泡的原理，把事件加到父元素或祖先元素上，触发执行效果。
>   
>   事件委托优点：
>   
>   1.  提高JavaScript性能。事件委托可以显著的提高事件的处理速度，减少内存的占用。
>   
>   2.  动态的添加DOM元素，不需要因为元素的改动而修改事件绑定。

*   原型和原型链？

>   [原型和原型链](https://github.com/esperanza1211/note/blob/master/doc/JS/%E5%8E%9F%E5%9E%8B%E5%92%8C%E5%8E%9F%E5%9E%8B%E9%93%BE.md)

*   ES6中let、const、var的区别是什么？
    
>   let和const在变量声明前使用会报错，var在变量声明前使用提示undefined，变量声明预解析。
>   
>   let和const有块级作用域，var声明在函数内则在函数内具有作用域，声明在函数外则是全局。
>   
>   let不支持重复声明，var可以重复声明
>   
>   const声明的是常量，声明后不可改变，对象则不改变地址，但对象本身是可变的。

*   写出至少三种求数组中的最大值的方法。

>   [数组最大值](https://github.com/esperanza1211/note/blob/master/doc/JS/%E6%95%B0%E7%BB%84%E6%9C%80%E5%A4%A7%E5%80%BC.md)

*   对数组`[5,6,6,7,8,8]`进行去重，ES5或者ES6方法，谈谈对ES6中`=>`的理解。

>   [数组去重](https://github.com/esperanza1211/note/blob/master/doc/JS/%E6%95%B0%E7%BB%84%E5%8E%BB%E9%87%8D.md)
>   
>   [ES6的箭头函数](https://github.com/esperanza1211/note/blob/master/doc/JS/ES6%E7%9A%84%E7%AE%AD%E5%A4%B4%E5%87%BD%E6%95%B0.md)

*   JS  `split()` `join()`的区别？

>   split() 方法使用指定的分隔符字符串将一个String对象分割成字符串数组，以将字符串分隔为子字符串，以确定每个拆分的位置。
>   
>   join() 方法将一个数组（或一个类数组对象）的所有元素连接成一个字符串并返回这个字符串。

*   封装一个深度克隆方法ES5或ES6。
    `json={a:6,b:5,c:[1,2,3,4]};`

```
    function deepinCopy(sources) {
        var obj = {};
        obj = JSON.parse(JSON.stringify(sources));
        return obj;
    }
```

*   JS中常用的弹出式消息提醒的命令是什么？

>   alert() 弹出个提示框 （警告框） 
>   
>   confirm() 弹出个确认框 （确认框） 
>   
>   prompt() 弹出个输入框 让你输入东西（信息输入框）

*   测试一个班级所有学生的成绩是否合格，例：`var arr = [90,89,65,40,100,77,50]`

```
function isPass(arr) {
    for( let i = 0; i < arr.length; i++) {
        if(arr[i] < 60) {
            return "不合格";
        } 
    }
    return "合格";
}
```

*   Canvas和SVG图形的区别是什么？

>   SVG
>   
>   SVG 是一种使用 XML 描述 2D 图形的语言。
>   
>   SVG 基于 XML，这意味着 SVG DOM 中的每个元素都是可用的。您可以为某个元素附加 JavaScript 事件处理器。
>   
>   在 SVG 中，每个被绘制的图形均被视为对象。如果 SVG 对象的属性发生变化，那么浏览器能够自动重现图形。
>   
>   特点：
>   *   不依赖分辨率
>   *   支持事件处理器
>   *   最适合带有大型渲染区域的应用程序（比如谷歌地图）
>   *   复杂度高会减慢渲染速度（任何过度使用 DOM 的应用都不快）
>   *   不适合游戏应用


>   Canvas
>   
>   Canvas 通过 JavaScript 来绘制 2D 图形。
>   
>   Canvas 是逐像素进行渲染的。
>   
>   在 canvas 中，一旦图形被绘制完成，它就不会继续得到浏览器的关注。如果其位置发生变化，那么整个场景也需要重新绘制，包括任何或许已被图形覆盖的对象。
>   
>   特点：
>   *   依赖分辨率
>   *   不支持事件处理器
>   *   弱的文本渲染能力
>   *   能够以 .png 或 .jpg 格式保存结果图像
>   *   最适合图像密集型的游戏，其中的许多对象会被频繁重绘
