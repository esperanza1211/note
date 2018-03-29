# 正则 - 正则表达式

正则表达式，又称规则表达式。（英语：Regular Expression，在代码中常简写为regex、regexp或RE），计算机科学的一个概念。正则通常被用来检索、替换那些符合某个模式(规则)的文本。

## 正则的写法

在js中，正则是以对象的形式存在的：RegExp，和数组类似，正则对象的创建有两种写法。
- 直接量定义(推荐)：/正则表达式/[修饰符]
- 对象方式：new RegExp(字符串,[修饰符])

##  测试正则表达式

### test

RegExp.test() 是属于正则对象的一个方法，用于检测一段字符串中是否符合正则中的规则

-   用法：\正则\.test(string)

-   返回值: 符合规则 返回true 否则返回false

**注意：当正则有全局搜索标识符，在使用test的时候，每调用一次test，那会记录匹配到的字符的位置，记录在正则对象lastIndex中。如果遇到问题，可以`re.lastIndex = 0`;就会从头开始搜索。**

```
let str = "abc";
let re = /a/;//当前字符串中是否包含a
let re2 = /x/;//当前字符串中是否包含x
console.log(re.test(str));// 输出 true
console.log(re2.test(str));	//输出 false
```

### search

String.search(/a/||str)方法查找某段字符，在大字符串中首次出现的位置

-   参数：search 方法接受两种参数，字符串或者正则对象

-   返回值：如果检索到字符串则返回位置，否则返回 -1

**注意：search和indexOf在传入字符串的时候功能是一样的。search可以接收正则为参数，indexOf不可以**

```
let str = "MiaoV"; 
console.log(str.search(/o/));//3
console.log(str.search(/x/));//-1
console.log(str.search(/m/));//-1 注意，search 对大小写敏感，如果不区分大小写 可以使用修饰符 i
console.log(str.search(/m/i)); // 0  修饰符 i 不区分大小写
```

### match

String.match方法(/a/||str) 用来检索字符串中，用来检索符合正则或者子字符串的值

-   参数：match 方法接受两种参数，字符串或者正则对象

-   返回值:

    *   会把所有符合规律的值，放入一个数组

    *   没有检索到返回null

    *   **如果不加 g 修饰符，则只会匹配一次字符，并且数组上会多出 index(匹配到的字符串所在位置) 和 input(完整的大字符串) 属性**

    *   **如果加 g 修饰符,则为全局匹配，返回的是匹配到的字符串组成的数组**

```
let str = "MiaoWeiQuXue";
console.log(str.match(/i/));//["i", index: 1, input: "MiaoWeiQuXue"]
console.log(str.match(/i/g)); //["i", "i"] 
```

实例：找出所有的数字

```
let str = "Miao2Wei3Qu5Xue";
console.log(str.match(/\d/));//["2", index: 4, input: "Miao2Wei3Qu5Xue"]
console.log(str.match(/\d/g)); // ["2", "3", "5"]
```

### replace

String.match方法(/a/||str,newStr||fn)，用来替换掉匹配的字符串或正则表达式匹配到的内容

*   参数：

    *   第一个参数：字符串或正则表达式

    *   第二个参数：字符串或函数

    *   第二个参数为函数时，该函数必须有返回值，返回值为替换后的内容

*   返回值：替换后新的字符串

```
let str = "Miao212Wei3Qu5Xue";
console.log(str.replace(/\d/,"*"));//Miao*Wei3Qu5Xue
console.log(str.replace(/\d/g,"*"));//Miao*Wei*Qu*Xue
console.log(str.replace(/\d/,function($1,$2,$3){
	console.log($1,$2,$3); //2(正则匹配到的内容) 4(在整个字符串中的位置) Miao212Wei3Qu5Xue(完整字符串)
	return "*"
}));
console.log(str.replace(/\d/g,function($1,$2){
	console.log($1,$2);
	/*
		执行多次：
				第1次：2  4
				第2次：1  5
				第3次：2  6
				第4次：3  10
				第5次：5  13 	
	*/ 
	return "*"
}));
```

实例：利用replace 匹配到所有的数字，并记录所有数字出现的位置
```
let str = "Miao212Wei3Qu5Xue";
let indexArr = [];
let indexArr2 = [];
str.replace(/\d/g,function($1,$2){
	indexArr.push($2);
	return $1;
});
console.log(indexArr);//[4, 5, 6, 10, 13]
// 在这里我们要注意 212 在我们这段正则中被匹配成了三个数字，但很多时候我们会认为这是一个数字，那这样我们就需要使用到量词
// + 量词  匹配 一位或多位
str.replace(/\d+/g,function($1,$2){
	console.log($1);
	/*
		212
		3
		5
	*/
	indexArr2.push($2);
	return $1;
});
console.log(indexArr2); //[4, 10, 13]
```

## 概念

### 转义字符

在正则中有些特殊的符号不能直接书写，这里我们就需要使用转义字符。比如我们要匹配"/"的话，写///肯定没事没啥用的,'/'本身在使用的时候，必须转义写成/\//.这个'' 就是转义符

常用转义字符 | 说明
--- | ---
. | 匹配除换行符(\n)外的任意一个字符(不包含\r\n)
\A | 只有匹配字符串开始处
\b | 匹配一个单词边界，词在[]内时无效。比如我们使用/\bM/g只能在'MiaoV XiaoMei'匹配到'Miaov'中的'M'。在英文中我们会以空格分割单词M\b匹配单词的结尾，\bM匹配单词的开始位置
\B | 匹配非单词边界.和\b相反匹配不是单词边界，也就是在单词中间的字符。\w的左边或右边不是一个\w就存在一个边界符
\d | 匹配一个数字字符. 从0 - 9,10个字符
\D | 匹配一个非数字字符. 非\d之外的字符
\f | 匹配一个换页符
\G | 匹配当前搜索的开始位置
\n | 匹配一个换行符
\r | 匹配一个回车符
\s | 匹配任何空白字符，包括空格、制表符、换页符等等
\S | 匹配任何非空白字符
\t | 匹配一个制表符,及我们按了键盘上的tab键产生的缩进
\w | 匹配包括下划线的任何单词字符. 小写字母a-z加上大写字母A-Z，数字0-9加"_"
\W | 匹配任何非单词字符。非\w的字符
\z | 只匹配字符串结束处
\Z | 匹配字符串结束处或行尾

### 字符范围

当我们需要匹配某个范围内的字符，而不是单一字符是就需要用到范围也就是[]

字符范围 | 说明
--- | ---
[0-9] | 匹配 从0 - 9 的数字,当然也可以写[1-5],[0-3]
[a-z],[A-Z] | 大写和小写的a-z
[0-9a-zA-Z] | 0-9,a-z以及A-Z
[\u4e00-\u9fa5] | 中文区间
^ | 排除
[^0-9] | 排除0-9这个范围的字符
[^a-z0-9] | 匹配任意不在括号中的字符集中的字符

-   | 代表或者，这个不是字符范围，但是不想单拎出来了. `/x|y/` 匹配 x或者y

### 量词

量词{}也叫限定符，设定该规则匹配多少个,比如\d{4}代表匹配4位数字

重复字符 | 说明
--- | ---
{n} | 匹配n个
{n,} | 匹配至少n个，最多不限
{n,m} | 匹配至少n个，最多m次
+ | 匹配至少1个，最多不限，等同于{1,}
? | 匹配至少0个，最多重复1个，等同于{0,1}
* | 匹配至少0个，最多不限，等同于{0,}

修饰符
i
g

### 子项
()

重复子项
\n : n这里表示一个数字变量
\1,\2,\3

### 行首和行尾

字符 | 说明
--- | ---
^ | 行首匹配
$ | 行尾匹配

### 分组与捕获

形式 | 字符 | 说明
--- | --- | ---
捕获某个子项 | \1 | 捕获第一个子项
捕获性分组 | /(\d+)([a-z])/; | 所有的分组都捕获返回
非捕获性分组 | /(\d+)(?:[a-z])/; | 只要在不需要捕获返回的分组加上?:就可以了
嵌套分组 | /(a?(b?(c?)))/; | 从外往内获取
前瞻捕获 | /goo(?=gle)/; | /后面必须是gle才能返回goo
特殊字符捕获 | /[/; | 用\来转义正则里的特殊字符
多行匹配 | /^\d+/gm; | 限定了首位匹配，开启m换行模式

### 贪婪与惰性

模式 | 说明 | 开启方式
--- | --- | ---
贪婪模式 | 从开始一直匹配到结束的地方 | 默认
懒惰模式 | 从开始一旦找到符合的就不再往后找 | 在最后面加?

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

-   [身份证号码简单校验](https://github.com/esperanza1211/note/blob/master/doc/RegExp/%E8%BA%AB%E4%BB%BD%E8%AF%81%E5%8F%B7%E7%A0%81%E7%AE%80%E5%8D%95%E9%AA%8C%E8%AF%81.md)
