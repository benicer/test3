


### 甘肃活动开发备注

1. 甘肃跳转局方订购后返回到专区页面携带的参数为
&transactionID=9999999920190625172708gsdg
20190625172708&result=0&description=%B6%A9%B9%BA%B3%C9%B9%A6&purchaseType=0&expiredTime=
20190625172912&subscriptionExtend=1&subscriptionID=subc01L7221b9fvLNbzy000008777583&
productID=8001013020&productPrice=2000&abstract=b6be538594f522b059e393873d650e5b
使用XEpg.My.parseUrl做参数解析时会报错，所以使用代码里的parseQueryString方法进行解析
```
        var numUrl = (window.location.href).split("&result")[0] || window.location.href;
    	var numUrl2 = decodeURIComponent(numUrl);
    	var param = parseQueryString(numUrl2);  //URL解析成对象
```
2. 局方跳转到专区携带的backUrl里会有参数，如backUrl=http%253A%252F%252F202.100.75.217%253A8080%252Fiptvepg%
252Fframe26%252Fportal.jsp%3Fff%3Drecommend7，用parseQueryString解析时会把ff后面的参数丢失，所以解析backUrl时用XEpg.My.parseUrl()解析
```
            var param2 = XEpg.My.parseUrl();
	        var exitBackUrl = param2.backUrl || '';
	        var mmBackUrl = decodeURIComponent(exitBackUrl);
```
3. 跳转云时播时，因为云时播会把backUrl全部解码成为解码的状态，所以跳转云时播返回时做个判断，如果从云时播回来就不再解析backUrl，用之前存到cookie里的backUrl返回



