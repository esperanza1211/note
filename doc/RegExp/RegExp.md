# 正则 - 正则表达式

正则表达式，又称规则表达式。（英语：Regular Expression，在代码中常简写为regex、regexp或RE），计算机科学的一个概念。正则通常被用来检索、替换那些符合某个模式(规则)的文本。

## 正则的写法

在js中，正则是以对象的形式存在的：RegExp，和数组类似，正则对象的创建有两种写法。
- new RegExp()
- //

## 概念

转义字符

- \d : 一个数字
- \D : 一个非数字
- \w : （字母、数字、下划线）中的一个，[0-9a-zA-Z_]
- \W : 非（字母、数字、下划线）中的一个，[0-9a-zA-Z_]
- \s : 一个空格
- \S : 一个非空格
- \b : 一个边界符
- \B : 一个非边界符

量词
{n}
{n,}
{n,m}
+
?
*

修饰符
i
g

子项
()

范围选择
[]

或
|

重复子项
\n : n这里表示一个数字变量
\1,\2,\3

任意字符（不包含\r\n）
.

## 案例
-   去除字符串首尾空格

```
function trim(str) {
    return str.replace(/^\s+|\s+$/g, '');
}
```

-   敏感词过滤

```
var str = '哈哈哈说：“喂喂喂呵呵”';

console.log( str.replace(/哈哈哈|喂喂喂呵呵/g, function(v) {
    var s = '';
    for (var i=0; i<v.length; i++) {
        s += '*';
    }
    return s;
}) );
```

-   找出字符串连续出现次数最多的字符

```
var str = 'jjjjjkkkkkkkkkhhhhhhhhhhjjjjddddddddduuuuuuuueee';

var s = '';
var n = 0;

str.replace(/(.)\1*/g, function(v, v1) {
    console.log(v)
    //v:连续出现的字符串
    if (v.length > n) {
        n = v.length;
        s = v1;
    }
});

console.log(n, s)；

//n:出现次数最多的次数
//s:出现次数最多的字符
```

-   单词首字母大写

```
function ReplaceFirstUper(str) {
    str = str.toLowerCase();
    return str.replace(/\b(\w)|\s(\w)/g, function(m) {
        return m.toUpperCase();  
    });
}
```

-   身份证号码简单校验
