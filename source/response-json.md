# 响应json数据

## ResponseVo

```java
public class ResponseVo {

	private int code = 200;
	private String message;
	private Object obj;
	
	public ResponseVo() {
	}
	
	public void success(String message) {
		this.message = message;
	}
	
	public void success(String message, Object obj) {
		this.message = message;
		this.obj = obj;
	}
	
	public void fatal(String message) {
		this.code = 500;
		this.message = message;
	}
	
	public void fatal(String message, Object obj) {
		this.code = 500;
		this.message = message;
		this.obj = obj;
	}
	
	public int getCode() {
		return code;
	}

	public void setCode(int code) {
		this.code = code;
	}

	public String getMessage() {
		return message;
	}

	public void setMessage(String message) {
		this.message = message;
	}

	public Object getObj() {
		return obj;
	}

	public void setObj(Object obj) {
		this.obj = obj;
	}

}
```

## Controller

```java
public void test(HttpServletResponse res) {
    //需要返回到客户端的数据
    User user = new User("imant", 12);

    ResponseVo responseVo = new ResponseVo();
    responseVo.success("测试", user);

    //异常或非法数据
    //responseVo.fatal("测试", user);
    
    RenderUtil.renderJson(responseVo, res);
}
```

## js

```js
$({
    url : xxxx/aaaa,
    type : 'POST',
    data : {
        name : 'imant',
        age : 101
    },
    dataType : 'JSON',
    success : function(data) {
        if (!!data && data.code === 200) {
            //message
            console.log(data.message);

            var user = data.obj;
            var name = user.username;//imant
            var age = user.age;//12
        }
    }
});
```