## jQuery
### cssHooks
    $.cssHooks
>   直接向 jQuery 中添加钩子，用于覆盖设置或获取特定 CSS 属性时的方法，目的是为了标准化 CSS 属性名或创建自定义属性。

    // 新增一个 miaov 的样式属性
    $.cssHooks['miaov'] = {
        // 获取该属性的时候执行get方法
        get: function() {
            return '就是不给你看';
        },
        // 设置该属性的时候执行set方法
        set: function(element, value) {
            //console.log('我被调用了')
            //console.log(this);
            //console.dir(arguments);
            var arr = value.split(',');
            element.style.width = arr[0];
            element.style.height = arr[1];
            element.style.background = arr[2];
        }
    };

    //console.dir( $.cssHooks );

    document.onclick = function() {

        /*
        * 自定义一个css属性：miaov，设置这个属性以后，那么就会给元素设置宽，高，背景色
        * 我们可以通过jq提供了一个接口 $.cssHooks 来设置
        *
        * 当我们去调用css方法的时候，会在 $.cssHooks中去查找是否有miaov这个属性存在，如果我们是设置该属性的值，那么就会调用 $.cssHooks.miaov.set()
        * */
        //$('div').css('miaov', '100px,100px,red');
        //console.log( $('div').css('miaov') );

    }

    var cssHooks = {
        miaov: {
            set: function(ele, value) {
                console.log(ele, value)
                var arr = value.split(',');
                ele.style.width = arr[0];
                ele.style.height = arr[1];
                ele.style.background = arr[2];
            }
        }
    };

    var div = document.querySelector('div');
    //css( div, 'background', 'red' );
    css(div, 'miaov', '100px,100px,red');

    function css(obj, attr, value) {

        //obj.style[attr] = value;

        // console.log( cssHooks[attr] )

        if ( cssHooks[attr] ) {
            cssHooks[attr].set(obj, value);
        } else {
            obj.style[attr] = value;
        }
    }

----
### cssNumber
    
----
### wrap() || unwrap()
    $().wrap(html|element|fn)
>   把所有匹配的元素用其他元素的结构化标记包裹起来。

    $().unwrap()
>   这个方法将移出元素的父元素。这能快速取消 .wrap()方法的效果。匹配的元素（以及他们的同辈元素）会在DOM结构上替换他们的父元素。

    var ul = document.querySelector('ul');

    wrap( ul, 'div' );
    unwrap( ul );

    function wrap(element, parentElement) {
        var parentElement = document.createElement(parentElement);
        element.parentNode.insertBefore(parentElement, element);
        parentElement.appendChild(element);
    }

    function unwrap(element) {
        var parentElement = element.parentNode;
        var children = parentElement.children;
        for (; children.length; ) {
            parentElement.parentNode.insertBefore(children[0], parentElement);
        }
        parentElement.parentNode.removeChild(parentElement);
    }
    
----

### classname
    $().hasClass(class)
>   检查当前的元素是否含有某个特定的类，如果有，则返回true。

    $().addClass(class)
>   为每个匹配的元素添加指定的类名。

    $().removeClass(class)
>   从所有匹配的元素中删除全部或者指定的类。

    $().toggleClass(class)
>   如果存在（不存在）就删除（添加）一个类。
 

     var arr = ['box', 'box', 'box1', 'box', 'box2', 'box1'];

        var newArr = (function() {
            var tempArr = [];
            arr.forEach( function(item) {
                if ( !tempArr.includes(item) ) {
                    tempArr.push(item);
                }
            } );
            return tempArr;
        })();

        var newArr = [...new Set(arr)];

        console.log(newArr);

        var divs = document.querySelectorAll('div');

        console.log( hasClass(divs[0], 'box') );

        addClass( divs[1], 'box' );
        addClass( divs[2], 'box' );
        addClass( divs[3], 'box' );

        removeClass( divs[2], 'box' );

        document.onclick = function() {
            toggleClass(divs[0], 'box');
        };

        function hasClass(element, classname) {
            var classes = element.className.split(' ');
            return classes.includes(classname);
        }

        function addClass(element, classname) {
            if (element.className == '') {
                element.className = classname;
                return;
            }
            if ( !hasClass(element, classname) ) {
                element.className += ' ' + classname;
            }
        }

        function removeClass(element, classname) {
            if (element.className != '') {
                element.className = element.className.split(' ').filter( function(item) {
                    return item != classname;
                } ).join(' ');
            }
        }

        function toggleClass(element, classname) {
            if ( hasClass(element, classname) ) {
                removeClass(element, classname);
            } else {
                addClass(element, classname);
            }
        }
        
----

### DOM操作
    $()
    有很多作用
    空
        返回空的jq对象
    字符串
        不包含<>
            选择器
        包含<>
            创建元素
    对象
        数组对象
            把数组的每一个赋值给jq对象每一个属性
        非数组对象
            jq对象第0个就是该对象值
    node
        jq对象的第0个属性就是该节点对象
    函数
        把该函数绑定到DOMContentLoaded和load中
            
    类似window.onload = function(){}
        DOMContentLoaded:结构加载完成
        load：资源（包括图片）加载完成
        
----

### 表单
#### 数据交换
>    我们js通常会和其他各种不同类型的数据进行打交道，比如html、css、xml、json、url、queryString(url？search)，formData，所以我们一定要清楚对不同格式的字符串的各种操作：转换

    jQuery.param( obj )
    把对象转成（序列化）成字符串（url查询字符串queryString）
    queryString: key=value&key1=value1...
    

    $('button')[0].onclick = function () {

        /*
        * location : url对象
        *   我们通常把location.search称为：查询字符串
        * */
        console.dir(location.search);

        console.log( $.param({a:1,b:2}) );//a=1&b=2
    }

    $('button')[1].onclick = function() {
        // 后期我们会把表单中数据通过ajax提交：username=..&password=...

        var str = $('form').serialize();

        console.log(str, JSON.stringify(str));
        //username=1&password=1&age=1 "username=1&password=1&age=1"

        var str2 = $('form').serializeArray();

        console.log(str2, JSON.stringify(str2));
        //"[{"name":"username","value":"1"},{"name":"password","value":"1"},{"name":"age","value":"1"}]"
    }
    
----

### data
    $().data([key],[value])
>   在元素上存放或读取数据,返回jQuery对象。

    console.log( $('div')[0].dataset );
    $('div')[0].dataset.age = 30;

    // 不推荐直接给对象添加自定义属性
    $('div').index = 1

    $('div').data('index', 1);

    setTimeout(function() {
        console.log( $('div').data('index') );
    }, 2000);
    
----

### 事件
    $().on(events,[selector],[data],fn)
>   在选择元素上绑定一个或多个事件的事件处理函数。

>   `.on()`方法绑定事件处理程序到当前选定的jQuery对象中的元素。在jQuery 1.7中，`.on()`方法 提供绑定事件处理程序所需的所有功能。帮助从旧的jQuery事件方法转换，see `.bind()`, `.delegate()`, 和 `.live()`. 要删除的.on()绑定的事件，请参阅`.off()`。要附加一个事件，只运行一次，然后删除自己， 请参阅`.one()`。

    /*
    * 事件绑定
    * */
    $('button').on('click', function () {

            $('li').off();
            $('li').off('mouseover');

            $('p').off('click.a');
        $('p').off('click.a.b');
    });

    $('li').on('mouseover', function () {
        console.log(1);
    });
    $('li').on('click', function () {
        console.log(2);
    });

    $('p').on('click.a', function() {
        console.log('p1');
    });
    $('p').on('click.a.b', function() {
        console.log('p1-1');
    });
    $('p').on('click.b', function() {
        console.log('p2');
    });
    
----

### 事件对象
- 在jq中事件函数的第一个参数也是事件对象
- 但是jq中的事件对象是经过处理的对象，不是原生事件对象
- 但是jq又预留一个属性`originalEvent`，存的就是原生对象

在jq中
- 通过`originalEvent`可以得到原生事件对象
- 阻止冒泡使用：`event.stopPropagation()`
- 阻止默认行为：`event.preventDefault()`  
- `return false`在jq中既可以阻止冒泡还可以阻止默认行为
- jq中事件函数中的`this`指向原生的对象

> 在jq中除了通过`on`来绑定函数以外，还可以通过其他一些别名方法来绑定:`click()`,`mouseover()`....这些方法其实只是一个别名:`on('click')`


### remove 与 detach 区别
    $().remove([expr])
>   从DOM中删除所有匹配的元素。
    这个方法不会把匹配的元素从jQuery对象中删除，因而可以在将来再使用这些匹配的元素。
    **但除了这个元素本身得以保留之外，其他的比如绑定的事件，附加的数据等都会被移除。**

    $().detach([expr])
>   从DOM中删除所有匹配的元素。
    这个方法不会把匹配的元素从jQuery对象中删除，因而可以在将来再使用这些匹配的元素。
    **与`remove()`不同的是，所有绑定的事件、附加的数据等都会保留下来。**
    
----

### 运动
    $().animate(params,[speed],[easing],[fn])
>   用于创建自定义动画的函数。
*   这个函数的关键在于指定动画形式及结果样式属性对象。这个对象中每个属性都表示一个可以变化的样式属性（如“height”、“top”或“opacity”）。注意：所有指定的属性必须用骆驼形式，比如用marginLeft代替margin-left.
*   而每个属性的值表示这个样式属性到多少时动画结束。如果是一个数值，样式属性就会从当前的值渐变到指定的值。如果使用的是“hide”、“show”或“toggle”这样的字符串值，则会为该属性调用默认的动画形式。

    $("#go").click(function(){
        $("#block").animate({ 
            width: "90%",
            height: "100%", 
            fontSize: "10em", 
            borderWidth: 10
        }, 1000 );
    });

    $('#div1').animate({
        width: 200
    }).animate({
        height: 200
    }).animate({
        left: 100
    }).animate({
        top: 100
    });

    $('#div1').animate({
        width: 200
    });
    $('#div1').animate({
        height: 200
    });
    $('#div1').animate({
        left: 100
    });
    $('#div1').animate({
        top: 100
    });
    
----
    $().show([speed,[easing],[fn]])
>   显示隐藏的匹配元素

    $().hide([speed,[easing],[fn]])
>   隐藏显示的元素

    $().slideDown([speed],[easing],[fn])
>   通过高度变化（向下增大）来动态地显示所有匹配的元素，在显示完成后可选地触发一个回调函数。

    $().slideUp([speed],[easing],[fn])
>   通过高度变化（向上减小）来动态地隐藏所有匹配的元素，在隐藏完成后可选地触发一个回调函数。

----

### 运动队列
[slideDown,slideUp,slideDown,slideUp]

jq采用的队列形式，每次都会把运动函数push到数组队列中，然后从队列头开始运动

    $('button').hover(function () {
        $('#div1').slideDown();
    }, function () {
        $('#div1').slideUp();
    })

    $('button').eq(0).click(function() {
        $('#div1').animate({
            width: 200
        }, 3000).animate({
            height: 200
        }, 3000).animate({
            left: 100
        }, 3000).animate({
            top: 100
        }, 3000)
    });

    $('button').eq(1).click(function () {
        /*
        * stop: 停止当前正在进行的运动
        *   第一个参数：是否清空队列
        *   第二个参数：是否把当前的运动值设置为当前目标点
        * */
        $('#div1').stop(true, true);
    })
    
----

### tween
引入`jquery.easing.1.3.js`文件

    $('button').click(function () {
        $('#div1').animate({
            width: 200,
            height: 200,
            left: 100,
            top: 100
        }, {
            duration: 600,
            easing: 'easeOutBounce'
        })
    })