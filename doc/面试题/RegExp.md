#   RegExp

*   请用正则校验身份证号码，要求符合15位或18位，末尾可能是X。

>   [身份证号码简单校验](https://github.com/esperanza1211/note/blob/master/doc/RegExp/%E8%BA%AB%E4%BB%BD%E8%AF%81%E5%8F%B7%E7%A0%81%E7%AE%80%E5%8D%95%E9%AA%8C%E8%AF%81.md)

*   使用正则表达式将'I Am A Good Boy'中所有的单词首字母大写。

```
function ReplaceFirstUper(str) {
    str = str.toLowerCase();
    return str.replace(/\b(\w)|\s(\w)/g, function(m) {
        return m.toUpperCase();  
    });
}
```
