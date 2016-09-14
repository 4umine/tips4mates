## 不进行过滤

### 后台

```java
public void getUserInfo(HttpServletRequest req, HttpServletResponse res) {
    String userId = req.getParameter("userId");
    //user {name:"imant", age:"100", password:"123456"}
    User user = userService.findById(userId);
    ResponseVo responseVo = new ResponseVo();
    responseVo.success("获取用户信息成功", user);

    RenderUtil.renderJson(responseVo, res);
}
```

### js

```js
$.ajax({
    ...
    success : function(data) {
        if (data.code === 200) {
            //{name:"imant", age:"100", password:"123456"}
            console.log(data.obj);
        }
    }
});
```

但其实返回到客户端的用户信息有些属性不能暴露，比如密码，所以要对返回的json进行过滤

## 进行过滤

### 后台

```java
public void getUserInfo(HttpServletRequest req, HttpServletResponse res) {
    String userId = req.getParameter("userId");
    //user {name:"imant", age:"100", password:"123456"}
    User user = userService.findById(userId);
    ResponseVo responseVo = new ResponseVo();
    responseVo.success("获取用户信息成功", user);

    JsonConfig config = new JsonConfig();
    config.setJsonPropertyFilter(new JsonPropertyFilter(false, new String[]{"password"}));
    JSONObject jsonObject = JSONObject.fromObject(responseVo, config);
    RenderUtil.renderJson(jsonObject, res);
}
```

### js

```js
$.ajax({
    ...
    success : function(data) {
        if (data.code === 200) {
            //{name:"imant", age:"100"}
            console.log(data.obj);
        }
    }
});
```

## 自定义JsonPropertyFilter

    JsonPropertyFilter filter = new JsonPropertyFilter(false, new String[]{"password"});
    false：是否过滤集合
    String[]：需要过滤的属性名