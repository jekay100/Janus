JavaScript程序编码规范
======================

书写规范
-----------

### 将你的代码写在闭包里（匿名函数），并对undefined进行处理; 并采用严格模式

```javascript

    (function( window, ng, undefined ){
        'use strict';
           
    })( window, angular );
    
```

### 注释

* 对方法或类，必须要有注释（ jsdoc 注释方式 ）
* 方法最好有示例
* 单行注释放在表达式上面（不要放在后面）
* 如果业务逻辑复杂，可在方法最前面说明逻辑步骤

```javascript

    /**
     * isEmpty( Object obj )
     * 判断对象是否为空
     * @params obj
     */
     
    /** 
        ex.(示例)
        isEmpty( [] ) => true
     */
      
    var isEmpty = function( /*Object*/ obj ){
        /**
         * 1. 判断基本类型
         * 2. 如果为数组或空对象则为 true
         * 3. 0 也为 true
         * 4. 字符串长度为0 true
         * 5. null 或 Nan 或 undefined 为 true
         */
    
        //判断对象类型
        var type = typeof obj;
        
        //...
        
    };

```

### 结尾“;”

单一个表达式结束，末尾必须加上";"表示结束

### 代码块 "{}"

起始“{”紧跟表达式后面，不要单起一行;

结束 “}”要另起一行（不包括其他符号"],)"）

```javascript

    /*bad*/
    
    if (condition)
    { statements; }
    
    /*good*/
    
    if(condition){
        statements;
    }
    
```

不能省略{}, 即使再简单的代码

```javascript

    /*bad*/
    if( condition )
        statements; 
        
    /*good*/
    if( condition ){
        statements; 
    }
    
```



### 缩进与 Tab

缩进的单位为四个空格;

如果你使用Tab，请在IDE中设置 Tab 的宽度;

### 每行长度

避免每行超过120个字符。

当一条语句一行写不下时,请考虑折行。

在运算符号,最好是逗号后换行。

在运算符后换行可以减少因为复制粘贴产生的错误被分号掩盖的几率。下一行应该缩进8个空格。

```javascript

    /*bad*/
    if( condition ){
    statements;
    }
    
    /*good*/
    if(condition){
        statements;
    }
    
```

### 引号

在JS中使用单引号\';

### 各种空格

* 条件语句后空格

```javascript

    if (true){
        //...
    }
    
```
>

* "(" 无空格，"）" 无空格

```javascript

    /*bad*/
    if ( true )
    
    /*good*/
    if (true)
    
    
```    

* "{" 紧贴着“）”； "}" 前面空格或换行(与表达式头字母对齐)

```javascript

    /*bad*/
    if (true) {
        //...}
    
    /*good*/
    if (true){
        //...
    }
    
    > * 例外
    
    return {
        //...
    };
``` 
 
* "," 后空格，前紧贴

```javascript

    /*bad*/
    var abc = function( a,b,c ){
        //...
    };
    
    var a,b,c;
    
    /*good*/
    var abc = function( a, b, c ){
            //...
    };
     
    var a, b, c;
    
```
    
* ":" 后空格，前紧贴

```javascript

    /*bad*/
    var obj = {
        'a':1,
        'b':2
    }
    
    /*good*/
    var obj = {
        'a': 1,
        'b': 2
    }
    
```
    
* ";" 紧贴无空格

```javascript

    /*bad*/
    var abc = function( a, b, c ){
        //...
    } ;
    
    var a, b, c ;
    
    /*good*/
    var abc = function( a, b, c ){
        //...
    };
    
    var a, b, c;
    
```
    
* 运算符，比较符，赋值符 前后空格

```javascript

    /*bad*/
    var a=1;
    if (a==1){
        a = a+1;
    }
    
    /*good*/
    var a = 1;
    if (a == 1){
        a = a + 1;
    }
    
```

### "," 行末逗号

```javascript

    /*bad*/
    var a = 1
      , b = 2
      , c = 3;
      
    var obj = {
        'a': 1
      , 'b': 2
      , 'c': 3
    };
      
    /*good*/
    var a = 1, 
        b = 2, 
        c = 3;
      
    var obj = {
        'a': 1, 
        'b': 2, 
        'c': 3
    };
    
```

### 参数赋值，单起一行

```javascript

    /*bad*/
    var a, b = 1, c, d = 2;
    
    /*good*/
    var a, c,
        b = 1
        d = 2;
        
    /*better*/
    var a, c;
    var b = 1,
        d = 2;
        
```
    
### 请习惯用（）表示运算的正确顺序

```javascript

    /*bad*/
    5 || false == 5
    
    var a = 6 + + new Date();
    
    /*good*/
    5 || (false == 5)
    
    var a = 6 + ( + new Date() );
    
```   


## 编码规范
----------

### 命名空间

可以用"对象-属性"来模拟命名空间
当然也可以用 function

### 命名规则

* 原则： 以最少的字母达到最容易理解的意义
* 命名应该由26个大小写字母(A .. Z, a .. z)，10个数字(0 .. 9)和_(下划线)组成
* 不要使用中文
* 不要在命名里使用"$"，包括最后一个字符
* 尽量不要使用"_"下划线作为首字母，它有时表示私有，但实际上不提供私有性；

```javascript

    //内部函数使用 _ 
    var a = function(){
        var _b = function(){
        }
    }
    
    //变量的copy 或 演化，但属于短作用域的临时变量，也可以使用
    var a = function( b ){
        var _b = b;
        //...
        return b;
    }
    

```

* 大多数变量和方法名应该以小写字母开始
* 采用骆驼命名规范，若有两个或两个以上单词组成，则第二个以及第N个单词，首字母大写
* 若多个单词，习惯采用动名词形式；一个单词时，要清晰明了的说明意思，具有泛类型；否则请用 动词+module（作用域）来表明；

```javascript

    /** bad */
    var list = function(){}
    
    /** good */
    //当list并不能表示是所有对象的list的时候，请为list加上 module或作用域；
    //即使当前的list已经在某个module或作用域下
    
    var listTalent = function(){}

```   

* 全局常量： 大写，若多个单词"_"用下划线表示连接；

* 全局变量： 全局变量使用g作为前缀，定义在window下。例如gUserName，gLoginTime
> 但建议慎用

* 构造函数名/类目： 首字母大写

* 无意义或临时变量名，可考虑用缩写或加前缀

```javascript

    数组 -> a => aValues
    布尔型 -> b => bFound
    浮点型（ 数字） -> f => fValue
    函数 -> fn => fnMethod
    整型（ 数字） -> i =>iValue
    对象 -> o => oType
    正则表达式 -> re => rePattern
    字符串 -> s => sValue
    变型（ 可以是任意类型） -> v => vValue
    
    //作用域不大临时变量可以简写
    对象 obj, o
    数组 arr, a
    字符串 str, s
    
    //循环变量可以简写，比如：i，j，k等
    for( var i in arr ){
        //...
    }
    
```

### 声明变量

* 每个变量必须申明
* 方法（function）声明必须使用 var;
* 除了构造函数和时间（Date）, 尽量不要用 new 来声明

> 使用 {}, [] 替代 new Object(); new Array();

* 尽量在函数的顶部声明变量
* 尽量不要在循环语句里声明变量

```javascript

    /*bad*/
    function abc (){
    };
    
    var abc = new Function(){};
    
    /*good*/
    var abc = function(){
    };

```

* 不要在条件语句中声明变量

```javascript
    
    /*bad*/
    if (true){
        var abc = false;
        //...
    }
    
    /*good*/
    var abc;
    if (true){
        abc = false;
        //...
    }

```

### 函数声明要用表达式，不使用直接声明

```javascript

    //not good 
    function a ( b ){
        //...
    }
    
    //bad
    var a = new Function("b", "//...");
    
    //good
    var a = function(){
        //...
    }
    
    //http://justjavac.com/named-function-expressions-demystified.html

```

### 不要使用 with

### 慎用 eval

### 避免使用 continue

### for-in 循环

* 只用于 object/map/hash 的遍历
* 对 Array 用 for-in 循环有时会出错. 因为它并不是从 0 到 length - 1 进行遍历, 而是所有出现在对象及其原型链的键值
* 若一定要用 for in 来遍历数组，通过使用 hasOwnProperty 来区分对象成员

```javascript
    
    /*bad*/
    for (var item in arr){
        //...
    } 
    
    /*good*/
    for (var item in arr){
        if (arr.hasOwnProperty(item)){
            //...
        }
    }
    
    /*better*/
    for (var item in arr) if (arr.hasOwnProperty(item)){
        //...
    }

```

### for 循环

```javascript

    for (initialization; condition; update) {
        statements;
    }

```

不要在 condition 中出现运算，或声明

```javascript

    var arr = [1,2,3,4,5];
    
    /*bad*/
    for (var i=0; i<arr.length; i++){
        //...
    }
    
    /*good*/
    for (var i = 0, l = arr.length; i < l; i++){
        //...
    }
```

### 不使用 void 

它令人困惑，而且没什么用

### =

在 if 和 while 中不期望看到它

```javascript

    /*bad*/
    if( a = b )
    
    //其实你可能表示的意思是
    if( a == b )
    
    //如果一定要表示 赋值，请带上（）
    if((a = b))
```

### 三元表达式

尽量避免三层或三层以上的三元表达式套用

### 不要使用自增（++）和自减（--）运算符，用+=和-=代替

除了在 for 循环中的控制语句

### 不要去封装基本类型

```javascript
    
    //bad
    var x = new Boolean(false); 
    if (x) {   
        alert('hi');
    }
    
    //也许你的意思是
    var x = Boolean(0); 
    if (x) { 
        alert('hi');
    }
    
```

### 不要使用"相等"（==）运算符，只使用"严格相等"（===）运算符

## 优化代码，让你的代码尽量优雅
=========

### '||', '&&'

```javascript

   /**
    * 几乎所有语言中||和&&都遵循“短路”原理，
    * 如&&中第一个表达式为假就不会去处理第二个表达式，而||正好相反。
    * js也遵循上述原则。
    * 当||时，找到为true的分项就停止处理，并返回该分项的值，否则执行完，并返回最后分项的值。
    * 当&&时，找到为false的分项就停止处理，并返回该分项的值。
    **/
    
    //	var a = "" || null || 3 || 4;//3
    //	var b = 4 && 5 && null && "0";//null

```

#### || 通常用于设置默认值

```javascript

    var b = function(/*String*/ a){
        if( a ){
            a = 'Hunteron';
        }
        
        a = a ? a : 'Hunteron';
        
        a = a || 'Hunteron';
    }

```

#### && 通常用来调用函数并执行

```javascript

    var b = function(/*Function*/ fn){
        if( !fn ){
            fn();
        }
        
        fn && fn();
    }
```

### 假值和条件语句的配合使用

```javascript
    
    //如果你想检查字符串是否为 null 或空:
    if (y != null && y != '') {
        //...
    }
    
    //这样也很好
    if (y) {
        //...
    }
    
    //但这样会更好
    y || （function(){
        //...
    })();

```


