#CSS最佳实践
##目录

##命名
css的命名也讲究命名要有意义，命名要尽可能短但是要足够表达含义；命名的词用连字符连接。
```css
/*bad*/
#navigation{
}
.demoimage{
}
.error_status{
}
/*good*/
#nav{
}
.demo-image{
}
.error-status{
}
```

##css选择器
不同的标签类型尽可能不用相同的css类名；尽可能不用标签类型选择器，用css类名和ID足够定义css，因为ID是可以唯一确定Dom元素的，而css类是不推荐用于不同的标签的；另外应该少用ID选择器定义，因为ID的唯一性使得定义的css无法重用。
```css
/*bad*/
ul#menus{
}
div.info{
}
/*good*/
.main-menus{
}
.info{
}
```

##属性名称和值的定义精简
css的某些属性定义可以可以分拆为各个独立项，比如padding，border, margin, background, font等，虽然分拆定义的可读性会好一些，但是就目前的经验来看，前端工程师们对这些常用的css理解程度足够好，合并后的定义不会对可读性带来影响，反而代码更简洁；此外对属性值为0的单位可以省略，在0后面添加入px em cm等单位是毫无意义的；对小数值可以省略小数点前的0；url值两端的引号可以省略。
```css
/*bad*/
border-top-style: none;
font-family: palatino, georgia, serif;
font-size: 100%;
line-height: 1.6;
padding-bottom: 2em;
padding-left: 1em;
padding-right: 1em;
padding-top: 0;
margin: 0.8em;
background: #00FF00 url('bgimage.gif') no-repeat fixed top;
/*good*/
border-top: 0;
font: 100%/1.6 palatino, georgia, serif;
padding: 0 1em 2em;
margin: .8em;
background: #00FF00 url(bgimage.gif) no-repeat fixed top;
```

##css代码的格式
漂亮统一的代码格式可以提高代码的可读性和可维护性，css的最佳代码格式主要有以下几点：定义顺序以字母序排列，不考虑浏览器前缀；定义以分号结束；属性名称定义的分号后添加一个空格。

```css
/*bad*/
background: fuchsia;
border-radius: 4px;
border: 1px solid;
-moz-border-radius:4px;
text-align: center;
text-indent:2em;
-webkit-border-radius: 4px;
color: black
/*good*/
background: fuchsia;
border: 1px solid;
-moz-border-radius: 4px;
-webkit-border-radius: 4px;
border-radius: 4px;
color: black;
text-align: center;
text-indent: 2em;
```

##重设(reset)
全局重设可以确保一个网站在所有浏览器保持统一的外观。完全不一样的浏览器会在一个网站上应用自己的默认设置，这可能导致一个网站在不同的浏览器有不同的界面表现.
```css
/*bad*/
*{
  margin: 0;
  padding: 0;
}
/*good*/
h1, h2, h3, h4, h5, h6{
  font-size: 100%;
  font-weight: normal;
}
```
##避免写兼容某个浏览器的css代码
避免写特定浏览器兼容代码，这里说的特定浏览器主要指的是万恶的IE系列浏览器，IE6，7尤为严重。碰到浏览器兼容问题，首先考虑的是能否换一种其它的解决方案，如果没有合适的解决方案，记得单独写一个css文件给这些特定的浏览器，不要把兼容代码和常规代码混合，这样方便代码的维护，如果后期不支持这些老旧浏览器，可以直接删除这些单独的css文件即可。
```css
/*bad*/
.bb{
height:32px;
background-color:#f1ee18;/*所有识别*/
.background-color:#00deff\9; /*IE6、7、8识别*/
+background-color:#a200ff;/*IE6、7识别*/
_background-color:#1e0bd1;/*IE6识别*/
}
```
```html
<!--good-->
<!--[if IE 6]>
<link rel="stylesheet" type="text/css" href="css/ie6.css" />
<![endif]-->
<!--[if IE 7]>
<link rel="stylesheet" type="text/css" href="css/ie7.css" />
<![endif]-->
```






