## 腾讯面试

第一场

### 面试官一
1. 自我介绍
2. setState 的过程
3. react为什么需要用到key
4. function Component    Component和PureComponent的不同点
    参考文章  http://www.php.cn/js-tutorial-398067.html
    Component和PureComponent有一个不同点
    除了为你提供了一个具有浅比较的shouldComponentUpdate方法，PureComponent和Component基本上完全相同。当props或者state改变时，PureComponent将对props和state进行浅比较。另一方面，Component不会比较当前和下个状态的props和state。因此，每当shouldComponentUpdate被调用时，组件默认的会重新渲染。
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
6. 闭包的自增实现  
7. 了解原型链吗
   prototype和__proto__的区别
   https://www.cnblogs.com/libin-1/p/5820550.html
8. 跨域及如何跨域  同源策略 同域名不同端口   不同协议算不算跨域
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
9. 如何提高浏览器端的效率  静态资源缓存
10. promise的状态  异步的同步写法
11. for 循环 console.log 输出的结果 为什么 及如何输出 1 2 3
12. 如何实现一个向下滑动的vue组件
13. 有什么想问的问题



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
1. Linux 754 介绍

2. 介绍冒泡排序，选择排序，冒泡排序如何优化

3. transform动画和直接使用left、top改变位置有什么优缺点
   动画修改一个元素的 left 和 top会改变它的形状，而且可能引起页面上其它元素的移动和形状改变，这个过程称为布局。基于 CSS 的动画和原生支持的 Web 动画通常在称为合成器线程的线程上处理，transforms 和 opacity 都可以在合成器线程中处理；它与浏览器的主线程不同，在该主线程中执行样式，布局，绘制和 JavaScript。这意味着如果浏览器在主线程上运行一些耗时的任务，这些动画可以继续运行而不会中断；如果任何动画出发了绘制，布局，或者两者，那么主线程会来完成该工作。这个对基于 CSS 还是 JavaScript 实现的动画都一样，布局或者绘制的开销巨大，让与之关联的 CSS 或 JavaScript 执行工作、渲染都变得毫无意义；避免使用触发布局或绘制的属性动画。对于大多数现代浏览器，这意味着将动画（修改的属性）限制为 opacity 和 transform；
    所以：在你修改left和top上，transform：translate（x, y）和left：xpx;top：ypx在性能上有区别，效果上可能会有区别

4. 如何判断链表是否有环

5. 介绍二叉搜索树的特点

6. 介绍暂时性死区

7. ES6中的map和原生的对象有什么区别
   区别:
    object和Map存储的都是键值对组合。但是：
    object的键的类型是 字符串；
    map的键的类型是 可以是任意类型；
    另外注意，object获取键值使用Object.keys（返回数组）；
    Map获取键值使用 map变量.keys() (返回迭代器)。

8. 观察者和发布-订阅的区别

9.  react异步渲染的概念,介绍Time Slicing 和 Suspense

10. 16.X声明周期的改变
    getDerivedStateFromProps——用来替换componentWillReceiveProps,并用更安全的方式
11. 16.X中props改变后在哪个生命周期中处理
    getDerivedStateFromProps——用来替换componentWillReceiveProps,并用更安全的方式

12. 介绍纯函数
    一个函数的返回结果只依赖于它的参数，并且在执行过程里面没有副作用，我们就把这个函数叫做纯函数。

    为什么要煞费苦心地构建纯函数？因为纯函数非常“靠谱”，执行一个纯函数你不用担心它会干什么坏事，它不会产生不可预料的行为，也不会对外部产生影响。不管何时何地，你给它什么它就会乖乖地吐出什么。如果你的应用程序大多数函数都是由纯函数组成，那么你的程序测试、调试起来会非常方便。

13. 前端性能优化
    参考链接： https://www.cnblogs.com/MarcoHan/p/5295398.html

    前端是庞大的，包括 HTML、 CSS、 Javascript、Image 、Flash等等各种各样的资源。前端优化是复杂的，针对方方面面的资源都有不同的方式。那么，前端优化的目的是什么 ?
    　　1. 从用户角度而言，优化能够让页面加载得更快、对用户的操作响应得更及时，能够给用户提供更为友好的体验。
    　　2. 从服务商角度而言，优化能够减少页面请求数、或者减小请求所占带宽，能够节省可观的资源。
    　　总之，恰当的优化不仅能够改善站点的用户体验并且能够节省相当的资源利用。
    　　前端优化的途径有很多，按粒度大致可以分为两类，第一类是页面级别的优化，例如 HTTP请求数、脚本的无阻塞加载、内联脚本的位置优化等 ;第二类则是代码级别的优化，例如 Javascript中的DOM 操作优化、CSS选择符优化、图片优化以及 HTML结构优化等等。另外，本着提高投入产出比的目的，后文提到的各种优化策略大致按照投入产出比从大到小的顺序排列。
    　　一、页面级优化
    　　1. 减少 HTTP请求数
    　　这条策略基本上所有前端人都知道，而且也是最重要最有效的。都说要减少 HTTP请求，那请求多了到底会怎么样呢 ?首先，每个请求都是有成本的，既包含时间成本也包含资源成本。一个完整的请求都需要经过 DNS寻址、与服务器建立连接、发送数据、等待服务器响应、接收数据这样一个 “漫长” 而复杂的过程。时间成本就是用户需要看到或者 “感受” 到这个资源是必须要等待这个过程结束的，资源上由于每个请求都需要携带数据，因此每个请求都需要占用带宽。另外，由于浏览器进行并发请求的请求数是有上限的 (具体参见此处 )，因此请求数多了以后，浏览器需要分批进行请求，因此会增加用户的等待时间，会给用户造成站点速度慢这样一个印象，即使可能用户能看到的第一屏的资源都已经请求完了，但是浏览器的进度条会一直存在。
    　　减少 HTTP请求数的主要途径包括：
    　　(1). 从设计实现层面简化页面
    　　如果你的页面像百度首页一样简单，那么接下来的规则基本上都用不着了。保持页面简洁、减少资源的使用时最直接的。如果不是这样，你的页面需要华丽的皮肤，则继续阅读下面的内容。
    　　(2). 合理设置 HTTP缓存
    　　缓存的力量是强大的，恰当的缓存设置可以大大的减少 HTTP请求。以有啊首页为例，当浏览器没有缓存的时候访问一共会发出 78个请求，共 600多 K数据 (如图 1.1)，而当第二次访问即浏览器已缓存之后访问则仅有 10个请求，共 20多 K数据 (如图 1.2)。 (这里需要说明的是，如果直接 F5刷新页面的话效果是不一样的，这种情况下请求数还是一样，不过被缓存资源的请求服务器是 304响应，只有 Header没有Body ，可以节省带宽 )
    　　怎样才算合理设置 ?原则很简单，能缓存越多越好，能缓存越久越好。例如，很少变化的图片资源可以直接通过 HTTP Header中的Expires设置一个很长的过期头 ;变化不频繁而又可能会变的资源可以使用 Last-Modifed来做请求验证。尽可能的让资源能够在缓存中待得更久。关于 HTTP缓存的具体设置和原理此处就不再详述了，有兴趣的可以参考下列文章：
    HTTP1.1协议中关于缓存策略的描述
    Fiddler HTTP Performance中关于缓存的介绍
    　　(3). 资源合并与压缩
    　　如果可以的话，尽可能的将外部的脚本、样式进行合并，多个合为一个。另外， CSS、 Javascript、Image 都可以用相应的工具进行压缩，压缩后往往能省下不少空间。
    　　(4). CSS Sprites
    　　合并 CSS图片，减少请求数的又一个好办法。
    　　(5). Inline Images
    　　使用 data: URL scheme的方式将图片嵌入到页面或 CSS中，如果不考虑资源管理上的问题的话，不失为一个好办法。如果是嵌入页面的话换来的是增大了页面的体积，而且无法利用浏览器缓存。使用在 CSS中的图片则更为理想一些。
    　　(6). Lazy Load Images（自己对这一块的内容还是不了解）
    　　这条策略实际上并不一定能减少 HTTP请求数，但是却能在某些条件下或者页面刚加载时减少 HTTP请求数。对于图片而言，在页面刚加载的时候可以只加载第一屏，当用户继续往后滚屏的时候才加载后续的图片。这样一来，假如用户只对第一屏的内容感兴趣时，那剩余的图片请求就都节省了。 有啊首页 曾经的做法是在加载的时候把第一屏之后的图片地址缓存在 Textarea标签中，待用户往下滚屏的时候才 “惰性” 加载。

    　　1. 将外部脚本置底（将脚本内容在页面信息内容加载后再加载）
    　　前文有谈到，浏览器是可以并发请求的，这一特点使得其能够更快的加载资源，然而外链脚本在加载时却会阻塞其他资源，例如在脚本加载完成之前，它后面的图片、样式以及其他脚本都处于阻塞状态，直到脚本加载完成后才会开始加载。如果将脚本放在比较靠前的位置，则会影响整个页面的加载速度从而影响用户体验。解决这一问题的方法有很多，在 这里有比较详细的介绍 (这里是译文和 更详细的例子 )，而最简单可依赖的方法就是将脚本尽可能的往后挪，减少对并发下载的影响。
    　　1. 异步执行 inline脚本(其实原理和上面是一样，保证脚本在页面内容后面加载。)
    　　inline脚本对性能的影响与外部脚本相比，是有过之而无不及。首页，与外部脚本一样， inline脚本在执行的时候一样会阻塞并发请求，除此之外，由于浏览器在页面处理方面是单线程的，当 inline脚本在页面渲染之前执行时，页面的渲染工作则会被推迟。简而言之， inline脚本在执行的时候，页面处于空白状态。鉴于以上两点原因，建议将执行时间较长的 inline脚本异步执行，异步的方式有很多种，例如使用 script元素的defer 属性(存在兼容性问题和其他一些问题，例如不能使用 document.write)、使用setTimeout ，此外，在HTML5中引入了 Web Workers的机制，恰恰可以解决此类问题。

    　　1. Lazy Load Javascript（只有在需要加载的时候加载，在一般情况下并不加载信息内容。）
    　　随着 Javascript框架的流行，越来越多的站点也使用起了框架。不过，一个框架往往包括了很多的功能实现，这些功能并不是每一个页面都需要的，如果下载了不需要的脚本则算得上是一种资源浪费 -既浪费了带宽又浪费了执行花费的时间。目前的做法大概有两种，一种是为那些流量特别大的页面专门定制一个专用的 mini版框架，另一种则是 Lazy Load。YUI 则使用了第二种方式，在 YUI的实现中，最初只加载核心模块，其他模块可以等到需要使用的时候才加载。

    　　1. 将 CSS放在 HEAD中
    　　如果将 CSS放在其他地方比如 BODY中，则浏览器有可能还未下载和解析到 CSS就已经开始渲染页面了，这就导致页面由无 CSS状态跳转到 CSS状态，用户体验比较糟糕。除此之外，有些浏览器会在 CSS下载完成后才开始渲染页面，如果 CSS放在靠下的位置则会导致浏览器将渲染时间推迟。
    　　1. 异步请求 Callback（就是将一些行为样式提取出来，慢慢的加载信息的内容）
    　　在某些页面中可能存在这样一种需求，需要使用 script标签来异步的请求数据。类似：
    　　Javascript:
    /*Callback 函数*/ 
    function myCallback(info){ 
    //do something here 
    } 
    　　HTML:

    　　cb返回的内容 :
    myCallback('Hello world!');
    像以上这种方式直接在页面上写 <script>对页面的性能也是有影响的，即增加了页面首次加载的负担，推迟了 DOMLoaded和window.onload 事件的触发时机。如果时效性允许的话，可以考虑在 DOMLoaded事件触发的时候加载，或者使用 setTimeout方式来灵活的控制加载的时机。
    　　1. 减少不必要的 HTTP跳转
    　　对于以目录形式访问的 HTTP链接，很多人都会忽略链接最后是否带 ’/'，假如你的服务器对此是区别对待的话，那么你也需要注意，这其中很可能隐藏了 301跳转，增加了多余请求。具体参见下图，其中第一个链接是以无 ’/'结尾的方式访问的，于是服务器有了一次跳转。
    　　1. 避免重复的资源请求
    　　这种情况主要是由于疏忽或页面由多个模块拼接而成，然后每个模块中请求了同样的资源时，会导致资源的重复请求

    　　二、代码级优化
    　　1. Javascript
    　　(1). DOM
    　　DOM操作应该是脚本中最耗性能的一类操作，例如增加、修改、删除 DOM元素或者对 DOM集合进行操作。如果脚本中包含了大量的 DOM操作则需要注意以下几点：
    　　a. HTML Collection（HTML收集器，返回的是一个数组内容信息）
    　　在脚本中 document.images、document.forms 、getElementsByTagName()返回的都是 HTMLCollection类型的集合，在平时使用的时候大多将它作为数组来使用，因为它有 length属性，也可以使用索引访问每一个元素。不过在访问性能上则比数组要差很多，原因是这个集合并不是一个静态的结果，它表示的仅仅是一个特定的查询，每次访问该集合时都会重新执行这个查询从而更新查询结果。所谓的 “访问集合” 包括读取集合的 length属性、访问集合中的元素。
    　　因此，当你需要遍历 HTML Collection的时候，尽量将它转为数组后再访问，以提高性能。即使不转换为数组，也请尽可能少的访问它，例如在遍历的时候可以将 length属性、成员保存到局部变量后再使用局部变量。
    　　b. Reflow & Repaint
    　　除了上面一点之外， DOM操作还需要考虑浏览器的 Reflow和Repaint ，因为这些都是需要消耗资源的，具体的可以参加以下文章：
    如何减少浏览器的repaint和reflow?
    Understanding Internet Explorer Rendering Behaviour
    Notes on HTML Reflow

    　　(2). 慎用 with
    with(obj){ p = 1}; 代码块的行为实际上是修改了代码块中的 执行环境 ，将obj放在了其作用域链的最前端，在 with代码块中访问非局部变量是都是先从 obj上开始查找，如果没有再依次按作用域链向上查找，因此使用 with相当于增加了作用域链长度。而每次查找作用域链都是要消耗时间的，过长的作用域链会导致查找性能下降。
    　　因此，除非你能肯定在 with代码中只访问 obj中的属性，否则慎用 with，替代的可以使用局部变量缓存需要访问的属性。
    　　(3). 避免使用 eval和 Function
    　　每次 eval 或 Function 构造函数作用于字符串表示的源代码时，脚本引擎都需要将源代码转换成可执行代码。这是很消耗资源的操作 —— 通常比简单的函数调用慢 100倍以上。
    　　eval 函数效率特别低，由于事先无法知晓传给 eval 的字符串中的内容，eval在其上下文中解释要处理的代码，也就是说编译器无法优化上下文，因此只能有浏览器在运行时解释代码。这对性能影响很大。
    　　Function 构造函数比 eval略好，因为使用此代码不会影响周围代码 ;但其速度仍很慢。
    　　此外，使用 eval和 Function也不利于Javascript 压缩工具执行压缩。
    　　(4). 减少作用域链查找（这方面设计到一些内容的相关问题）
    　　前文谈到了作用域链查找问题，这一点在循环中是尤其需要注意的问题。如果在循环中需要访问非本作用域下的变量时请在遍历之前用局部变量缓存该变量，并在遍历结束后再重写那个变量，这一点对全局变量尤其重要，因为全局变量处于作用域链的最顶端，访问时的查找次数是最多的。
    　　低效率的写法：
    // 全局变量 
    var globalVar = 1; 
    function myCallback(info){ 
    for( var i = 100000; i--;){ 
    //每次访问 globalVar 都需要查找到作用域链最顶端，本例中需要访问 100000 次 
    globalVar += i; 
    }
    } 
    　　更高效的写法：
    // 全局变量 
    var globalVar = 1; 
    function myCallback(info){ 
    //局部变量缓存全局变量 
    var localVar = globalVar; 
    for( var i = 100000; i--;){ 
    //访问局部变量是最快的 
    localVar += i; 
    } 
    //本例中只需要访问 2次全局变量
    在函数中只需要将 globalVar中内容的值赋给localVar 中区
    globalVar = localVar; 
    }
    　　此外，要减少作用域链查找还应该减少闭包的使用。
    　　(5). 数据访问
    　　Javascript中的数据访问包括直接量 (字符串、正则表达式 )、变量、对象属性以及数组，其中对直接量和局部变量的访问是最快的，对对象属性以及数组的访问需要更大的开销。当出现以下情况时，建议将数据放入局部变量：
    　　a. 对任何对象属性的访问超过 1次
    　　b. 对任何数组成员的访问次数超过 1次
    　　另外，还应当尽可能的减少对对象以及数组深度查找。
    　　(6). 字符串拼接
    　　在 Javascript中使用"+" 号来拼接字符串效率是比较低的，因为每次运行都会开辟新的内存并生成新的字符串变量，然后将拼接结果赋值给新变量。与之相比更为高效的做法是使用数组的 join方法，即将需要拼接的字符串放在数组中最后调用其 join方法得到结果。不过由于使用数组也有一定的开销，因此当需要拼接的字符串较多的时候可以考虑用此方法。

    　　关于 Javascript优化的更详细介绍请参考：
    Write Efficient Javascript(PPT)
    Efficient JavaScript
    　　1. CSS选择符
    　　在大多数人的观念中，都觉得浏览器对 CSS选择符的解析式从左往右进行的，例如
    #toc A { color: #444; }
    　　这样一个选择符，如果是从右往左解析则效率会很高，因为第一个 ID选择基本上就把查找的范围限定了，但实际上浏览器对选择符的解析是从右往左进行的。如上面的选择符，浏览器必须遍历查找每一个 A标签的祖先节点，效率并不像之前想象的那样高。根据浏览器的这一行为特点，在写选择符的时候需要注意很多事项，有人已经一一列举了， 详情参考此处。

    　　1. HTML
    　　对 HTML本身的优化现如今也越来越多的受人关注了，详情可以参见这篇 总结性文章 。

    　　1. Image压缩
    　　图片压缩是个技术活，不过现如今这方面的工具也非常多，压缩之后往往能带来不错的效果，具体的压缩原理以及方法在《 Even Faster Web Sites》第10 章有很详细的介绍，有兴趣的可以去看看。
    　　总结
    　　本文从页面级以及代码级两个粒度对前端优化的各种方式做了一个总结，这些方法基本上都是前端开发人员在开发的过程中可以借鉴和实践的，除此之外，完整的前端优化还应该包括很多其他的途径，例如 CDN、 Gzip、多域名、无 Cookie服务器等等，由于对于开发人员的可操作性并不强大，在此也就不多叙述了，详细的可以参考 Yahoo和Google 的这些“金科玉律 

14. pureComponent和FunctionComponent区别
    我开始转向使用PureCompoent是因为它是一个更具性能的Component的版本。虽然事实证明这是正确的，但是这种性能的提高还伴随着一些附加的条件。让我们深挖一下PureComponent，并理解为什么我们应该使用它。

    Component和PureComponent有一个不同点
    除了为你提供了一个具有浅比较的shouldComponentUpdate方法，PureComponent和Component基本上完全相同。当props或者state改变时，PureComponent将对props和state进行浅比较。另一方面，Component不会比较当前和下个状态的props和state。因此，每当shouldComponentUpdate被调用时，组件默认的会重新渲染。

    浅比较101
    当把之前和下一个的props和state作比较，浅比较将检查原始值是否有相同的值（例如：1 == 1或者ture==true）,数组和对象引用是否相同。

15. 介绍JSX

16. 如何做RN在安卓和IOS端的适配

17. RN为什么能在原生中绘制成原生组件（bundle.js）

18. 介绍虚拟DOM

19. 如何设计一个localStorage，保证数据的实效性

20. 如何设计Promise.all()

21. 介绍高阶组件

22. sum(2, 3)实现sum(2)(3)的效果

23. react性能优化

24. 两个对象如何比较



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
1. ES6新的特性

2. 介绍Promise

    Promise有几个状态
    pending、fulfilled、rejected(未决定，履行，拒绝)，同一时间只能存在一种状态,且状态一旦改变就不能再变。promise是一个构造函数，promise对象代表一项有两种可能结果（成功或失败）的任务，它还持有多个回调，出现不同结果时分别发出相应回调。

    1.初始化，状态：pending
    ​
    2.当调用resolve(成功)，状态：pengding=>fulfilled
    ​
    3.当调用reject(失败)，状态：pending=>rejected


说一下闭包

React的生命周期

componentWillReceiveProps的触发条件是什么

React16.3对生命周期的改变

介绍下React的Fiber架构

画Fiber渲染树

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
1. localStorage和cookie有什么区别

2. CSS选择器有哪些

3. 盒子模型，以及标准情况和IE下的区别

4. 如何实现高度自适应

5. prototype和——proto——区别

6. _construct是什么

7. new是怎么实现的
    new操作符具体干了什么呢?其实很简单，就干了三件事情。
8. promise的精髓，以及优缺点

9. 如何实现H5手机端的适配

10. rem、flex的区别（root em）

11. em和px的区别

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

