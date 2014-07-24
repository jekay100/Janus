#JavaScript程序编码规范

### 将你的代码写在闭包里，并对undefined进行处理; 并采用严格模式
```
(function( window, ng, undefined ){
    'use strict';
       
})( window, angular );
````

### 注释

*对方法或类，必须要有注释（ jsdoc 注释方式 ）
*方法最好有示例
*单行注释放在表达式上面（不要放在后面）
*如果业务逻辑复杂，可在方法最前面说明逻辑步骤

···
/**
 * isEmpty( Object obj )
 * 判断对象是否为空
 * @params obj
 */
 /** ex.(示例)
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
    ...
};
···

### 结尾“;”

单一个表达式结束，末尾必须加上";"表示结束

### 代码块 "{}"

起始“{”紧跟表达式后面，不要单起一行;
结束 “}”要另起一行（不包括其他符号"],)"）

```
/** bad */

if ( condition )
{ statements; }

/** good */
if( condition ){
    statements;
}

···







