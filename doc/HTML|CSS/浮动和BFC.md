#   浮动

`float: left/right/none;`

特性：

*   支持宽高
*   在一行显示
*   不设置宽度，由内容撑开
*   会按照制定的方向移动，直到碰到浮动元素，或者父级的边界停止
*   触发BFC
*   脱离文档流
*   元素浮动后，上下margin就不会叠加了

文档流是文档中可显示对象在排列中所占用的位置。

脱离文档流：元素在排列的时候，不再占有位置。

##  clear

`clear: left/right/both/none;`

元素的某个方向上不能有浮动元素

*   如果在元素的前边有对应的浮动元素，元素会折到下一行显示

*   要加在具体有块属性的元素上

*   只对结构里在它前边的元素起效果

##  清浮动

1.  在浮动元素的最下边添加`<div class="clearFix"></div>`
        .clearFix{clear:both;}

2.  在浮动元素的最下边添加`<br clear="all" />`

3.  给浮动元素的父级加`class="clearFix"`
```
.clearFix:after{
    content: "";
    display: block;
    clear: both;
}
```

4.  给浮动元素的父级，触发BFC，在IE低版本触发haslayout
```
#box:before{content: " ";}
//在元素的内容的最开始加一段内容进去，内容写在content里
#box:after{content: " ";}
//在元素的内容的最末尾加一段内容进去，内容写在content里
```

##  浮动注意事项

1.  需要并列在一行的元素，都加浮动

2.  浮动最好在同级元素之间去加

3.  元素浮动之后，如果宽度不需要内容撑开，就设置固定宽度

4.  元素浮动之后，如果高度不需要内容撑开，就给父级清浮动或设置高度

#   BFC
Block Formatting Content    块级格式化上下文

布局环境，规定该环境内盒子的排列，使环境内的元素不会受到环境外元素的影响，也不会让环境内的元素影响到外边。

BFC作用：

1.  包含浮动元素(清浮动)

2.  阻止margin传递

3.  不被浮动元素覆盖

BFC触发条件：

*   float的值不为none

*   overflow的值不为visible

*   display的值为inline-block,table-cell,table-caption

*   position的值为absolute或fixed
