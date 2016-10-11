## 微信公众号JSSDK接口权限验证配置

### 代码中调用

```java
public ModelAndView credentialsPage(HttpServletRequest request) {
    //获取配置参数appId，timestamp，nonceStr
    WechatConfig config = tokenService.getConfigByAppid(WechatConstant.APPID, WechatConstant.APPSECRET);
    //通过上面参数生成签名signature
    String signature = WechatSign.sign(config, request);
    
    ModelAndView mv = new ModelAndView();
    //页面使用
    mv.addObject("config", config);
    mv.addObject("signature", signature);
    mv.setViewName("/mobile/fillupfile");
    
    return mv;
}
```

### jsp使用

```html
<%-- 微信授权参数 --%>
<input id="appid" type="hidden" value="${config.appId }">
<input id="timestamp" type="hidden" value="${config.timestamp }">
<input id="nonceStr" type="hidden" value="${config.nonceStr }">
<input id="signature" type="hidden" value="${signature }">

<!-- 注意js导入顺序 -->
<script src="${path}/js/jquery.min.js" type="text/javascript" ></script>
<!-- 微信官方api -->
<script src="${path}/js/jweixin-1.0.0.js" type="text/javascript" ></script>
<!-- config接口注入权限配置（自定义） -->
<script src="${path}/js/mobile/wechatJsApi.js" type="text/javascript" ></script>
```

### config接口js
```js
/*
 * 微信js api
 * 
 * 文档
 * http://mp.weixin.qq.com/wiki/7/aaa137b55fb2e0456bf8dd9148dd613f.html
 */

wx.config({
    debug: 		true,
    appId: 		$('#appid').val(),
    timestamp: 	$('#timestamp').val(),
    nonceStr: 	$('#nonceStr').val(),
    signature: 	$('#signature').val(),
    jsApiList: [
                'checkJsApi',
                'onMenuShareTimeline',
                'onMenuShareAppMessage',
                'onMenuShareQQ',
                'onMenuShareWeibo',
                'onMenuShareQZone',
                'hideMenuItems',
                'showMenuItems',
                'hideAllNonBaseMenuItem',
                'showAllNonBaseMenuItem',
                'translateVoice',
                'startRecord',
                'stopRecord',
                'onRecordEnd',
                'playVoice',
                'pauseVoice',
                'stopVoice',
                'uploadVoice',
                'downloadVoice',
                'chooseImage',
                'previewImage',
                'uploadImage',
                'downloadImage',
                'getNetworkType',
                'openLocation',
                'getLocation',
                'hideOptionMenu',
                'showOptionMenu',
                'closeWindow',
                'scanQRCode',
                'chooseWXPay',
                'openProductSpecificView',
                'addCard',
                'chooseCard',
                'openCard'
                ]
});

```