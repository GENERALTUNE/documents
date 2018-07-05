## 移动APP开发.

1. 移动端最小触控区域是多大？
    因为达成了一个基本共识，所以就谈论的就少了。
    苹果推荐是 44pt x 44pt 「具体看 WWDC 14」，也可以看下面这个网址
    https://developer.apple.com/ios/human-interface-guidelines/visual-design/layout/
2. fiddler 手机抓包
3. meta基础知识
    1)  H5页面窗口自动调整到设备宽度，并禁止用户缩放页面
        ```
        <meta name="viewport" content="width=device-width,initial-scale=1.0,minimum-scale=1.0,maximum-scale=1.0,user-scalable=no" />
        ```
    2)  忽略将页面中的数字识别为电话号码
        ```
        <meta name="format-detection" content="telephone=no" />
        ```
    3)  忽略Android平台中对邮箱地址的识别
        ```
        <meta name="format-detection" content="email=no" />
        ```
    4） 当网站添加到主屏幕快速启动方式，可隐藏地址栏，仅针对ios的safari
         ```
         <meta name="apple-mobile-web-app-status-bar-style" content="black" />
            <!-- 可选default、black、black-translucent -->
         ```
4. 移动端如何定义字体font-family
    中文字体使用系统默认即可，英文用Helvetica
    ```
        /* 移动端定义字体的代码 */
        body{font-family:Helvetica;}
        
    ```
5.  移动布局自适应不同屏幕的几种方式
    （1）响应式布局
    （2）100%布局（弹性布局）
    （3）等比缩放布局（rem）

6.  iscroll安卓低版本卡顿，如何解决？

    方案一：iScroll v5.1.3 设置momentum: true
    方案二：配置probeType
    方案三：开启硬价加速：给scroll元素增加css样式：-webkit-transform:translate3d(0,0,0);
    方案四：判断手机版系统版本，应用原生CSS：overflow-y:scroll

7. 移动布局自适应不同屏幕的几种方式
    （1）响应式布局
    （2）100%布局（弹性布局）
    （3）等比缩放布局（rem）

8. 你们做移动端平时在什么浏览器上测试？
    Chrome，Safari，微信X5，UC，其他手机自带浏览器
9. 说说移动端是如何调试的？
    移动端调试：
    （1）模拟手机调试chrome://inspect
    （2）真机调试之android手机+Chrome
    （3）真机调试之iphone + safari
    （4）UC浏览器
    （5）微信内置浏览器调试
    （6）debuggap
    （7）抓包
10. 说说ICONFONT是如何用的？
    从以下几个方面做答：
    （1）font-face
    （2）什么是iconfont,iconfont怎么用
    （3）iconfont怎么做
    （4）iconfont的利和弊

11. 说说移动端Web分辨率

    从以下几个方面做答：
    （1）PC到移动，渲染的变迁
    （2）可以更改的布局宽度
    （3）再次变迁的像素
    （4）又一次变迁
    （5）是时候说说安卓了
12. 移动端字体单位font-size选择px还是rem
    对于只需要适配少部分手机设备，且分辨率对页面影响不大的，使用px即可

    对于需要适配各种移动设备，使用rem，例如只需要适配iPhone和iPad等分辨率差别比较挺大的设备

    rem配置参考，适合视觉稿宽度为640px的：
    ```
        <meta content="width=device-width,initial-scale=1.0,maximum-scale=1.0,user-scalable=no" name="viewport">
        html{font-size:10px}
        @media screen and (min-width:321px) and (max-width:375px){html{font-size:11px}}
        @media screen and (min-width:376px) and (max-width:414px){html{font-size:12px}}
        @media screen and (min-width:415px) and (max-width:639px){html{font-size:15px}}
        @media screen and (min-width:640px) and (max-width:719px){html{font-size:20px}}
        @media screen and (min-width:720px) and (max-width:749px){html{font-size:22.5px}}
        @media screen and (min-width:750px) and (max-width:799px){html{font-size:23.5px}}
        @media screen and (min-width:800px){html{font-size:25px}}
    ```
13. 移动端touch事件(区分webkit 和 winphone)
    当用户手指放在移动设备在屏幕上滑动会触发的touch事件

    以下支持webkit

    touchstart——当手指触碰屏幕时候发生。不管当前有多少只手指
    touchmove——当手指在屏幕上滑动时连续触发。通常我们再滑屏页面，会调用event的preventDefault()可以阻止默认情况的发生：阻止页面滚动
    touchend——当手指离开屏幕时触发
    touchcancel——系统停止跟踪触摸时候会触发。例如在触摸过程中突然页面alert()一个提示框，此时会触发该事件，这个事件比较少用
    TouchEvent

    touches：屏幕上所有手指的信息
    targetTouches：手指在目标区域的手指信息
    changedTouches：最近一次触发该事件的手指信息
    touchend时，touches与targetTouches信息会被删除，changedTouches保存的最后一次的信息，最好用于计算手指信息
    参数信息(changedTouches[0])

    clientX、clientY在显示区的坐标
    target：当前元素
    参考：https://developer.mozilla.org/en-US/docs/Web/API/TouchEvent

    以下支持winphone 8

    MSPointerDown——当手指触碰屏幕时候发生。不管当前有多少只手指
    MSPointerMove——当手指在屏幕上滑动时连续触发。通常我们再滑屏页面，会调用css的html{-ms-touch-action: none;}可以阻止默认情况的发生：阻止页面滚动
    MSPointerUp——当手指离开屏幕时触发
14. 移动端click屏幕产生200-300 ms的延迟响应
    移动设备上的web网页是有300ms延迟的，玩玩会造成按钮点击延迟甚至是点击失效。
    以下是历史原因，来源一个公司内一个同事的分享：
    2007年苹果发布首款iphone上IOS系统搭载的safari为了将适用于PC端上大屏幕的网页能比较好的展示在手机端上，使用了双击缩放(double tap to zoom)的方案，比如你在手机上用浏览器打开一个PC上的网页，你可能在看到页面内容虽然可以撑满整个屏幕，但是字体、图片都很小看不清，此时可以快速双击屏幕上的某一部分，你就能看清该部分放大后的内容，再次双击后能回到原始状态。

    双击缩放是指用手指在屏幕上快速点击两次，iOS 自带的 Safari 浏览器会将网页缩放至原始比例。

    原因就出在浏览器需要如何判断快速点击上，当用户在屏幕上单击某一个元素时候，例如跳转链接<a href="#"></a>，此处浏览器会先捕获该次单击，但浏览器不能决定用户是单纯要点击链接还是要双击该部分区域进行缩放操作，所以，捕获第一次单击后，浏览器会先Hold一段时间t，如果在t时间区间里用户未进行下一次点击，则浏览器会做单击跳转链接的处理，如果t时间里用户进行了第二次单击操作，则浏览器会禁止跳转，转而进行对该部分区域页面的缩放操作。那么这个时间区间t有多少呢？在IOS safari下，大概为300毫秒。这就是延迟的由来。造成的后果用户纯粹单击页面，页面需要过一段时间才响应，给用户慢体验感觉，对于web开发者来说是，页面js捕获click事件的回调函数处理，需要300ms后才生效，也就间接导致影响其他业务逻辑的处理。

    解决方案：

    fastclick可以解决在手机上点击事件的300ms延迟
    zepto的touch模块，tap事件也是为了解决在click的延迟问题
15. 触摸事件的响应顺序
    1、ontouchstart 
    2、ontouchmove 
    3、ontouchend 
    4、onclick
16. 什么是Retina 显示屏，带来了什么问题
    retina：一种具备超高像素密度的液晶屏，同样大小的屏幕上显示的像素点由1个变为多个，如在同样带下的屏幕上，苹果设备的retina显示屏中，像素点1个变为4个
    在高清显示屏中的位图被放大，图片会变得模糊，因此移动端的视觉稿通常会设计为传统PC的2倍
    那么，前端的应对方案是：
    设计稿切出来的图片长宽保证为偶数，并使用backgroud-size把图片缩小为原来的1/2
    //例如图片宽高为：200px*200px，那么写法如下
    .css{width:100px;height:100px;background-size:100px 100px;}
    其它元素的取值为原来的1/2，例如视觉稿40px的字体，使用样式的写法为20px
    .css{font-size:20px}
17. ios系统中元素被触摸时产生的半透明灰色遮罩怎么去掉
18. 部分android系统中元素被点击时产生的边框怎么去掉
19. winphone系统a、input标签被点击时产生的半透明灰色背景怎么去掉
20. webkit表单元素的默认外观怎么重置
21. webkit表单输入框placeholder的颜色值能改变么
22. webkit表单输入框placeholder的文字能换行么
23. IE10（winphone8）表单元素默认外观如何重置
24. 禁止ios 长按时不触发系统的菜单，禁止ios&android长按时下载图片
25. 禁止ios和android用户选中文字
26. 打电话发短信的怎么实现
27. 模拟按钮hover效果
28. 屏幕旋转的事件和样式
    window.orientation，取值：正负90表示横屏模式、0和180表现为竖屏模式；
    ```
    window.onorientationchange = function(){
        switch(window.orientation){
            case -90:
            case 90:
            alert("横屏:" + window.orientation);
            case 0:
            case 180:
            alert("竖屏:" + window.orientation);
            break;
        }
    }
    //竖屏时使用的样式
    @media all and (orientation:portrait) {
    .css{}
    }

    //横屏时使用的样式
    @media all and (orientation:landscape) {
    .css{}
    }  
    ```
29. audio元素和video元素在ios和andriod中无法自动播放
30. 摇一摇功能
    关于devicemotion 
    html5提供了几个新的DOM事件来获得设备物理方向及运动的信息，包括：陀螺仪、罗盘及加速计。
    第一个DOM事件是**deviceorientation**，其提供设备的物理方向信息，表示为一系列本地坐标系的旋角。
    第二个DOM事件是**devicemotion**，其提供设备的加速信息，表示为定义在设备上的坐标系中的卡尔迪坐标。其还提供了设备在坐标系中的自转速率。
    第三个DOM事件是**compassneedscalibration**，其用于通知Web站点使用罗盘信息校准上述事件。
    说是这么说，什么是陀螺仪，罗盘又是个啥，加速计又是个神马东东
    原理
    开发者从各个内置传感器那里获取未经修改的传感数据，并观测或响应设备各种运动和角度变化。这些传感器包括陀螺仪、加速器和磁力仪(罗盘)。
    加速器和陀螺仪的数据都是描述沿着iOS设备三个方向轴上的位置，对于一个竖屏摆放的iPhone来说，X方向从设备的左边(负)到右边(正)，Y方向则是由设备的底部(-)到顶部(+)，而Z方向为垂直于屏幕由设备的背面(-)到正面(+)。

31. 手机拍照和上传图片
    ```
    <input type="file">的accept 属性

    <!-- 选择照片 -->
    <input type=file accept="image/*">
    <!-- 选择视频 -->
    <input type=file accept="video/*">
    ```
    使用总结：

    ios 有拍照、录像、选取本地图片功能
    部分android只有选取本地图片功能
    winphone不支持
    input控件默认外观丑陋
32. 微信浏览器用户调整字体大小后页面矬了，怎么阻止用户调整
33. 消除transition闪屏
34. 开启硬件加速
35. 取消input在ios下，输入的时候英文首字母的默认大写
36. android上去掉语音输入按钮
37. android 2.3 bug
38. android 4.x bug
39. 设计高性能CSS3动画的几个要素
40. fixed bug
41. 如何阻止windows Phone的默认触摸事件
42. 常用的移动端框架
    zepto.js
    iscroll.js
    解决页面不支持弹性滚动，不支持fixed引起的问题~
    实现下拉刷新，滑屏，缩放等功能~
    最新版本已经更新到5.0
    官网：http://cubiq.org/iscroll-5
    underscore.js
    滑屏框架
    适合上下滑屏、左右滑屏等滑屏切换页面的效果
    slip.js iSlider.js fullpage.js swiper.js
    flex布局 (new)
    FastClick
    Sea.js

### 移动web开发

1. 移动端常用类库及优缺点
2. Zepto库和JQ区别