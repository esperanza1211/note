#   CSS3

### 边框

属性 | 描述 
---|---
border-image | 设置所有border-image-*属性的简写属性。
border-radius | 设置所有四个border-*-radius属性的简写属性。
box-shadow | 向方框添加一个或多个阴影。

### 背景

属性 | 描述 
---|---
background-clip | 规定背景的绘制区域。
background-origin | 规定背景图片的定位区域。
background-size | 规定背景图片的尺寸。

### 文本效果

属性 | 描述 
:---:|:---:
hanging-punctuation | 规定标点字符是否位于线框之外。
punctuation-trim | 规定是否对标点字符进行修剪。
text-align-last | 设置如何对齐最后一行或紧挨着强制换行符之前的行。
text-emphasis | 向元素的文本应用重点标记以及重点标记的前景色。
text-justify | 规定当 text-align 设置为 "justify" 时所使用的对齐方法。
text-outline | 	规定文本的轮廓。
text-overflow | 规定当文本溢出包含元素时发生的事情。
text-shadow | 向文本添加阴影。
text-wrap | 规定文本的换行规则。
word-break | 规定非中日韩文本的换行规则。
word-wrap | 允许对长的不可分割的单词进行分割并换行到下一行。


### 字体

<table style="float:left">
    <thead>
        <tr style="background: #ccc">
            <th>属性</th>  
            <th>值</th>
            <th>描述</th>     
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>font-family</td>  
            <td>name</td>
            <td>必需。规定字体的名称。</td>     
        </tr>
        <tr>
            <td>src</td>  
            <td>URL</td>
            <td>必需。定义字体文件的 URL。</td>     
        </tr>
        <tr>
            <td rowspan="9">font-stretch</td>  
            <td>normal</td>
            <td rowspan="9">可选。定义如何拉伸字体。默认是 "normal"。</td>     
        </tr>
        <tr>
            <td>condensed</td>
        </tr>
        <tr>
            <td>ultra-condensed</td>
        </tr>
        <tr>
            <td>extra-condensed</td>
        </tr>
        <tr>
            <td>semi-condensed</td>
        </tr>
        <tr>
            <td>expanded</td>
        </tr>
        <tr>
            <td>semi-expanded</td>
        </tr>
        <tr>
            <td>extra-expanded</td>
        </tr>
        <tr>
            <td>ultra-expanded</td>
        </tr>
        <tr>
            <td rowspan="3">font-style</td>  
            <td>normal</td>
            <td rowspan="3">可选。定义字体的样式。默认是 "normal"。</td>     
        </tr>
        <tr>
            <td>italic</td>
        </tr>
        <tr>
            <td>oblique</td>
        </tr>
        <tr>
            <td rowspan="7">font-weight</td>  
            <td>normal</td>
            <td rowspan="7">可选。定义字体的粗细。默认是 "normal"。</td>     
        </tr>
        <tr>
            <td>bold</td>
        </tr>
        <tr>
            <td>100</td>
        </tr>
        <tr>
            <td>200</td>
        </tr>
        <tr>
            <td>300</td>
        </tr>
        <tr>
            <td>...</td>
        </tr>
        <tr>
            <td>900</td>
        </tr>
        <tr>
            <td>unicode-range</td>  
            <td>unicode-range</td>
            <td>可选。定义字体支持的 UNICODE 字符范围。默认是 "U+0-10FFFF"。</td>     
        </tr>
    </tbody>
</table>

使用您需要的字体

在新的 @font-face 规则中，您必须首先定义字体的名称（比如 myFirstFont），然后指向该字体文件。

如需为 HTML 元素使用字体，请通过 font-family 属性来引用字体的名称 (myFirstFont)：
```
<style> 
    @font-face{
        font-family: myFirstFont;
        src: url('Sansation_Light.ttf'), url('Sansation_Light.eot');
        /* IE9+ */
    }
    div{
        font-family:myFirstFont;
    }
</style>
```

### 2D转换

属性 | 描述
--- | ---
transform | 向元素应用2D或3D转换。
transform-origin | 允许你改变被转换元素的位置。

### 3D转换

属性 | 描述
--- | ---
transform | 向元素应用2D或3D转换。
transform-origin | 允许你改变被转换元素的位置。
transform-style | 规定被嵌套元素如何在 3D 空间中显示。
perspective | 规定 3D 元素的透视效果。
perspective-origin | 规定 3D 元素的底部位置。
backface-visibility | 定义元素在不面对屏幕时是否可见。

### 过渡

属性 | 描述
--- | ---
transition | 简写属性，用于在一个属性中设置四个过渡属性。
transition-property | 规定应用过渡的 CSS 属性的名称。
transition-duration | 定义过渡效果花费的时间。默认是 0。
transition-timing-function | 规定过渡效果的时间曲线。默认是 "ease"。
transition-delay | 规定过渡效果何时开始。默认是 0。

### CSS3动画

属性 | 描述
--- | ---
@keyframes | 规定动画。
animation | 所有动画属性的简写属性，除了 animation-play-state 属性。
animation-name | 规定 @keyframes 动画的名称。
animation-duration | 规定动画完成一个周期所花费的秒或毫秒。默认是 0。
animation-timing-function | 规定动画的速度曲线。默认是 "ease"。
animation-delay | 规定动画何时开始。默认是 0。
animation-iteration-count | 规定动画被播放的次数。默认是 1。
animation-direction | 规定动画是否在下一周期逆向地播放。默认是 "normal"。
animation-play-state | 规定动画是否正在运行或暂停。默认是 "running"。
animation-fill-mode | 规定对象动画时间之外的状态。

### CSS3多列

属性 | 描述
--- | ---
column-count | 规定元素应该被分隔的列数。
column-fill | 规定如何填充列。
column-gap | 规定列之间的间隔。
column-rule | 设置所有 column-rule-* 属性的简写属性。
column-rule-color | 规定列之间规则的颜色。
column-rule-style | 规定列之间规则的样式。
column-rule-width | 规定列之间规则的宽度。
column-span | 规定元素应该横跨的列数。
column-width | 规定列的宽度。
columns | 规定设置 column-width 和 column-count 的简写属性。

### CSS3用户界面

属性 | 描述
--- | ---
appearance | 允许您将元素设置为标准用户界面元素的外观
box-sizing | 允许您以确切的方式定义适应某个区域的具体内容。
icon | 为创作者提供使用图标化等价物来设置元素样式的能力。
nav-down | 	规定在使用 arrow-down 导航键时向何处导航。
nav-index | 设置元素的 tab 键控制次序。
nav-left | 规定在使用 arrow-left 导航键时向何处导航。
nav-right | 规定在使用 arrow-right 导航键时向何处导航。
nav-up | 规定在使用 arrow-up 导航键时向何处导航。
outline-offset | 对轮廓进行偏移，并在超出边框边缘的位置绘制轮廓。
resize | 规定是否可由用户对元素的尺寸进行调整。


