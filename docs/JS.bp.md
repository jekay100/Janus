#Make It Understandable
变量和函数选择容易理解，较短的单词命名

###不好的变量名
`x1 fe2 bqne`
`incrementerForMainLoopWhichSpansFromTenToTwenty`
`createNewMemberIfAgeOverTwentyOneAndMoonIsFull`
###好的变量名
`isLegalAge()`

#避免全局变量
全局变量是魔鬼

问题：所有全局变量都可以被访问；访问不受控制，页面任何东西都可以被覆盖
```
var current = null;
var labels = {
	'home': 'home',
	'articles': 'articles',
	'contact': 'contact'
};
function init() {
	
};
function show() {
	current = 1;
};
function hide() {
	show();
};
```