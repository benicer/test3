# 这是EPG部门专区文档
## 专区开发介绍

专区开发就是按照产品经理的需求开发一整个专区，目前主要做的是芒果专区，爱动漫专区，专区开发因为网络环境的原因，一般需要出差进行开发。

## 专区开发默认逻辑介绍

1. 节目名称滚动效果:
```
当节目名称超过显示区域时，焦点移上去要让节目名称自动滚动
```
 <img src="/doc1/zhuanqu/vodScroll.png"   width="800" height="450">

2. 原进原出:
```
从节目A点击跳转到别的地方时，别的地方再按返回仍然回到节目A
```

3. 详情页下侧推荐位点击规则
```
从详情页下侧推荐位点击跳转到新的详情页时，再按返回不遵循原进原出，而应该返回之前的列表页，防止用户点击过多推荐跳转详情页时需要多次返回才能返回到列表页
```
4. 收藏
```
收藏时单集收藏的是当前节目code，多集收藏的是剧头code
```
5. 播放记录
```
1.添加播放记录时，多集添加的是当前子集的code，单集添加的是当前节目code
2.详情页获取当前节目的播放记录时，多集通过剧头code查询，获取的是最近一条子集的续播信息
```

## 专区开发基本流程
阅读需求文档=>按照psd图进行静态页面开发=>对接后台接口数据=》实现页面逻辑=》对接鉴权订购播放功能=》数据埋点（探针功能）

### 阅读需求文档
阅读需求文档时需要评估文档中的功能是否能够实现，需要结合当地后台接口做判断，如：
 
运营想让详情页显示评分字段，但是相应地区接口里没有评分字段，所以无法实现

### 按照psd图进行静态页面开发

开发时保留一份静态页面的代码，方便以后复用

### 对接后台接口数据
目前的几种后台数据接口:
1. 融合平台（公司自己的平台，甘肃，青海都使用这个平台）
2. vis平台（公司自己的平台，老平台，还附带活动平台功能，海南目前还在用来作为数据接口）
3. 广东成思平台（局方的平台，发布代码新建栏目比较麻烦，后台有些接口逻辑也和融合平台不同）
4. 华为基础平台(华为C05 接口，为jsp代码，开发起来调测麻烦，目前深圳在用，但是深圳有封好的jsp，可以通过html直接访问这些jsp)
5. 重庆电信平台(淘景立画公司平台，引入了推荐位的概念，具体参考重庆爱动漫代码)

### 实现页面逻辑
* 首页
  1. 视频框（小视频播放，一般逻辑为获取一个栏目下编排的所有节目，播放5分钟切换下一个节目，电视剧一般默认播放第一集）,背景图视频窗位置必须透明，不然会遮住视频

  <img src="/doc1/zhuanqu/smallScreen.png"   width="800" height="450">

  2. 轮播图（一般为获取一个栏目下的几个节目，几秒钟切换下一个节目）
  3. vas推荐位（运营可以在后台配置链接的推荐位，比较灵活，能够跳转到任意专题页，详情页或者活动页，缺点是运营配置链接可能出错，而且需要手动配置比较麻烦）
  4. vod推荐位 （节目推荐位，代码里做判断只能跳转到详情页，运营在后台配置节目绑定在首页栏目下面，不灵活但是方便运营操作）
* 列表页
  1. 左侧导航栏(根据地址栏里的栏目code获取子栏目列表)
  2. 右侧节目列表（根据左侧导航栏驻留位置的栏目获取下面绑定的所有节目）

  <img src="/doc1/zhuanqu/list.png"   width="800" height="450">

* 详情页
  1. 节目信息展示
    一般显示剧名，海报，导演演员简介等
  2. 功能按钮
  <img src="/doc1/zhuanqu/movie.png"   width="800" height="450">
  <img src="/doc1/zhuanqu/detail-set.png"   width="800" height="450">
  <img src="/doc1/zhuanqu/zy-detail.png"   width="800" height="450">
  
    1. 播放按钮
       * 电影详情页
       * 电视剧详情页一般播放第一集
       * 综艺详情页一般播放最新一期
    2. 续播按钮
       * 电影详情页续播播放记录的时间（播放页需要判断如果节目快结束需要直接重头播放，不然每次进去都是播放最后几秒）
       * 电视剧详情页续播播放记录的集数和时间
       * 综艺剧详情页续播播放记录的集数和时间
    3. 选集按钮
       * 电影详情页无此按钮
       * 电视剧详情页显示集数（点击对应集数直接从该集开头开始播放）
       * 综艺详情页倒序展示节目的期数，最新一期展示在最前面（点击对应集数直接从该集开头开始播放）

    4. 收藏按钮
        剧头收藏，收藏完会在收藏记录列表页面展示
    5. 试看功能
        * 电影详情页进入播放页一般试看5分钟
        * 电视剧详情页一般前三集免费播放
        * 综艺详情页一般都收费
  3. 下方推荐位
    
    * 下方推荐位一般通过地址栏参数里的推荐位栏目code去获取节目
    * 从列表页进入详情页时默认带上当前栏目的code 
    * 从搜索页进入详情页时会根据类型判断，电影电视剧综艺带上不同的栏目code
    * 从推荐位栏目获取推荐节目时，要对当前节目去重
* 搜索页
 <img src="/doc1/zhuanqu/search.png"   width="800" height="450">

    1. 左侧搜索按钮区域（一般都是按照首字母拼音搜索，如寒战搜索HZ）
    2. 右侧大家都在看节目列表（未输入搜索字母时显示）
    3. 右侧搜索展示节目列表（展示搜索到的节目列表）
    4. 右侧搜索不到节目时展示的提示（一般提示为搜索不到节目，然后给出一些推荐节目）
* 播放记录和收藏记录列表页面
<img src="/doc1/zhuanqu/piece-collect.png"   width="800" height="450">

    1. 播放记录列表页面:点击直接进行节目的续播
    2. 收藏记录节目：点击跳转到对应节目详情页面
* 专题列表页面
<img src="/doc1/zhuanqu/topic-list.png"   width="800" height="450">

    1. 左侧导航栏(根据地址栏里的栏目code获取子栏目列表)
    2. 右侧专题列表（根据左侧导航栏驻留位置的栏目获取下面绑定的所有栏目）
* 专题详情页面
<img src="/doc1/zhuanqu/topic-detail.png"   width="800" height="450">

    1. 背景图（上传当前栏目上面）
    2. 下方节目列表（获取当前栏目下的所有子节目）

### 对接鉴权订购播放功能
* 鉴权
    1. 产品鉴权
    ```
        通过计费包的code进行鉴权，判断一个用户是否计费要先后判断包年包，包月包，包季包是否都鉴权通过
    ```
    2. 内容鉴权
    ```
        后台可以进行媒资计费关系的绑定，如一个节目绑定包月包，包季包，包年包，鉴权时传入这个节目的code，鉴权接口自动判断返回这个节目是否鉴权成功
    ```
    3. 垫片
    ```
    后台的一个节目,绑定了所有计费包，用来作为用户内容鉴权的默认code,判断用户是否订购过
    ```
* 订购
    1. 主动订购
    ``` 
    指用户主动点击订购按钮触发的订购
    ```
    2. 被动订购
    ```
        用户在详情页点击播放时触发的订购
    ```
* 播放页
    * 自己实现的播放页
        通过接口获取播放地址，然后使用机顶盒的mediaPlayer方法进行播放，如贵州酷喵播放页
    * 播控自己实现，局方的播放方法
        调用华为或者中兴的播放页面进行视频流的播放，播控还是使用mediaPlayer进行播放，如甘肃芒果播放页，青海芒果播放页
    * 局方播放页
        播放时直接按对接文档传递相应参数跳转到局方播放页，如广东电信播放页，海南环球播放页

### 数据埋点（探针功能）
* 局方探针
    ```
    按照局方探针文档开发的探针，数据上报到局方的大数据平台
    ```
* vis平台探针
    ```
    调用vis平台的探针接口上报的探针，数据上报到vis平台上，运营可以在vis平台直接看到数据
    ```
* 大数据探针
    ```
    按照大数据文档进行采集，通过log.js里的方法进行探针数据上报
    ```