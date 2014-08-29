##AngularJs表单验证

ex.
```HTML
<form novalidate name="form">
  <label name="email">Your email</label>
  <input type="email" name="email" ng-model="email" placeholder="Email Address" />
  <label name="password">Your Password</label>
  <input type="password" name="password" ng-model="password" required/>
</form>
```
###Requied
必填项
```HTML
<input type="text" ng-model="***" required />
```
###Minimum length
最小长度
```HTML
<input type="text" ng-model="***" ng-minlength=5 />
```
###Maximum length
最大长度
```HTML
<input type="text" ng-model="***" ng=maxlength=20 />
```
###Matches a pattern
正则匹配
```HTML
<input type="text" ng-pattern="[a-zA-Z]" />
```
###Email
邮箱格式
```HTML
<input type="email" ng-model="***" />
```
###Number
数字
```HTML
<input type="number" ng-model="***" />

<input type="text" ng-model="***" ng-pattern="/^\d+$/" />
```
###Url
<input type="url" ng-model="***" />

###Custome validations自定义验证

####数据到视图的更新 
    - NgModelController#$formatters
####视图到数据的更新
    - NgModelController#$parsers

###获取表单状态
```javascript

formName.inputFieldName.property

/** Unmodified */

formName.inputFiledName.$prostine

/** Modified */

formName.inputFiledName.$dirty

/** Valid */

formName.inputFiledName.$valid

/** Invalid */

formName.inputFiledName.$invalid

/** Errors */

formName.inputFiledName.$error

```