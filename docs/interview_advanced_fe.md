## 腾讯面试

第一场

### 面试官一
1. 自我介绍
2. setState 的过程
3. react为什么需要用到key
4. function Component
5. react 的组件如何不更新
6. webpack plugin dll 了解吗
7. webpack  gulp grunt 的区别
### 面试官二
1. 遇到的困难如何克服
2. tcp/ip 协议 和http 有什么区别

第二场

1. 自我介绍
2. 遇到的困难如何克服
3. jquery 选择器的实现  . # 的性能
4. jquery 事件代理的原理   捕获和冒泡的过程
5. 了解es6 吗  如何定义一个类
6. 了解原型链吗
7. 跨域及如何跨域  同源策略 同域名不同端口   不同协议算不算跨域
   协议+域名+端口号  任一不同都是跨域 违反同源策略
   后端跨域解决:
        前端单独作为服务发布，势必会涉及到无法直接调用后端的接口的问题，因为浏览器是不允许跨域提交请求的。

       所谓跨域访问，就是在浏览器窗口，和某个服务端通过某个协议+域名+端口号建立了会话的前提下，去使用与这三个属性任意一个不同的源提交了请求，比如:打开新窗口，iframe,xmlhttprequest，那么浏览器就认为你是跨域了，违反了浏览器的同源策略。 

    　　解决此问题，w3c标准中，有针对跨域请求的规范：

    　　在响应头中带上Access-Control-Allow-Origin，值是你允许跨域访问的源，比如http://www.baidu.com，注意这里只支持*（表示所有源）号或者某个源，不支持多个源，如果要实现多个源，可以自己包装一个集合，对每次的请求在集合中判断是否存在，如存在，就放到响应头中来；

    　　使用Access-Control-Allow-Methods 限制允许跨域访问的http方法类型，多个以逗号隔开，比如：POST,GET,OPTIONS

    　　使用Access-Control-Allow-Headers，限制允许跨域访问的http头，包含这里设置的头，才允许跨域访问 比如：foo-x

    　　对于客户端在发送请求的时候，浏览器会检测如果本次请求是一个非简单的跨域请求，就会先发送一个OPTIONS的请求到后台预检一下是否支持本源的跨域，如果支持，后台就用上面提到的几个响应头信息告诉浏览器，接着浏览器会发送真正的请求到后台，否则请求将不会得到结果，浏览器会报违反同源策略的警告。header(‘Access-Control-Allow-Origin:*’);

    　　关于简单跨域请求和非简单跨域请求解释如下：

    　　CORS(Cross Origin Resourse-Sharing),中文意思是跨域资源共享，定义了两种跨域请求，简单跨域请求和非简单跨域请求。当一个跨域请求发送简单跨域请求包括：请求方法为HEAD，GET，POST;请求头只有4个字段，Accept，Accept-Language，Content-Language，Last-Event-ID;如果设置了Content-Type，则其值只能是application/x-www-form-urlencoded,multipart/form-data,text/plain，所以，我们设置一下content-type为其它的值，比如application/json,此次请求就会被认为是非简单跨域请求，浏览器就会提交预检请求了。

    php 利用Access-Control-Allow-Origin响应头解决跨域请求:
    在服务器响应客户端的时候，带上Access-Control-Allow-Origin头信息。有以下两种设置方式:

    泛域名: (* 允许所有域名的脚本访问该资源。)
    Access-Control-Allow-Origin: *        
    特定域名: ( http://www.aerchi.com: 允许特定的域名访问。)
    Access-Control-Allow-Origin: http://www.aerchi.com  

    比如在PHP添加响应头信息：(表示支持所有域名访问)

    header("Access-Control-Allow-Origin: *");

    如下列PHP 语法设置:

    // 指定允许其他域名访问

    header('Access-Control-Allow-Origin:*');

    // 响应类型

    header('Access-Control-Allow-Methods:*');

    // 响应头设置

    header('Access-Control-Allow-Headers:x-requested-with,content-type');

    php支持多个地址跨域访问:

    $origin = isset($_SERVER['HTTP_ORIGIN']) ? $_SERVER['HTTP_ORIGIN'] : '';
    $allow_origin = array(
        'http://www.a.com',
        'http://www.b.com'
    );
    if(in_array($origin, $allow_origin)){
        header('Access-Control-Allow-Origin:'.$origin);
        header('Access-Control-Allow-Methods:POST');
        header('Access-Control-Allow-Headers:x-requested-with,content-type');
    }
    前端跨域解决: HTTP技能之同源策略
    安全考量
    有这种限制的主要原因就是如果没有同源策略将导致安全风险。假设用户在访问银行网站，并且没有登出。然后他又去了任意的其他网站，刚好这个网站有恶意的js代码，在后台请求银行网站的信息。因为用户目前仍然是银行站点的登陆状态，那么恶意代码就可以在银行站点做任意事情。例如，获取你的最近交易记录，创建一个新的交易等等。因为浏览器可以发送接收银行站点的session cookies，在银行站点域上。访问恶意站点的用户希望他访问的站点没有权限访问银行站点的cookie。当然确实是这样的，js不能直接获取银行站点的session cookie，但是他仍然可以向银行站点发送接收附带银行站点session cookie的请求，本质上就像一个正常用户访问银行站点一样。关于发送的新交易，甚至银行站点的CSRF（跨站请求伪造）防护都无能无力，因为脚本可以轻易的实现正常用户一样的行为。所以如果你需要session或者需要登陆时，所有网站都面临这个问题。如果上例中的银行站点只提供公开数据，你就不能触发任意东西，这样的就不会有危险了，这些就是同源策略防护的。当然，如果两个站点是同一个组织的或者彼此互相信任，那么就没有这种危险了。

    规避同源策略
    在某些情况下同源策略太严格了，给拥有多个子域的大型网站带来问题。下面就是解决这种问题的技术：

    document.domain属性
    如果两个window或者frames包含的脚本可以把domain设置成一样的值，那么就可以规避同源策略，每个window之间可以互相沟通。例如，orders.example.com下页面的脚本和catalog.example.com下页面的脚本可以设置他们的document.domain属性为example.com，从而让这两个站点下面的文档看起来像在同源下，然后就可以让每个文档读取另一个文档的属性。这种方式也不是一直都有用，因为端口号是在内部保存的，有可能被保存成null。换句话说，example.com的端口号80，在我们更新document.domain属性的时候可能会变成null。为null的端口可能不被认为是80，这主要依赖浏览器实现。

    跨域资源共享
    这种方式使用了一个新的Origin请求头和一个新的Access-Control-Allow-Origin响应头扩展了HTTP。允许服务端设置Access-Control-Allow-Origin头标识哪些站点可以请求文件，或者设置Access-Control-Allow-Origin头为"*"，允许任意站点访问文件。浏览器，例如Firefox3.5，Safari4，IE10使用这个头允许跨域HTTP请求。

    跨文档通信
    这种方式允许一个页面的脚本发送文本信息到另一个页面的脚本中，不管脚本是否跨域。在一个window对象上调用postMessage()会异步的触发window上的onmessage事件，然后触发定义好的事件处理方法。一个页面上的脚本仍然不能直接访问另外一个页面上的方法或者变量，但是他们可以安全的通过消息传递技术交流。

    JSONP
    JOSNP允许页面接受另一个域的JSON数据，通过在页面增加一个可以从其它域加载带有回调的JSON响应的<script>标签。
    jsonp的产生:

    1.AJAX直接请求普通文件存在跨域无权限访问的问题,不管是静态页面也好.

    2.不过我们在调用js文件的时候又不受跨域影响,比如引入jquery框架的,或者是调用相片的时候

    3.凡是拥有scr这个属性的标签都可以跨域例如<script><img><iframe>

    4.如果想通过纯web端跨域访问数据只有一种可能,那就是把远程服务器上的数据装进js格式的文件里.

    5.而json又是一个轻量级的数据格式,还被js原生支持

    6.为了便于客户端使用数据，逐渐形成了一种非正式传输协议，人们把它称作JSONP，该协议的一个要点就是允许用户传递一个callback 参数给服务端，

    WebSocket
    现代浏览器允许脚本直连一个WebSocket地址而不管同源策略。然而，使用WebSocket URI的时候，在请求中插入Origin头就可以标识脚本请求的源。为了确保跨站安全，WebSocket服务器必须根据允许接受请求的白名单中的源列表比较头数据。

    个例以及异常
    在一些个例中，例如哪些没有明确定义主机名或者端口的协议(file:,data:,等)，同源检查以及相关机制如何运作没有很好的定义。这在历史上导致了很多安全问题，例如任意本地存储的HTML文件不能访问磁盘上的其他文件，也不能与任何网络上的站点通信。

    另外，很多遗留的跨域操作，早期是不受同源策略限制的，例如<script>的跨域请求以及表单POST提交。

    最后，某些类型的攻击，例如DNS重新绑定，服务端代理，可以破坏主机名检查，让流氓页面可以直接通过地址与站点通信，尽管地址不是同源的。这种攻击的影响仅限于某些特殊情况下，例如，如果浏览器仍然相信正在通信的攻击者的站点，然后没有公开第三方cookie或者其他敏感信息给攻击者。

    变通方法
    为了让开发者可以在可控情况下绕过同源策略，一些"hacks"方法可以被用来在不同域的文档之间传输数据，例如fragment identifier ，window.name属性。根据HTML5标准，一个postMessage接口可以实现这样的功能，但是只有最新的浏览器才支持。JSONP也可以用来保证通过类似Ajax的方式访问跨域资源。
    同源策略限制了不同源之间的交互，但是有人也许会有疑问，我们以前在写代码的时候也常常会引用其他域名的js文件，样式文件，图片文件什么的，没看到限制啊，这个定义是不是错了。其实不然，同源策略限制的不同源之间的交互主要针对的是js中的XMLHttpRequest等请求，下面这些情况是完全不受同源策略限制的。

    页面中的链接，重定向以及表单提交是不会受到同源策略限制的。链接就不用说了，导航网站上的链接都是链接到其他站点的。而你在域名www.foo.com下面提交一个表单到www.bar.com是完全可以的。
    跨域资源嵌入是允许的，当然，浏览器限制了Javascript不能读写加载的内容。如前面提到的嵌入的<script src="..."></script>，<img>，<link>，<iframe>等。当然，如果要阻止iframe嵌入我们网站的资源(页面或者js等)，我们可以在web服务器加上一个X-Frame-Options DENY头部来限制。nginx就可以这样设置add_header X-Frame-Options DENY;。
    既然有这么多的情况是没有同源策略限制的，那么通常的跨域问题从何而来呢？转到下一节跨域问题。

    2 跨域问题
    这一节来讨论下跨域问题，当然前置条件是我们在WEB服务器或者服务端脚本中设置ACCESS-CONTROL-ALLOW-ORIGIN头部，如果设置了这些头部并允许某些域名跨域访问，则浏览器就会跳过同源策略的限制返回对应的内容。此外，如果你不是通过浏览器去获取资源，比如你通过一个python脚本去调用接口或者获取js文件，也不在这个限制之内。
8. 如何提高浏览器端的效率  静态资源缓存
9.  promise的状态  异步的同步写法
10. for 循环 console.log 输出的结果 为什么 及如何输出 1 2 3
11. 如何实现一个向下滑动的vue组件
12. 有什么想问的问题



## 阿里
    使用过的koa2中间件

    koa-body原理

    介绍自己写过的中间件

    有没有涉及到Cluster

    介绍pm2

    master挂了的话pm2怎么处理

    如何和MySQL进行通信

    React声明周期及自己的理解

    如何配置React-Router

    路由的动态加载模块

    服务端渲染SSR

    介绍路由的history

    介绍Redux数据流的流程

    Redux如何实现多个组件之间的通信，多个组件使用相同状态如何进行管理

    多个组件之间如何拆分各自的state，每块小的组件有自己的状态，它们之间还有一些公共的状态需要维护，如何思考这块

    使用过的Redux中间件

    如何解决跨域的问题

    常见Http请求头

    移动端适配1px的问题

### 介绍flex布局


    1. 容器的属性

    flex-direction
    flex-wrap
    flex-flow
    justify-content
    align-items
    align-content

    1. 项目的属性
    order
    flex-grow
    flex-shrink
    flex-basis
    flex
    align-self

```javascript 
    display: flex;
    flex

```


    参考： http://www.runoob.com/w3cnote/flex-grammar.html

    其他css方式设置垂直居中

    居中为什么要使用transform（为什么不使用marginLeft/Top）

    使用过webpack里面哪些plugin和loader

    webpack里面的插件是怎么实现的

    dev-server是怎么跑起来

    项目优化

    抽取公共文件是怎么配置的

    项目中如何处理安全问题

    怎么实现this对象的深拷贝



## 网易
介绍redux，主要解决什么问题

文件上传如何做断点续传

表单可以跨域吗

promise、async有什么区别

搜索请求如何处理（防抖）

搜索请求中文如何请求

介绍观察者模式

介绍中介者模式

观察者和订阅-发布的区别，各自用在哪里

介绍react优化

介绍http2.0

通过什么做到并发请求

http1.1时如何复用tcp连接

介绍service worker

介绍css3中position:sticky

redux请求中间件如何处理并发

介绍Promise，异常捕获

介绍position属性包括CSS3新增

浏览器事件流向

介绍事件代理以及优缺点

React组件中怎么做事件代理

React组件事件代理的原理

介绍this各种情况

前端怎么控制管理路由

使用路由时出现问题如何解决

React怎么做数据的检查和变化



## 滴滴
react-router怎么实现路由切换

react-router里的<Link>标签和<a>标签有什么区别

<a>标签默认事件禁掉之后做了什么才实现了跳转

React层面的性能优化

整个前端性能提升大致分几类

import { Button } from 'antd'，打包的时候只打包button，分模块加载，是怎么做到的

使用import时，webpack对node_modules里的依赖会做什么

JS异步解决方案的发展历程以及优缺点

Http报文的请求会有几个部分

cookie放哪里，cookie能做的事情和存在的价值

cookie和token都存放在header里面，为什么只劫持前者

cookie和session有哪些方面的区别

React中Dom结构发生变化后内部经历了哪些变化

React挂载的时候有3个组件，textComponent、composeComponent、domComponent，区别和关系，Dom结构发生变化时怎么区分data的变化，怎么更新，更新怎么调度，如果更新的时候还有其他任务存在怎么处理

key主要是解决哪一类的问题，为什么不建议用索引index（重绘）

Redux中异步的请求怎么处理

Redux中间件是什么东西，接受几个参数（两端的柯里化函数）

柯里化函数两端的参数具体是什么东西

中间件是怎么拿到store和action，然后怎么处理

state是怎么注入到组件的，从reducer到组件经历了什么样的过程

koa中response.send、response.rounded、response.json发生了什么事，浏览器为什么能识别到它是一个json结构或是html

koa-bodyparser怎么来解析request

webpack整个生命周期，loader和plugin有什么区别

介绍AST（Abstract Syntax Tree）抽象语法树

安卓Activity之间数据是怎么传递的

安卓4.0到6.0过程中WebView对js兼容性的变化

WebView和原生是如何通信

跨域怎么解决，有没有使用过Apache等方案



## 今日头条
对async、await的理解，内部原理 

介绍下Promise，内部实现 

清除浮动  

定位问题（绝对定位、相对定位等） 

从输入URL到页面加载全过程 

tcp3次握手 

tcp属于哪一层（1 物理层 -> 2 数据链路层 -> 3 网络层(ip)-> 4 传输层(tcp) -> 5 应用层(http)） 

redux的设计思想 

接入redux的过程 

绑定connect的过程 

connect原理 

webpack介绍 

== 和 ===的区别，什么情况下用相等== 

bind、call、apply的区别 

动画的了解 

介绍下原型链（解决的是继承问题吗） 

对跨域的了解 



## 有赞
Linux 754 介绍

介绍冒泡排序，选择排序，冒泡排序如何优化

transform动画和直接使用left、top改变位置有什么优缺点

如何判断链表是否有环

介绍二叉搜索树的特点

介绍暂时性死区

ES6中的map和原生的对象有什么区别

观察者和发布-订阅的区别

react异步渲染的概念,介绍Time Slicing 和 Suspense

16.X声明周期的改变

16.X中props改变后在哪个生命周期中处理

介绍纯函数

前端性能优化

pureComponent和FunctionComponent区别

介绍JSX

如何做RN在安卓和IOS端的适配

RN为什么能在原生中绘制成原生组件（bundle.js）

介绍虚拟DOM

如何设计一个localStorage，保证数据的实效性

如何设计Promise.all()

介绍高阶组件

sum(2, 3)实现sum(2)(3)的效果

react性能优化

两个对象如何比较



## 挖财
JS的原型

变量作用域链

call、apply、bind的区别

防抖和节流的区别

介绍各种异步方案

react生命周期

介绍Fiber

前端性能优化

介绍DOM树对比

react中的key的作用

如何设计状态树

介绍css，xsrf

http缓存控制

项目中如何应用数据结构

native提供了什么能力给RN

如何做工程上的优化

shouldComponentUpdate是为了解决什么问题

如何解决props层级过深的问题

前端怎么做单元测试

webpack生命周期

webpack打包的整个过程

常用的plugins

pm2怎么做进程管理，进程挂掉怎么处理

不用pm2怎么做进程管理



## 沪江
介绍下浏览器跨域

怎么去解决跨域问题

jsonp方案需要服务端怎么配合

Ajax发生跨域要设置什么（前端）

加上CORS之后从发起到请求正式成功的过程

xsrf跨域攻击的安全性问题怎么防范

使用Async会注意哪些东西

Async里面有多个await请求，可以怎么优化（请求是否有依赖）

Promise和Async处理失败的时候有什么区别

Redux在状态管理方面解决了React本身不能解决的问题

Redux有没有做过封装

react生命周期，常用的生命周期 

对应的生命周期做什么事 

遇到性能问题一般在哪个生命周期里解决 

怎么做性能优化（异步加载组件...）

写react有哪些细节可以优化 

React的事件机制（绑定一个事件到一个组件上）

介绍下事件代理，主要解决什么问题

前端开发中用到哪些设计模式

React/Redux中哪些功能用到了哪些设计模式

JS变量类型分为几种，区别是什么

JS里垃圾回收机制是什么，常用的是哪种，怎么处理的

一般怎么组织CSS（Webpack）



## 饿了么
小程序里面开页面最多多少

React子父组件之间如何传值

Emit事件怎么发，需要引入什么

介绍下React高阶组件，和普通组件有什么区别

一个对象数组，每个子对象包含一个id和name，React如何渲染出全部的name

在哪个生命周期里写

其中有几个name不存在，通过异步接口获取，如何做

渲染的时候key给什么值，可以使用index吗，用id好还是index好

webpack如何配sass，需要配哪些loader

配css需要哪些loader

如何配置把js、css、html单独打包成一个文件

div垂直水平居中（flex、绝对定位）

两个元素块，一左一右，中间相距10像素

上下固定，中间滚动布局如何实现

[1, 2, 3, 4, 5]变成[1, 2, 3, a, b, 5]

取数组的最大值（ES5、ES6）

apply和call的区别

ES5和ES6有什么区别

some、every、find、filter、map、forEach有什么区别

上述数组随机取数，每次返回的值都不一样

如何找0-5的随机数，95-99呢

页面上有1万个button如何绑定事件

如何判断是button

页面上生成一万个button，并且绑定事件，如何做（JS原生操作DOM）

循环绑定时的index是多少，为什么，怎么解决

页面上有一个input，还有一个p标签，改变input后p标签就跟着变化，如何处理

监听input的哪个事件，在什么时候触发



## 携程
对React看法，有没有遇到一些坑

对闭包的看法，为什么要用闭包

手写数组去重函数

手写数组扁平化函数

介绍下Promise的用途和性质

Promise和Callback有什么区别

React生命周期

两道手写算法题



## 喜马拉雅
ES6新的特性

介绍Promise

Promise有几个状态

说一下闭包

React的生命周期

componentWillReceiveProps的触发条件是什么

React16.3对生命周期的改变

介绍下React的Filber架构

画Filber渲染树

介绍React高阶组件

父子组件之间如何通信

Redux怎么实现属性传递，介绍下原理

React-Router版本号

网站SEO怎么处理

介绍下HTTP状态码

403、301、302是什么

缓存相关的HTTP请求头

介绍HTTPS

HTTPS怎么建立安全通道

前端性能优化（JS原生和React）

用户体验做过什么优化

对PWA有什么了解

对安全有什么了解

介绍下数字签名的原理

前后端通信使用什么方案

RESTful常用的Method

介绍下跨域

Access-Control-Allow-Origin在服务端哪里配置

csrf跨站攻击怎么解决

前端和后端怎么联调



## 兑吧
localStorage和cookie有什么区别

CSS选择器有哪些

盒子模型，以及标准情况和IE下的区别

如何实现高度自适应

prototype和——proto——区别

_construct是什么

new是怎么实现的

promise的精髓，以及优缺点

如何实现H5手机端的适配

rem、flex的区别（root em）

em和px的区别

React声明周期

如何去除url中的#号

Redux状态管理器和变量挂载到window中有什么区别

webpack和gulp的优缺点

如何实现异步加载

如何实现分模块打包（多入口）

前端性能优化（1js css；2 图片；3 缓存预加载； 4 SSR； 5 多域名加载；6 负载均衡）

并发请求资源数上限（6个）

base64为什么能提升性能，缺点

介绍webp这个图片文件格式

介绍koa2

Promise如何实现的

异步请求，低版本fetch如何低版本适配

ajax如何处理跨域

CORS如何设置

jsonp为什么不支持post方法

介绍同源策略

React使用过的一些组件

介绍Immuable

介绍下redux整个流程原理

介绍原型链

如何继承



## 微医
介绍JS数据类型，基本数据类型和引用数据类型的区别

Array是Object类型吗

数据类型分别存在哪里

var a  = {name: "前端开发"}; var b = a; a = null那么b输出什么

var a = {b: 1}存放在哪里

var a = {b: {c: 1}}存放在哪里

栈和堆的区别

垃圾回收时栈和堆的区别

数组里面有10万个数据，取第一个元素和第10万个元素的时间相差多少

栈和堆具体怎么存储

介绍闭包以及闭包为什么没清除

闭包的使用场景

JS怎么实现异步

异步整个执行周期

Promise的三种状态

Async/Await怎么实现

Promise和setTimeout执行先后的区别

JS为什么要区分微任务和宏任务

Promise构造函数是同步还是异步执行，then呢

发布-订阅和观察者模式的区别

JS执行过程中分为哪些阶段

词法作用域和this的区别

平常是怎么做继承

深拷贝和浅拷贝

loadsh深拷贝实现原理

ES6中let块作用域是怎么实现的

React中setState后发生了什么

setState为什么默认是异步

setState什么时候是同步的

为什么3大框架出现以后就出现很多native（RN）框架（虚拟DOM）

虚拟DOM主要做了什么

虚拟DOM本身是什么（JS对象）

304是什么

打包时Hash码是怎么生成的

随机值存在一样的情况，如何避免

使用webpack构建时有无做一些自定义操作

webpack做了什么

a，b两个按钮，点击aba，返回顺序可能是baa，如何保证是aba（Promise.then）

node接口转发有无做什么优化

node起服务如何保证稳定性，平缓降级，重启等

RN有没有做热加载

RN遇到的兼容性问题

RN如何实现一个原生的组件

RN混原生和原生混RN有什么不同

什么是单页项目

遇到的复杂业务场景

Promise.all实现原理



## 寺库
介绍Promise的特性，优缺点

介绍Redux

RN的原理，为什么可以同时在安卓和IOS端运行

RN如何调用原生的一些功能

介绍RN的缺点

介绍排序算法和快排原理

堆和栈的区别

介绍闭包

闭包的核心是什么

网络的五层模型

HTTP和HTTPS的区别

HTTPS的加密过程

介绍SSL和TLS

介绍DNS解析

JS的继承方法

介绍垃圾回收

cookie的引用为了解决什么问题

cookie和localStorage的区别

如何解决跨域问题

前端性能优化



## 宝宝树
使用canvas绘图时如何组织成通用组件

formData和原生的ajax有什么区别

介绍下表单提交，和formData有什么关系

介绍redux接入流程

rudux和全局管理有什么区别（数据可控、数据响应）

RN和原生通信

介绍MVP怎么组织

介绍异步方案

promise如何实现then处理

koa2中间件原理

常用的中间件

服务端怎么做统一的状态处理

如何对相对路径引用进行优化

node文件查找优先级

npm2和npm3+有什么区别



## 海康威视
knex连接数据库响应回调

介绍异步方案

如何处理异常捕获

项目如何管理模块

前端性能优化

JS继承方案

如何判断一个变量是不是数组

变量a和b，如何交换

事件委托

多个<li>标签生成的Dom结构是一个类数组

类数组和数组的区别

dom的类数组如何转成数组

介绍单页面应用和多页面应用

redux状态树的管理

介绍localstorage的API



## 蘑菇街
html语义化的理解

<b>和<strong>的区别

对闭包的理解

工程中闭包使用场景

介绍this和原型

使用原型最大的好处

react设计思路

为什么虚拟DOM比真实DOM性能好

react常见的通信方式

redux整体的工作流程

redux和全局对象之间的区别

Redux数据回溯设计思路

单例、工厂、观察者项目中实际场景

项目中树的使用场景以及了解

工作收获



## 酷家乐
react生命周期

react性能优化

添加原生事件不移除为什么会内存泄露

还有哪些地方会内存泄露

setInterval需要注意的点

定时器为什么是不精确的

setTimeout(1)和setTimeout(2)之间的区别

介绍宏任务和微任务

promise里面和then里面执行有什么区别

介绍pureComponet

介绍Function Component

React数据流

props和state的区别

介绍react context

介绍class和ES5的类以及区别

介绍箭头函数和普通函数的区别

介绍defineProperty方法，什么时候需要用到

for..in 和 object.keys的区别

介绍闭包，使用场景

使用闭包特权函数的使用场景

get和post有什么区别



## 百分点
React15/16.x的区别

重新渲染render会做些什么

哪些方法会触发react重新渲染

state和props触发更新的生命周期分别有什么区别

setState是同步还是异步

对无状态组件的理解

介绍Redux工作流程

介绍ES6的功能

let、const以及var的区别

浅拷贝和深拷贝的区别

介绍箭头函数的this

介绍Promise和then

介绍快速排序

算法：前K个最大的元素



## 海风教育 
对react看法，它的优缺点 

使用过程中遇到的问题，如何解决的 

react的理念是什么（拿函数式编程来做页面渲染）

JS是什么范式语言(面向对象还是函数式编程)

koa原理，为什么要用koa(express和koa对比) 

使用的koa中间件 

ES6使用的语法 

Promise 和 async/await 和 callback的区别 

Promise有没有解决异步的问题（promise链是真正强大的地方）

Promise和setTimeout的区别（Event Loop）

进程和线程的区别（一个node实例就是一个进程，node是单线程，通过事件循环来实现异步 

）

介绍下DFS深度优先 

介绍下观察者模式 

观察者模式里面使用的数据结构(不具备顺序 ，是一个list) 

