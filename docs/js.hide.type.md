JS 隐性类型转换
------------------

这里说的隐性类型转换，是==引起的转换。

如果存在NaN，一律返回false
再看有没有布尔，有布尔就将布尔转换为数字
接着看有没有字符串, 有三种情况，对方是对象，对象使用toString进行转换；对方是数字，字符串转数字；对方是字符串，直接比较；其他返回false
如果是数字，对方是对象，对象取valueOf进行比较, 其他一律返回false
null, undefined不会进行类型转换, 但它们俩相等
这个顺序一定要死记，这是面试时经常问到的。

下面是一些杂题，自己做做

```javascript

0 == undefined

1 == true


2 == {valueOf: function(){return 2}}


NaN == NaN

8 == undefined

1 == undefined

null == {toString: function(){return 2}}

0 == null

null == 1

{ toString:function(){ return 1 } , valueOf:function(){ return [] }} == 1

```