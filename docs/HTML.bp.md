#HTML最佳实践
##目录

##保持标签闭合
```
<!--bad-->
<li>Some text here.  
<li>Some new text here.  
<li>You get the idea.

<!--good-->
<ul>  
	<li>Some text here. </li>  
	<li>Some new text here. </li>  
	<li>You get the idea. </li>  
</ul> 
```

##不要使用内联样式
```
<!--bad-->
<p style="color: #CCC; font-size:16px; font-family: arial">An example to illustrate inline style in html</p>

<!--good-->
<p class="html_bp">An example to illustrate inline style in html</p>
.html_bp{
	color:#CCC;
	font-size:16px;
	font-family: arial;
}

<!--bad-->

<!--good-->
```

##使用连续的标题
```
<!--bad-->
<h1>This is the topmost heading</h1>
<h3>This is a sub-heading underneath the topmost heading</h3>

<!--good-->
<h1>This is the topmost heading</h1>
<h2>This is a sub-heading underneath the topmost heading</h2>
```

##在合适的地方使用合适的标签
HTML标签是构造规范内容结构的关键。例如，`<em>`标签用来强调重点内容。`<p>`标签适用于突出文章段落。如果想要在段落间加空行，就不要使用`<br/>`标签。
'''
<!--bad-->
<p>段落一内容<br/>
    段落二内容</p>
<!--good-->
<p>段落一内容</p>
</p>段落二内容</p>
```
