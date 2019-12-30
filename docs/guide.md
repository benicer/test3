
# 海南修改开机广告地址方123
## 背景介绍
* 海南机顶盒在开机时会有一个开机广告页面，这个页面由局方设置，展现节目的海报，用户点击时跳转到对应专区里的节目详情页
+ 我们提供了一个中转页面，用户点击开机广告跳转到中转页面，然后再通过中转页面里面的代码跳转到指定的节目详情页

## 海南环球专区
- 中转页访问地址: http://10.255.7.4:8090/hainanIPTV/hainanUnifiedIPTVCommon/page/toggleUrl.html 

### 操作流程
1. 驻地运营提出12月1日-12月5日开机广告更换为蜘蛛侠
2. 访问海南环球搜索页面
http://36.101.204.156:8090/hainanIPTV/HainanTest/page/w-search.html
3. 搜索节目蜘蛛侠
4. 点击蜘蛛侠跳转到蜘蛛侠详情页面
5. 截取蜘蛛侠链接，截取详情地址
<font color="#dd0000">
detail.html?contentCode=00040000001015209304604703850000
&categoryCode=00040000000514644059002445000000
&parentCode=00040000000514561071568685000000</font><br />
6. 打开toggleUrl.html，修改代码里的跳转链接，并修改currentTime时间判断
7. 上传代码到测试环境
http://36.101.204.156:8090/hainanIPTV/HainanTest/page/index.html
通过
http://36.101.204.156:8090/hainanIPTV/HainanTest/page/toggleUrl.html
访问，如果跳到指定详情页则代码正确
8. 发包更新到现网

## 海南华数专区
* 中转页访问地址:
http://10.255.53.2:8090/epg/page/toggleUrl.html

### 操作流程
1. 驻地运营提出12月1日-12月5日开机广告更换为蜘蛛侠
2. 访问海南华数搜索页面
http://124.225.67.203:8090/epg/page/w-search.html
3. 搜索节目蜘蛛侠
4. 点击蜘蛛侠跳转到蜘蛛侠详情页面
5. 截取蜘蛛侠链接，截取详情地址
<font color="#dd0000">
detail.html?contentCode=00040000001015209304604703850000
&categoryCode=00040000000514644059002445000000
&parentCode=00040000000514561071568685000000</font>
6. 对取到的链接进行编码
6. 打开toggleUrl.html，修改代码里的跳转链接，将
<font color="#dd0000">
entryIndex.html?targetUrl=detail.html%3fcontentCode%3d10008001000007022019090917090092%26
categoryCode%3d00040000000515613577781903030000</font>中的targetUrl值替换成去到的链接，并修改currentTime时间判断
7. 上传代码到测试环境http://124.225.67.203:8090/epg/page/index.html
通过
<font color="#dd0000">
http://124.225.67.203:8090/epg/page/toggleUrl.html?UserID=38985017
&iptv_flag=hw&epg_info=<server_ip>10.255.18.164</server_ip>
<group_name>1610060</group_name><group_path>en/Category.jsp</group_path><oss_user_id>38985017</oss_user_id><page_url>http://10.255.18.164:33200/EPG/jsp/zunxiangbao/en/Category.jsp</page_url>
<partner>HW2X</partner><area>9999</area>
&backUrl=http://10.255.18.164:33200/EPG/jsp/zunxiangbao/en/Category.jsp
</font>
访问，如果跳到指定详情页则代码正确