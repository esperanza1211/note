#   AJAX

###  前后端（客户端 - 服务端）数据通信

通常我们想获取一个后端数据，需要发送http请求来完成！

- 通过浏览器发送

- 通过一些内置html标签

    link、img、script、iframe、form

- 通过js内置对象

    Image、script、XMLHttpReqeust

- 除了form和XMLHttpReqeust，其他只支持控制get方式发送

- form和XMLHttpReqeust是能够选择get还是post方式，但是form的发送会刷新或新开窗口

- XMLHttpReqeust能够在当前页面不重新渲染的情况下发送get和post请求

##  XMLHttpReqeust 流程
1. 创建`XMLHttpReqeust`对象
2. 监听onload事件
3. 设置请求参数：open()
4. 发送请求：send()

## 1. 创建XMLHttpReqeust对象

该对象是标准浏览器支持对象，不支持低版本的ie6浏览器
        new ActiveXObject('Microsoft.XMLHTTP')

## 2. open(request Method, request URI, is Async)

- request Method: 请求方式，包括（get、post、put、delete、trace、head、options），因为大部分浏览器以及后端基于http1.1的协议，所以除了get、post，其他方式支持并不友好。

- request URI: 请求地址

- is Async: 是否异步

### 异步 & 同步

-   异步
-   同步
-   阻塞
-   非阻塞

1.  异步阻塞
2.  异步非阻塞
3.  同步阻塞
4.  同步非阻塞

首先同步异步于阻塞非阻塞并没有关系。同步异步主要是事情做完以后，如何进行处理、或者说关注的是一种消息通信机制。
同步的情况下，是由处理消息者自己去等待消息是否被触发；
而异步的情况下是由触发机制来通知处理消息者；

阻塞非阻塞，主要是对于请求者而言的。
阻塞：发出请求等待结果返回，然后再处理后续的事情；
非阻塞：发出请求不等待结果返回，可以接着做后续的事情；

    http://miaov.com/index.php/news/newsDetail/nid/82

    todo().on('end', function() {...});

    console.log(a)


## 3. send()

发送http请求

## 4. 监听onload事件

因为ajax推荐使用异步无阻塞模式，当任务完成以后，ajax会通过事件方式通知我们js进行后续的处理。ajax把获取到数据存放在该对象的一个属性之下：`responseText`

ajax对象还可以触发其他的一些事件

    onerror:
    onloadend:
    onload:

有些错误是请求错误，会触发error，有些错误是服务器处理错误，不会触发error，我们既要处理error，同时也要处理服务器错误。

其他属性
- status: 返回的状态码


## get / post

http请求方式，不同请求方式应该有不同的含义，后端通常会按照不同的请求方式做不同的处理和返回

数据的传输方式与http的请求方式没有任何直接关系，主要是看后端从什么地方去解析数据

当我们把数据通过 http 的正文进行发送的时候，要设置提交内容的 类型

对提交的数据进行格式化处理

- `application/x-www-form-urlencoded` ：把提交的数据格式化为 urlencode 格式
- `multipart/form-data` ： 把提交的数据格式化为二进制格式
- `text/plain` ：纯文本

通过`queryString`的方式发送的数据为什么不需要设置格式，`queryString`只支持字符串，但是需要注意的是，一些浏览器（ie）不会对`queryString`的内容做编码（urlencode）处理，所以`queryString`的数据最好能够手动做处理：`encodeURI('字符串')`，post方式数据的格式是通过设置头信息的时候处理的，所以不需要手动去设置数据的编码。


- get
    - 一个请求为主的http请求方式
    - 提交的数据只有字符格式，对一些数据需要做编码处理，否则可能会有乱码问题
    - get会根据请求的url进行缓存，所以如果不需要缓存可以在url的queryString添加随机值
    - 因为get会缓存，所有会对用户提交的数据进行记录，有一定安全隐私泄露风险

- post
    - 一个获取数据为主的http请求方式
    - 提交的数据支持三种基本格式：url编码，二进制，纯文本
    - 提交数据的时候需要同时设置提交方式：头信息 `content-type`
    - 没有缓存问题

- 因为url的长度是有限制，所以通过queryString传递的数据也是有一定限制的，多出的数据会被丢弃
- 通过正文提交的数据，理论上没有限制的

- 因为get方式不支持设置正文，所有get方式只能通过`queryString`来提交数据
- post方式可以通过`queryString`和正文提交数据


## AJAX 基本步骤：

- 初始化ajax对象
- 连接地址，准备数据
- 发送请求
- 接收数据（正在接收，尚未完成）
- 接收数据完成

        //初始化ajax对象
        var xhr = new XMLHttpRequest();
        //在IE6下
        //var xhr = new ActiveXObject('Microsoft.XMLHTTP');
        //连接地址，准备数据
        xhr.open(“方式”,”地址”,是否为异步);
        //接收数据完成触发的事件
        xhr.onload =function(){}
        //发送数据
        xhr.send();

##  ajax数据

通过ajax返回的数据，会保存在ajax对象的对应属性之下，ajax对象在保存这些数据的时候会对这个数据做处理之后再保存的，在使用后端返回的数据之前，对数据进行必要的分析

`responseText`: 保存的永远是字符串类型

可能返回的数据格式：
-   纯字符串
-   html字符串
-   JSON格式字符串
-   xml格式


        const xhr = new XMLHttpRequest();
        xhr.onload = function () {
            // 如果我们接收到是一个xml格式的数据，responseText里面会存储该xml的字符串的内容
            // 但是ajax早期在数据传输的时候，默认传输格式其实就是xml，为了能够更加方便的操作xml，ajax对象提供了一个属性 responseXML，这个属性里面保存的是被解析成对象以后的数据
            // console.log(this.responseText);
            //console.dir(this.responseXML);

            var teachers = [...this.responseXML.getElementsByTagName('teacher')];
            teachers.forEach( teacher => {
                console.log(teacher.getAttribute('name'), teacher.getAttribute('gender'), teacher.textContent)
            } );
            ps[3].innerHTML = '';
        };
        xhr.open('get', '/getXmlData', true);
        xhr.send();

---
        const xhr = new XMLHttpRequest();
        xhr.onload = function () {
            console.log('下载完成');
        };
        /*
        * 我们每次发送请求到服务器，服务器回传数据到客户端，其本质上是一个上传与下载的过程
        * ajax对象下的onprogress事件就是来监听下载的过程，因为上传下载的数据会分包发送，那么这个progress其实会在一个间隔时间内不断的触发，知道上传或下载完成
        * */
        xhr.onprogress = function(e) {
            console.log('progress');
            /*
            * e.total : 当前需要下载的资源的总大小
            * e.loaded: 当前这次progress事件触发的时候已经下载完成的大小
            * */
            console.log(e);
        };
        xhr.open('get', '/public/1.jpg', true);
        xhr.send();

---

上传文件

如果传输的二进制数据，则必须把content-type设置form-data格式，传递也是form-data格式的数据
http://blog.csdn.net/five3/article/details/7181521

        queryString
        username=小明&gender=男

        Content-Type: multipart/form-data; boundary=${bound}

        --${bound}
        Content-Disposition: form-data; name="username"

        小明

        --${bound}
        Content-Disposition: form-data; name="gender"

        男

我们可以通过使用 html5 新增的一个对象 FormData来构建 formdata格式数据，该对象会自动帮助我们生成一个 formdata 格式的数据。

上传数据（非文本，字符型），也就是二进制数据，一定要通过http的正文传输，不能使用queryString，上传二进制数据通过 post。


##  [防止重复发送AJAX请求的解决办法](https://github.com/esperanza1211/note/blob/master/doc/AJAX/%E9%98%B2%E6%AD%A2%E9%87%8D%E5%A4%8D%E5%8F%91%E9%80%81AJAX%E8%AF%B7%E6%B1%82.md)
