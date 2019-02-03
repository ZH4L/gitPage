---
title: js中的一些简写操作
date: 2019-02-03 14:06:37
categories:
    - javascript
tags:
    - javascript
---

自从这个博客搭建完，写了一篇怎么搭建hexo后，就再也没动过了，主要是不知道该写点什么（大概是自己的技能掌握的不够全面和深入，没有什么可以拿出来写写的）。
这篇就把工作中常常用到的一些js的简写方法记录一下吧，有些简写可以大大提高代码的简洁性，不过也会造成因为某些维护者不知道这种语法导致的维护困难。

### 快速给变量赋默认值
{% codeblock lang:javascript line_number:false %}
let fun = (param) => {
    param = param || 5;
    console.log(param);
}
fun(); // -> 5

// 等同于
let fun = (param) => {
    if(param === undefined) {
        param = 5;
    }
    console.log(param);
}
fun(); // -> 5
{% endcodeblock %}
`param = param || 5;`在这里的作用相当于将param这个参数的默认值设置成5（这种说法不太严谨）
在js中，`undefined、null、数字0、NaN、空字符串""`等会隐式转换成`false`，相当于`undefined==false`，所以在`||`左边为false时，就会取它右边的值。
{% blockquote %}
在es6中，新增了函数参数默认值的写法，如下：
{% codeblock lang:javascript line_number:false %}
let fun = (param=5) => {
    console.log(param);
}
fun(); // -> 5
fun(1); // -> 1
fun(0); // -> 0
fun(undefined); // -> 5
fun(false); // -> false
{% endcodeblock %}只有在参数为`undefined`的时候才会是默认值
{% endblockquote %}

### if判断简写
{% codeblock lang:javascript line_number:false %}
typeof fun === 'function' && fun();

// 等同于
if(typeof fun === 'function') {
    fun();
}
{% endcodeblock %}
`&&`操作需要左边的为true，才会执行右边的语句。

### 判断非空
{% codeblock lang:javascript line_number:false %}
if(!data) {
    ...
}

// 等同于
if(data === undefined || data === null || data === 0 || data === false || data === NaN || data === "") {
    ...
}
{% endcodeblock %}
详见第一条，隐式类型转换。

### 快速转成布尔值
{% codeblock lang:javascript line_number:false %}
let a = 0;
console.log(!!a); -> false
a = null;
console.log(!!a); -> false
a = "abc";
console.log(!!a); -> true
a = function() {};
console.log(!!a); -> true
{% endcodeblock %}
`!`为取反操作，`!!`负负得正。

### 深拷贝
{% codeblock lang:javascript line_number:false %}
let data = JSON.parse(JSON.stringify(res));
{% endcodeblock %}

### 快速取当前时间戳
{% codeblock lang:javascript line_number:false %}
let timestamp = +new Date(); // -> 1549179377368

// 等同于
let timestamp = new Date().valueOf();
{% endcodeblock %}


写下来怎么好像都是隐式类型转换的东西。。。说明要正确理解`==`和`===`呐。