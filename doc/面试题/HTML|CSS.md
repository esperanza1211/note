#   HTML/CSS

*   块标签和行内标签有哪些？

>   块标签：header/footer/nav/section/article/aside/main/h1-h6/p/ul/ol/li/dl/dt/dd/div/figure/figcaption/form/option
>   
>   内嵌标签：strong/em/span/a/mark/time/b/label/small/big/s

*   简要手绘盒子模型，并对边框和边距进行标注。

    ![index](https://raw.githubusercontent.com/esperanza1211/note/master/image/%E7%9B%92%E6%A8%A1%E5%9E%8B.jpg)

*   CSS的盒模型？

>   标准盒模型：
>   
>   可视宽/高　＝　width/height + padding + border
>   
>   content =  width/height

>   怪异盒模型：
>   
>   可视宽/高　＝　width/height
>   
>   content =  width/height - padding - border
>   
>   在IE6，不设置文档说明，浏览器就进入怪异盒模型解析。

*   界面div三平分除了flex布局外，简写其他两种布局代码。

>   [三等分](https://github.com/esperanza1211/note/blob/master/doc/HTML%7CCSS/%E7%95%8C%E9%9D%A2%E4%B8%89%E5%B9%B3%E5%88%86.md)

*   CSS实现垂直水平居中。

>   [垂直水平居中](https://github.com/esperanza1211/note/blob/master/doc/HTML%7CCSS/%E5%B1%85%E4%B8%AD%E9%97%AE%E9%A2%98.md)

*   html5和css3中新增了哪些标签和属性？

>   [HTML5](https://github.com/esperanza1211/note/blob/master/doc/HTML%7CCSS/HTML5.md)
>   
>   [CSS3](https://github.com/esperanza1211/note/blob/master/doc/HTML%7CCSS/CSS3.md)

*   用css3写一个开关按钮，按下时置灰变色，并改变按钮文字。（如按下之前是on，按下之后是off）。

```
    html:
    <input type="checkbox" id="inp" />
    <label for="inp"></label>

    css:
    input{
        width: 50px;
        height: 50px;
        display: none;
    }
    label{
        width: 200px;
        height: 100px;
        display: inline-block;
        border: 3px solid #ccc;
        border-radius: 100px;
        transition: .5s;
    }
    label:before{
        content: "off";
        font: 50px/2 "微软雅黑";
        color: #ccc;
        text-align: center;
        display: inline-block;
        width: 100px;
        height: 100px;
        background-color: #eee;
        border-radius: 100px;
        border: 1px solid #9d9d9d;
        box-shadow: 0 0 10px 1px #000;
        margin-top: -1px;
        margin-left: -1px;
        transition: .5s;
    }
    input:checked+label{
        background-color: #ccc;
    }
    input:checked+label:before{
        content: "on";
        background-color: #fff;
        margin-left: 99px;
    }
```

*   rem布局的那个函数怎么写？

>   [rem布局](https://github.com/esperanza1211/note/blob/master/doc/HTML%7CCSS/rem%E5%B8%83%E5%B1%80.md)

*   CSS优先级？

>   style行间样式　> id选择器　> class选择器 > 类型选择器 > 通配符*
>   
>   包含选择器的优先级是一种叠加关系
>   
>   群组选择器的优先级不会叠加
>   
>   !important优先级最高

*   CSS3有哪些新特性。

>   可以对CSS3的新特性做一个简单的分类：
>   
>   在布局方面新增了flex布局；
>   
>   在选择器方面新增了例如:first-of-type,nth-child等选择器； 
>   
>   在盒模型方面添加了box-sizing来改变盒模型；
>   
>   在动画方面增加了animation、2d变换、3d变换等；
>   
>   在颜色方面添加透明、rgba等；
>   
>   在字体方面 允许嵌入字体和设置字体阴影；
>   
>   同时当然也有盒子的阴影，最后还有关键的媒体查询。


