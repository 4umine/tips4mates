# Js模块化写法

## 模块一：登陆Js

```js
// 登陆注册相关js
var passportJs = $.extend({}, passportJs);

//登陆
passportJs.login = function() {
    var username = $('#username').val();
    var password = $('#password').val();

    $.ajax(
        //...
    );
};

//注册
passportJs.register = function() {
    var username = $('#username').val();
    var password = $('#password').val();

    $.ajax(
        //...
    );
};
```

## 模块二：用户Js

```js
// 登陆注册相关js
var userJs = $.extend({}, userJs);

//保存
userJs.saveUser = function() {
    var username = $('#username').val();
    var password = $('#password').val();

    $.ajax(
        //...
    );
};

//修改姓名
userJs.changeUserName = function() {
    var username = $('#username').val();
    var password = $('#password').val();

    $.ajax(
        //...
    );
};
```

## html

```html
<html>
    <head></head>
    <body>
        用户名：<input type="text" id="username"><br>
        密码：  <input type="text" id="password"><br>
        <input type="button" value="登陆" onclick="passportJs.login();">

        <script type="text/javascript" src="../passprot.js"></script>
        <script type="text/javascript" src="../user.js"></script>
    </body>
</html>
```