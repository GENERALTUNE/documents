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
12. 移动端如何定义字体font-family
13. 移动端字体单位font-size选择px还是rem
14. 移动端touch事件(区分webkit 和 winphone)
15. 移动端click屏幕产生200-300 ms的延迟响应
16. 触摸事件的响应顺序
17. 什么是Retina 显示屏，带来了什么问题
18. ios系统中元素被触摸时产生的半透明灰色遮罩怎么去掉
19. 部分android系统中元素被点击时产生的边框怎么去掉
20. winphone系统a、input标签被点击时产生的半透明灰色背景怎么去掉
21. webkit表单元素的默认外观怎么重置
22. webkit表单输入框placeholder的颜色值能改变么
23. webkit表单输入框placeholder的文字能换行么
24. IE10（winphone8）表单元素默认外观如何重置
25. 禁止ios 长按时不触发系统的菜单，禁止ios&android长按时下载图片
26. 禁止ios和android用户选中文字
27. 打电话发短信的怎么实现
28. 模拟按钮hover效果
29. 屏幕旋转的事件和样式
30. audio元素和video元素在ios和andriod中无法自动播放
31. 摇一摇功能
32. 手机拍照和上传图片
33. 微信浏览器用户调整字体大小后页面矬了，怎么阻止用户调整
34. 消除transition闪屏
35. 开启硬件加速
36. 取消input在ios下，输入的时候英文首字母的默认大写
37. android上去掉语音输入按钮
38. android 2.3 bug
39. android 4.x bug
40. 设计高性能CSS3动画的几个要素
41. fixed bug
42. 如何阻止windows Phone的默认触摸事件

### 移动web开发

1. 移动端常用类库及优缺点
2. Zepto库和JQ区别