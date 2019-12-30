
# 甘肃云时播

## 服务器登陆 
[（甘肃云时播登陆方法文档）](http://git.pukkasoft.cn/seeingtv_epg/gan-su-mangguo/blob/master/doc/%E4%BA%91%E6%97%B6%E6%92%AD%E7%9B%B8%E5%85%B3%E6%96%87%E6%A1%A3/%E6%93%8D%E4%BD%9C%E6%89%8B%E5%86%8C--EPG%E7%99%BB%E9%99%86%E6%B5%81%E7%A8%8B.doc)
## 简介
- 甘肃的云时播分为两种 : 芒果云时播和广场舞云时播,使用的是一套代码，在代码里通过channelKind参数去判断播放的是广场舞频道还是芒果的频道 

 1. 芒果云时播，播放的都是芒果的内容，可以上下切换频道，左侧滚动条有上下可以切换频道的提示，访问地址为<http://172.30.6.73:8081/cloudLive/page/cloudLive.html>
 2. 广场舞云时播，一部分是芒果的内容，一部分是局方的内容，视频通过我们平台手动上传的，左侧滚动条无上下切换频道的提示,访问地址为<http://172.30.6.73:8081/cloudLive/page/cloudLive.html?channelKind=1>
- 甘肃的云时播版本为EPG与云时播后台和融合平台结合的版本,EPG通过云时播后台获取频道列表和节目单，使用contentCode调用中兴华为播放器进行播放,播控逻辑由EPG进行控制，跳转到点播时需要通过contentCode调用融合平台接口获取节目详情再跳转到芒果对应的详情页面

## 产品形态
[甘肃云时播需求文档](http://git.pukkasoft.cn/seeingtv_epg/gan-su-mangguo/blob/master/doc/%E4%BA%91%E6%97%B6%E6%92%AD%E7%9B%B8%E5%85%B3%E6%96%87%E6%A1%A3/%E7%94%98%E8%82%83%E7%94%B5%E4%BF%A1%E8%99%9A%E6%8B%9F%E4%BA%91%E6%97%B6%E6%92%AD%E4%BA%A7%E5%93%81%E9%9C%80%E6%B1%82%E6%96%87%E6%A1%A3V1.0.docx)

<img src="/Area/GanSu/Cloud/cloud1.png"   width="800" height="450">

## 地址相关
提供给局方的地址platform中HW为华为，ZTE为中兴
```
http://125.74.70.73:18080/cloudLive/page/cloudLive.html?userId={userId}&platform=HW&backUrl={backUrl}
```
