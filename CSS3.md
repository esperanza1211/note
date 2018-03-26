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
