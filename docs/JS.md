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
    
    if ( condition )
    { statements; }
    
    /*good*/
    
    if( condition ){
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

避免每行超过80个字符。

当一条语句一行写不下时,请考虑折行。

在运算符号,最好是逗号后换行。

在运算符后换行可以减少因为复制粘贴产生的错误被分号掩盖的几率。下一行应该缩进8个空格。

```javascript

    /*bad*/
    if( condition ){
    statements;
    }
    
    /*good*/
    if( condition ){
        statements;
    }
    
```

### 引号

在JS中使用单引号\';

### 各种空格

* 条件语句后空格

```javascript

    if ( true ){
        //...
    }
    
```
>

* "(" 右空格，"）" 左空格

```javascript

    /*bad*/
    if (true)
    
    /*good*/
    if ( true )
    
```    

* "{" 紧贴着“）”； "}" 前面空格或换行(与表达式头字母对齐)

```javascript

    /*bad*/
    if ( true ) {
        //...}
    
    /*good*/
    if ( true ){
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
    var abc = function( a,b,c ){
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
    var abc = function( a,b,c ){
        //...
    };
    
    var a, b, c;
    
```
    
* 运算符，比较符，赋值符 前后空格

```javascript

    /*bad*/
    var a=1;
    if( a==1 ){
        a = a+1;
    }
    
    /*good*/
    var a = 1;
    if( a == 1 ){
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
        b = 2 , 
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
        
    /*btter*/
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
    5 || ( false == 5 )
    
    var a = 6 + ( + new Date() );
    
```   


## 编码规范
----------








