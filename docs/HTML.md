#HTML编码规范
##目录

##通用代码风格
* 每次缩进四个空格，不要使用tab键进行缩进，也不要把tab键以及空格混合起来进行缩进。单纯的使用空格进行缩进就好了.
```html 

<ul>
    <li>Fantastic</li>
    <li>Great</li>
</ul>

```
* 只使用小写，包括标签名、属性名、属性值（一些可以自定义的字符串属性值除外）.
```html
<!-- 不推荐 -->
<A HREF="/">Home</A>

<!-- 推荐 -->
<img src="google.png" alt="Google">

```

##通用Meta规则
* 确保你的IDE使用的是UTF-8编码来保存文件的，且不要带上BOM。在定义页面的编码时使用<meta charset="utf-8"> 就好了。在样式表文件里不用去声明UTF-8编码什么的。

* 在需要地地方进行注释。

* 用 TODO 来标志代码中需要完善的地方
```html

<!-- TODO: remove optional tags -->
<ul>
  <li>Apples</li>
  <li>Oranges</li>
</ul>
```
