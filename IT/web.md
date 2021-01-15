<div class="title">
<img src="E:\package\VNote\IT\_v_images/kj0.jpg"/>
<h2>web前端</h2><h4>——酷炫的界面。</h4>
</div>

### 一、HTML
#### 1、svg：
```html
<svg width="300" height="300" xmlns="http://www.w3.org/2000/svg" version="1.1"></svg>

<!--xmlns：xlink表示前缀为xlink的元素应该由理解该规范的UA使用xlink规范来解释.
xmlns定义了默认命名空间,因此不需要前缀,-->

<!--rx，ry控制圆角-->
<rect x="" y="" width="" rx="10" ry="20" height="" style="fill:red;stroke-width:2;stroke:blue;"/>
//rect标签绘制矩形，x,y为位置,fill,stroke等属性可写在style外。
<circle cx="" cy="" r=""/>绘制圆，cx,cy为位置。
<ellipse cx="" cy="" rx="" ry=""/>绘制椭圆，cx,cy为位置，rx,ry为宽高。
<line x1="0" y1="0" x2="20" y2="20"/>绘制线条，x1,y1,x2,y2为起始及结尾坐标。
<polygon points="10,10 20,20 150,320"/>绘制多边形，points中没两个值是一对坐标。
<polyline points=""/>绘制折线
<path d="M10 5L100 15C19 60,50 99"/>绘制任意路径、形状。d中属性如下：

<g></g><!--其它元素可以放到里面，做一组使用，无其它实意-->
<defs><!--用于定义模板，其它标签用xlink引用-->
    <path id="a1" d="M0 50 C150 150 100 -50 300 50" stroke="#000" fill="none"/>
</defs>
<text x="10" y="15">
    <!--text用于在svg中放置文字-->
    <textPath xlink:href="#a1">在平坦的路上曲折前行</textPath>
</text>
```
M：移动至起始点，必须。L：直线结束点。H：从当前点画水平线。V:垂直线。C:三阶贝塞尔曲线。Q：二阶贝塞尔曲线。
(将元素使用appendChild()方法动态添加到svg中并不会被显示出来,可以使用svg.innerHTML方法将元素写入)。[基础部分学习地址](http://www.mamicode.com/info-detail-1988813.html)
**svg内联**：css的background-img的url可以显示链接图片和base64图片，将svg转为base64的也能在其中显示出来，部分版本较高的浏览器可以直接用svg代码，如下：
```css
.aa{
    background:url('data:image/svg+xml;utf8,<svg version="1.1" xmlns="http://www.w3.org/2000/svg" version="1.1">...');
}
/*ie和一些浏览器中不能显示出来，但可以使用
-------js的encodeURIComponent()方法将其转码后使用,注意需要xmlns属性：
*/
.bb{
    background: url(data:image/svg+xml,%3Csvg%...) no-repeat center;
}
/*这种内联的svg渲染几乎无延迟*/
```

**table的使用**：
```html
<table border="1" cellspacing="0">
<thead><!--border为线宽，cellspacing为格间距-->
<tr><th></th></tr>
</thead>
<tbody>
<tr><td rowspan="2" colspan="3"></td></tr>
</tbody>
</table>
```
#### 2、页面渲染过程：
- 先向服务端请求html网页。对html内容由上至下进行扫描，然后从头加载。
- 由上至下将内容构建DOM树和CSSOM树。
- 如果中途遇到css请求资源的加载会先请求css资源，然后加入到cssom树的构建中。
- 若中途遇到js，会先阻塞DOM树，因为js可以操作DOM。
- 两颗树构建完成之后会构建渲染树，由cssom树和dom树合并而成。
- [参考学习地址。](https://www.cnblogs.com/chenyoumei/p/9156849.html)

**页面的重绘与重排**（回流）：元素颜色的改变、css3的一些变换等会引起页面的重绘，不过重绘速度非常快。而元素大小、display、position、float、overflow，js的resize等会导致对页面的重新布局，即重排（也称回流）。无论是渲染树构建过程和渲染完毕后。回流比重绘需要的时间多得多，**所以应该尽量避免重排**。
#### 3、第三方资源的加载：
前端中有很多加载资源的标签例：iframe,video,audio,img,script,link等是用src属性或是用href属性，一些标签不能跨域加载资源多数标签允许跨域加载资源。除了link和script外其它标签几乎都有onload事件和onerror事件可在元素上添加这两个事件做加载成功和加载失败后的处理。js代码中的函数块语句需要达到相应的条件才能触发（body，head中添加的onload和`<script></script>`中的window.onload=“”除外)就算是onmouseout指定的函数也不行，因为它运行的前提就是有onmouseover被触发。
外部资源引入标签：
`<embed></embed>、<iframe></iframe>、<object></object>`
`<embed type="image/svg+xml" codebase="http:"></embed>`标签是H5新标签所有主流浏览器都支持，codebase属性中写资源路径,可以引入脚本;类似iframe标签用于引	入外资源(`<iframe>`标签只在大部分浏览器可用),但规范的xhtml和html中不支持`<embed>`标签.`<object data="rect.svg" type="image/svg+xml" codebase="http">	`
`</object>`1标签是H4的新标签，浏览器支持性差，但不能引入脚本.(引入的文件中的js对象和本页的js对象是不能共用的,且在引入的文件中获取的url也不是该页的)
#### 4、canvas:
`<canvas width="500" height="500"></canvas>`
HTMLCanvasElement//表示页面内所有canvas元素，其余元素也有此类似对象。
HTMLCanvasElement.toDataURL()方法将画布转化为base64图片格式。
HTMLCanvasElement.toBlob()方法将画布转化为Blob对象。

var ctx = canvas.getContext("2d")//获取2d对象
ctx.fillStyle = "blue"//填充颜色需要放在绘制形状前
ctx.fillRect(x,y,width,height)//矩形填充颜色...
ctx.clearRect(x,y,width,height)//矩形清除图像像素
ctx.strokeRect(x,y,width,height)//绘制一个矩形框
ctx.fillText("str",x,y)//填充文字时不能填充其它且不能绘制形状。
ctx.font = "20px Arial"//定义字体大小及类型。
ctx.textAlign='center'//left,start,right,end
ctx.beginPath()//绘制路径，不规则图圆时先调用
ctx.lineWidth=3;//线框
ctx.filter='blur(15px)';//模糊滤镜。
ctx.lineCap="butt"//线头样式,round:圆形头、square:方形头。
ctx.setLineDash([2,5,20,30])//设置为虚线，断点距头位置。
ctx.lineDashOffset=10//设置虚线起始偏离起始点距离。
a = ctx.createLinearGradient(0,0,300,0);//创建一个线性渐变，参数为区域
a.addColorStop(0,"red");//渐变a中添加位置,颜色
b=ctx.createRadialGradient(x0,y0,r0,x1,y1,r1)//中心渐变，两个圆中间的区域
patt=ctx.createPattern(ct1,null)//创建一个填充块，参数1是另一个canvas对象
可将canvas对象ct1填充到canvas对象ctx中。
ctx.shadowBlur=20//阴影模糊程度
ctx.shadowColor="red"//阴影颜色
ctx.shadowOffsetX=2,ctx.shadowOffsetY=3//阴影偏移
ctx.strokeStyle="orange"//设置边框颜色
坐标若超出canva画布大小则全部都不能绘制出来
ctx.quadraticCurveTo(10,10,20,20)//二次贝塞尔曲线，中转点，结束点
ctx.bezierCurveTo()//三次贝塞尔曲线
`ctx.arc(x,y,r,stAngle,Math.PI*2)`//绘制圆,控制第5个参数大小控制弧长。
ctx.ellipse(x,y,rx,ry,Math.PI/4)//绘制椭圆
画圆，椭圆前定义lineWidth值填充strokeStyle值可画出圆环效果。
ctx.clip()//裁剪，使用之前先绘制一个路径区域再调用,裁剪掉区域外的东西
ctx.stroke()//绘制所描绘的路径
ctx.translate(10,10)//画布圆心位置移动,ctx.scale(0.1,0.1)//缩放,
ctx.rotate(Math.PI*30/180)//旋转,(在绘制时若多个变换一起使用需要先使用
translate()变换否则出现的位置与设计的不一致)
ctx.globalAlpha=0.2;//设置画布全局透明度
img=new Image()//继承Image类，img.src="mv.jpg"//获取图片文件像素数据。
img.width、img.height、img.data//直接获取该图片的宽高，像素数据。
ctx.drawImage(img,dx,dy,width,height)//绘制图片,img可以是图片、svg、canvas
图形对象(不写width和height时自己会计算宽高);该方法写在img.onload=function(){}内。
imgdata=ctx.createImageData(300,100)//创建一个全0像素矩阵,可操控每个点值
使用imgdata.data[0]=230;这种形式改变。
dat=ctx.getImageData(x,y,width,height);//dat.data获取像素矩阵，
getImageData()方法能获取canvas上任意图形的像素数据。
img.src =canvas.toDataURL(type,scl);//将整个canvas上的像素数据转换为
base64格式,能直接显示到img中,type有图片格式,有:image/png(默认),
image/jpeg,image/webp;scl为缩放值(更改图片质量0~1)
ctx.putImageData(imgdata,x,y)//重绘imgdata
ctx.save()//保存当前画布状态到栈空间，restore()方法依次取出。需要配合使用
save()方法放绘制的开头，restore(）方法放绘制的结尾。
ctx.globalCompositeOperation="source-over"//图形重叠处理，source-in:重叠部分绘制，source-out:重叠位置不绘制、source-atop:重叠处类似遮罩的绘制、lighter:颜色叠加效果、copy:只显示新内容、xor:互相重叠部分为透明、multiply:顶层像素与底层像素相乘，一般得到黑暗图形、screen:重叠处像素反转、overlay:multiply与screen叠加效果、darken:变暗
lighten:叠加部分变量、color-dodge:底层像素值除顶层像素值、color-burn:颜色加深。底部图层的色值除以顶部图层色值，得到的结果再反相、hard-light:重叠处强光、soft-light:柔光......
(利用globalCompositeOperation中的copy属性可以实现图形的位移、旋转)(如果要用一个2d对象绘制多个图形且让其能产生动画效果那么需要在每个绘制图形前都加一个globalCompositeOperation,属性值不为copy即可)
```js
var cn = document.getElementById("canvas");
function play(){
    var cv = cn.getContext("2d");
    // 以下两个图形用一个2d对象绘制。
    cv.globalCompositeOperation = "copy";
    cv.beginPath();
    cv.moveTo(10,20);
    cv.lineTo(150,230);
    cv.stroke();
    // 绘制另一个图形中间添加globalCompositeOperation属性
   cv.globalCompositeOperation = "source-over";
   //cv.save();若只想用transform中的方法产生动画在这里加上save()末尾用
   //restore()即可产生想要的结果。
   cv.beginPath();
   cv.moveTo(50,200);
   cv.lineTo(310,430);
   cv.stroke();
   cv.restore();
   // 使用这种模式，以上值处改为动态值即可产生动画
   requestAnimationFrame(play);
}

```
用for循环绘制多个图形：
```js
var can = document.getElementById("can");
var ttx = can.getContext("2d");
for(var i=0;i<3;i++){
ttx.globalCompositeOperation = "source-over";
ttx.fillStyle = "blue";
ttx.fillRect(0,i*150,300,150);
ttx.fill();
}

```
只刷新一个画笔的图形：
```js
var can = document.getElementById('can');
var ctx1 = can.getContext('2d');
var ctx2 = can.getContext('2d');
// 一个画布上有两个画笔
ctx1.fillStyle = 'blue';
ctx1.fillRect(0,0,50,100);
ctx1.fill();
ctx2.fillStyle = 'red';
ctx2.fillRect(200,30,150,90);
ctx2.fill();
window.onkeydown = function(){
    //只想改变一个画笔的图形时加上save()和restore()方法。就不影响其它图形了
	ctx2.save();
	ctx2.globalCompositeOperation = 'source';
	ctx2.fillStyle = 'red';
	ctx2.fillRect(200,30,200,90);
	ctx2.fill();
	ctx2.restore();
}

```
第一个条语句用globalCompositeOperation可用for循环配合动态变量，绘制多个图形，放在动画代码中依然可用。
ctx.isPointInPath(x,y);ctx.isPointInStroke(x,y);//检测坐标点x,y是否在画笔对象ctx所绘制的图形中和边框上，canvas上绘制的图形与html元素在生成的方式、操作上不一样所以canvas绘制的图形不能用addEventLisener()来添加鼠标事件，所以可以借用以上这两个方法来添加鼠标事件效果。(不过这两个方法只支持使用begInPath()方法绘制出来的图形对象。)
#### 5、HTML转义字符对照表：
http://tool.oschina.net/commons?type=2
https://blog.csdn.net/chb_1_2/article/details/80728732
#### 6、meta标签属性大全：
`<meta name=”redaner”content=”webkit”/>`告诉浏览器用什么内核解析。[meta标签的使用学习地址。](https://blog.csdn.net/blue225/article/details/53894181%0A)

#### 9、概念
**位图与矢量图**：位图又叫做点阵图，是一个个很小的颜色小方块组合在一起的图片。一个小方块代表1px（像素）。矢量图是由一个个点链接在一起组成的，是根据几何特性来绘制的图像，和位图的分辨率是没有关系的。因此图片放大后也不会失真，不会出现位图的马赛克的样子，也就是说可以无限放大图片。
**各设备屏幕尺寸**：手机屏宽范围：300 – 768 px;        平板屏宽范围: 769 – 1199px;笔记本屏宽范围:1200 – 1400px;    台式，一体机屏宽范围:1401 – 1920px;广场电视机:1921 – 99999px。
**缓存**：缓存分为CDN缓存、数据库缓存、代理服务器缓存和浏览器缓存，浏览器的缓存问题主要指的是http缓存即协议层，H5新增的storage缓存 和数据库缓存是应用层缓存。（协议层缓存可以分为强制缓存和对比缓存)。
强制缓存：缓存失效时才会去服务器获取最新资源的方式，就是强制缓存,协议层中可以使用字段expires和cache-control。（暂未知）
对比缓存：先从缓存中获取对应的数据标识，然后向服务器发送请求,确认数据是否更新,如果更新则返回新数据和新缓存;反之返回304状态码（缓存可继续使用）浏览器行为引起的缓存变化：
(1)刷新网页：如果缓存没有失效浏览器会直接使用缓存；
(2)手动刷新（F5）：浏览器会认为缓存失效；
(3)强制刷新（ctrl+F5）：浏览器会直接忽略缓存；
**CDN**：Content Delivery Network，即内容分发网络。CDN是构建在现有网络基础之上的智能虚拟网络，依靠部署在各地的边缘服务器，通过中心平台的负载均衡、内容分发、调度等功能模块，使用户就近获取所需内容，降低网络拥塞，提高用户访问响应速度和命中率。CDN的关键技术主要有内容存储和分发技术。<b c=v>中小企业使用CDN一般是使用其它服务商提供的CDN服务，类似在域名解析处更改DNS地址即可。</b>
**OSS**：OSS 是一个分布式的对象存储服务，提供的是一个 Key-Value 对形式的对象存储服务。用户可以根据 Object 的名称（Key）唯一的获取该Object的内容。
- bucket：存储空间。同一个存储空间的内部是扁平的，没有文件系统的目录等概念，所有的对象都直接隶属于其对应的存储空间。存储空间的名称在 OSS 范围内必须是全局唯一的，一旦创建之后无法修改名称。
- 对象/文件：对象是 OSS 存储数据的基本单元，也被称为 OSS 的文件。对象由元信息（Object Meta），用户数据（Data）和文件名（Key）组成。对象由存储空间内部唯一的 Key 来标识。对象元信息是一个键值对，表示了对象的一些属性，比如最后修改时间、大小等信息，同时用户也可以在元信息中存储一些自定义的信息。
- 访问域名：Endpoint 表示 OSS 对外服务的访问域名。OSS 以 HTTP RESTful API 的形式对外提供服务，当访问不同的 Region 的时候，需要不同的域名。
- AccessKey：AccessKey，简称 AK，指的是访问身份验证中用到的 AccessKeyId 和AccessKeySecret。OSS 通过使用 AccessKeyId 和 AccessKeySecret 对称加密的方法来验证某个请求的发送者身份。AccessKeyId 用于标识用户，AccessKeySecret 是用户用于加密签名字符串和 OSS 用来验证签名字符串的密钥。
- [学习地址。](http://www.360doc.com/content/18/0823/22/49604565_780716594.shtml)
#### 10、web中的安全措施：
<i class="label1">a、sql注入</i>：通过输入框中输入一些sql的插入、删除等语句，在传到后台时被运行，然后操作数据库。防御：做一些正则匹配，替换输入中的特殊字符等，后台做一些站位等措施。
<i class="label1">b、XSS (Cross-Site Scripting)，跨站脚本攻击</i>因为缩写和 CSS重叠，所以只能叫 XSS。跨站脚本攻击是指通过存在安全漏洞的Web网站注册用户的浏览器内运行非法的HTML标签或JavaScript进行的一种攻击。
跨站脚本攻击有可能造成以下影响：利用虚假输入表单骗取用户个人信息。利用脚本窃取用户的Cookie值，被害者在不知情的情况下，帮助攻击者发送恶意请求。显示伪造的文章或图片。
<i class="label2">非持久型 XSS（反射型 XSS ）</i>：攻击者可以直接通过 URL (类似：https://xxx.com/xxx?default=<script>alert(document.cookie)</script>) 注入可执行的脚本代码。不过一些浏览器如Chrome其内置了一些XSS过滤器，可以防止大部分反射型XSS攻击。防御：Web 页面渲染的所有内容或者渲染的数据都必须来自于服务端。尽量不要从 URL，document.referrer，document.forms 等这种 DOM API 中获取数据直接渲染。尽量不要使用 eval, new Function()，document.write()，document.writeln()，window.setInterval()，window.setTimeout()，innerHTML，document.createElement() 等可执行字符串的方法。如果做不到以上几点，也必须对涉及 DOM 渲染的方法传入的字符串参数做 escape 转义。前端渲染的时候对任何的字段都需要做 escape 转义编码。
<i class="label2">持久型 XSS（存储型 XSS）</i>：持久型 XSS 漏洞，一般存在于 Form 表单提交等交互功能，如文章留言，提交文本信息等，黑客利用的 XSS 漏洞，将内容经正常功能提交进入数据库持久保存，当前端页面获得后端从数据库中读出的注入代码时，恰好将其渲染执行。防御：只允许加载本站资源Content-Security-Policy: default-src 'self'。只允许加载 HTTPS 协议图片：Content-Security-Policy: img-src https://*。允许加载任何来源框架：Content-Security-Policy: child-src 'none'
<i class="label1">c、CSRF</i>：CSRF(Cross Site Request Forgery)，即跨站请求伪造，是一种常见的Web攻击，它利用用户已登录的身份，在用户毫不知情的情况下，以用户的名义完成非法操作。
完成 CSRF 攻击必须要有三个条件：用户已经登录了站点 A，并在本地记录了 cookie。在用户没有登出站点 A 的情况下（也就是 cookie 生效的情况下），访问了恶意攻击者提供的引诱危险站点 B (B 站点要求访问站点A)。站点 A 没有做任何 CSRF 防御。
防御：防范 CSRF 攻击可以遵循以下几种规则：Get 请求不对数据进行修改。不让第三方网站访问到用户 Cookie。阻止第三方网站请求接口。请求时附带验证信息，比如验证码或者 Token
<i class="label1">d、点击劫持</i>：是一种视觉欺骗的攻击手段。攻击者将需要攻击的网站通过 iframe 嵌套的方式嵌入自己的网页中，并将 iframe 设置为透明，在页面中透出一个按钮诱导用户点击。
X-FRAME-OPTIONS是一个 HTTP 响应头，在现代浏览器有一个很好的支持。这个 HTTP 响应头 就是为了防御用 iframe 嵌套的点击劫持攻击。
该响应头有三个值可选，分别是：DENY，表示页面不允许通过 iframe 的方式展示。SAMEORIGIN，表示页面可以在相同域名下通过 iframe 的方式展示。ALLOW-FROM，表示页面可以在指定来源的 iframe 中展示。
[web端安全问题及应对方法。](https://www.cnblogs.com/pretty-sunshine/p/11442326.html)
#### 11、HTML5规范：
html5中加了一些新的规范，如下示例：[H5的一些新标签的使用学习地址。](https://www.cnblogs.com/nuanai/p/8856814.html)
```html
<! DOCTYPE html> //声明使用H5规范来解析文档。
<html>// html5中标签名可以用大写，但推荐使用小写。不要省略html,head,body标签。
<head></head>
<body> // 如果父元素中的子元素个数很少时可以不用缩进。每个标签都必须关闭。
<img src="" alt="HTML5"/> //alt能在图片加载失败时代替图片显示。
// 一行代码尽量少于80个字符。少一些不必要的空行和缩进。
</body>
</html>
```
#### 12、十大经典排序算法：
分为两类排序：非线性时间比较类排序(通过比较来决定元素间的排序)，线性时间非比较类排序(不通过比较来决定元素间的排序)。(以下均是以从小到大的排序为从下到大)
**冒泡排序**：for(var i=0;i<arr.length-1;i++){for(var j=0;j<arr.length-i-1;j++){}}对比相邻两个元素的大小排序，执行数组长度-1次即可排完。(i<len(dat)-1)
选择排序****：从中选择最大或最小的值放到开头，再从剩余之中重复次操作。
**插入排序**：从数组位置1开始然后比较0，1位置排序，再选择2位置在0，1，2中比较排序，...
**希尔排序**：简单插入排序的改进版，分为3次进行排序(以长度为10的数组举例)，第一次将整个数组分为2份第6个与第1个对比若不符合顺序则交换位置，第7个与第2个比较若不符合则交换顺序...，第次排序则奇数位与奇数位比较，下标偶数的比较，第2个与第0个比较若不符合顺序则交换位置，第4个与第2个比较不符合则交换位置...偶数位拍完后排奇数位的，第3个与第1个比较不符合则交换位置...，第三次排序从第二个开始与第一个比较若不符合则交换顺序，第3个与第2个比较若不符合则再与第一个比较，若符合则插入到第二个前，若不符合则插入到第1个前...
**快速排序**：快速排序是冒泡排序的改进，假设有一个n长度的数组从中任选一个做为基数(一般选择第一个,这里选下标0)。从下标1开始与第0个比较找到第一个小于该基数的数(若没找到则该基数为最小。再以下标1的为基数执行以上步骤)设其下标为j则将下标j与0的数互换位置再从前向后找用下标1,2..的数与基数也就是位置j的数比较找到第一个大于它的数与其交换位置。(若没找到则下标为j的数已将该数组分为两部分再将这两个子数组分别用以上步骤排序)，再从j-1从后向前开始与比较与下标j的数据比较找到第一个比下标j大的数和其互换...直到该分区不可分组为止，对下标j左右的两个子数组再此使用此法排序。
**堆排序**：堆排序就是利用堆这种数据结构建立的一种排序(堆结构就是一颗完全二叉树，节点的值按从上到下从做到有的大小顺序排列)，步骤：先根据数组建立一颗完全二叉树然后根据大顶堆(根节点大于两个子节点)的结构从树的最低部向上调整左子树和右子树，调整好后比较根节点与左右子节点比较选择最大的一个做为根节点，然后将该根节点与右子树最底层最右边的节点与根节点值互换(因为安照堆结构最大的值放最右下脚,其余依次放置)然后再从根节点向下按大顶堆的结构调整树结构(先调整右子树因为得保证右子树最底部的节点值是整个数据中最大的几个)右子树最底部节点值都调为最大值后再用此方法调整左子树，整颗树最底部都调为最大值后并不再考虑最低层的值，再重复上面的方法将倒数第二层的节点...。
**计数排序**：例：有待排序的数组a和一个空数组b，求出a的最大最小值确定b的长度，扫描a根据其值依次将其放到b中对应下标位置处(如a[0]=12，a中为12的值的有3个那b[12]=3)全部放置完成后清空a将b中有值的位置根据其下标做为值放到a中。
桶排序：桶排序是计数排序的升级版，求出带排数组的最大最小值确定好桶数(空数组数)，分段的将其分到这些空数组中(例：<50的放到第1个空数组,>=50&&<110的放到第二个空数组...)各子数组使用其它排序算法或继续使用桶排序方法排好序，再按顺序将这些排好序的子数组拼接起来。
**基数排序**：步骤：求出待排数组的最大值确定其最大位数是个位,十位还是百位...；取出带排数组a中的每个数据根据其个位值放到对应的下标的一个空二维数组中去(因为个位相同的可能有多个值将其归为一组)，结束后再将该二维数组中的值依次取出按取出顺序放回原数组中，再按十位为对应下标从原数组中取出值放到二维数组中结束后再依次取出...
**归并排序**：将待排数组a划分为若干个子数组，比较1，2个子数组的值将其排好序，对比3，4个子数组的值将其排好序，对比1，2，3，4子数组的值排序(1,2,3,4已分别合并)，前一半的数组排好序后再排后一半子数组，最后合并排序。
https://www.cnblogs.com/onepixel/articles/7674659.html
#### 13、文档流和BFC：
文档流其实分为定位流、浮动流、普通流三种。而普通流其实就是指BFC中的FC。FC(Formatting Context)，直译过来是格式化上下文，它是页面中的一块渲染区域，有一套渲染规则，决定了其子元素如何布局，以及和其他元素之间的关系和作用。常见的FC有BFC、IFC，还有GFC和FFC。
BFC全称是Block Formatting Context，即块格式化上下文。它是CSS2.1规范定义的，关于CSS渲染定位的一个概念。视觉格式化模型定义了盒（Box）的生成，盒主要包括了块盒、行内盒、匿名盒（没有名字不能被选择器选中的盒）以及一些实验性的盒（未来可能添加到规范中）。盒的类型由display属性决定。
BFC的创建方法：根元素或其它包含它的元素；浮动 (元素的float不为none)；绝对定位元素 (元素的position为absolute或fixed)；行内块inline-blocks(元素的 display: inline-block)；
表格单元格(元素的display: table-cell，HTML表格单元格默认属性)；overflow的值不为visible的元素；弹性盒 flex boxes (元素的display: flex或inline-flex)；但其中，最常见的就是overflow:hidden、float:left/right、position:absolute。也就是说，每次看到这些属性的时候，就代表了该元已经创建了一个BFC了(是一个独立的布局环境，我们可以理解为一个箱子（实际上是看不见摸不着的），箱子里面物品的摆放是不受外界的影响的)。[参考学习地址1。](https://blog.csdn.net/qf2019/article/details/99828150)[参考学学习地址2。](https://www.cnblogs.com/magicg/p/12650563.html)

盒子模型：html的一个元素就是一个盒子，w3c盒子内容包括：marging、border、padding、content。ie的盒子模型中content部分包括border和padding部分。
#### 14、项目构建相关：
[别人收集的vue相关资源。](https://github.com/opendigg/awesome-github-vue#UI组件)
一、ui框架一览：
- 后台开发类框架可选择element-ui，MuseUI。飞冰(阿里-直接复制使用的ui组件库)。[Ant Design](https://pro.ant.design/index-cn)
- 金融移动端类ui框架可选择Mand-mobile。
- 较通用的移动端ui库：vux
- 可视化的：echars、plotly。
- [we-vue：适合微信公众号，小程序。](https://wevue.org/)
- [nutUI：适合电商网站的移动端ui库。](https://nutui.jd.com/#/index)
- 特效动画的：[Animate.css](https://animate.style/)。
- pc端（非管理）：[vue material，特效稍多](http://vuematerial.materializecss.cn/#/components/button)。[mue-ui，特效稍多](https://muse-ui.org/#/zh-CN/expansion-panel)
二、脚手架：vue-cli
三、js功能库：
- 处理时间的：moment。[moment文档官网。](http://momentjs.cn/)
- 处理数据：Lodash,[Lodash官方文档。](https://lodash.com/docs/4.17.15)。
- 富文本编辑：wangeditor

四、请求处理：axios
五、包管理工具：npm、[yarn](https://blog.csdn.net/moshowgame/article/details/103358313)。
六、检查代码规范的eslint（可编写规则，vscode使用设置eslint相应设置进行规范化）。
七、服务端渲染框架：与react结合的next.js，与vue结合的Nuxt.js。
#### 15、web端性能优化：
先列出一些方法：懒加载、字体图标、图片适当压缩、需要时才加载、vue中用keep-alive缓存加载过的组件、组件项用动态导入组件：Load:import('../component/test')。
图片处理专项：(png转为jpg后一般能缩小一半，但png色彩更丰富，且透明背景属性，所以项目中一般使用的是png)
jpg：全名是JPEG，是数码相机的常用格式，特点呢就是色彩还原性好，天生适合风景照，可以在照片不明显失真的情况，大幅度降低体积。
png：png是最适合网络的图片，色彩丰富，png 不适用于颜色很少，或亮度差异十分明显的较简单的图片。
<i class="label1">mask-image优化png图片加载</i>如果是不需要透明属性的png图片我们可以直接转为jpg，但如果有透明要求转为jpg后就会透明部分变成白色。
所以使用css的mask-image属性有一张纯色png图(轮廓与原png一样，纯色填充后是以前的1/100大小)遮在jpg图上(png转化后的)，这样使用jpg图片就能代替png了。
```css
img {// 不用担心兼容性问题。
    -webkit-mask-image: url(card-mask.png);
    mask-image: url(card-mask.png);
}
```
#### 16、文字继承单选框和复选框：
```html
<input type="radio" id="a"/> <label for="a">点我触发前面id为a的单选框</label>
<input type="checkbox" id="b"/> <label for="b">点我触发前面id为b的复选框</label>
{
    appearence:button;//设置单选框或复选框为正常状态。为none时无法使用
}
```
改变复选框状态：
`<input type="checkbox" checked='checked' value='1' id="ele"/>`
写上checked表示默认为选中这与value值无关，动态改变复选框或单选框状态需要用js控制：
```js
ele = document.getElementById("ele");
ele.checked = false;//false表示没选中，true改为选中。
ele.checked获取复选框状态返回true/false(布尔值，非字符串)。
```
#### 17、拖拽：
将一个元素拖拽到另一个元素。
```html
<div id="div1" ondrop="drop(event)" ondragover="allowDrop(event)"></div>
<div id="drag1" draggable="true" ondragstart="drag(event)">可拖拽对象</div>
<script>
//    拖拽结束触发。
    function allowDrop(ev) {
            ev.preventDefault();
        }

        function drag(ev) {
        //拖拽该元素时，设置一个键值对，第二个参数用于选中该元素。
            ev.dataTransfer.setData("Text", ev.target.id);
        }

    function drop(ev) {
    // 拖入到该元素上，松开鼠标触发，通过键获取元素id，
       ev.preventDefault();
       var data = ev.dataTransfer.getData("Text");
       ev.target.appendChild(document.getElementById(data));
    }
</script>
```
### 二、CSS
:::alert-info
简介：css(Cascading Style Sheets)层叠样式表，1996-12-17css1诞生，2003年1月svg被定为w3c规范，但当时的网页只是图文内容，css更受偏爱。
:::
#### 1、基本概念：
- **流**：俗称文档流，指的是css中的基本的定位和布局机制，css中的布局规则。所以从上而下从左至右的描述只是css的一个默认流而已。
- **选择器**：css中id的等级强于class强于标签名，只要带有id名的选择器（id选择器或是带有id名的兄弟选择器）语句块中定义的样式就是浏览器会显示的，他会覆盖类选择的器、标签选择器（前提：两个不同的选择器作用在一个元素上时；如果是两个相同类型选择器作用在同一个元素上以后一个选择器为主(为主指的是在相同的属性定义上)。
- **自适应布局**：对凡是具有自适应布局的一类统称，流体布局是自适应布局的一部分，但**流体布局**狭窄的多，<b class="violet">如div+css就是流布局，而table布局则不属于流布局，因为css真正是从css2.1开始的，IE8开始支持它，在这之前table就已经存在，所以ie8前的浏览器多数使用table布局。</b>
- **css3**：移动端的掀起崔氏css3的产生，css3中新添了很多丰富网页的属性，如3d、变换、渐变、圆角、弹性布局、栅格布局、动画等。但并未影响，更新之前2.1的流属性。
- **未定义行为**：相同的css代码在不同浏览器可能效果不一样，甚至不显示，这并非bug。因为各浏览器厂商去实现css时有一些自己的理解和定义，导致一些特殊情况未在其规则内导致的差异，繁杂多变的情况总有遗漏。<b class="gray">如伪类::activity元素上同时绑定事件，事件中使用`event.preventDefault()`#这样能使拖动之类的效果更流畅，但火狐上不会显示active定义的行为。</b>

box-sizing:content-box;//定义的width不包含border宽度，即总宽度= padding值+border值+width值（margin值不算元素宽度）但如果是背景图片依然会占据	padding部分（不会占据border部分），文本内容不会占据padding部分；Box-sizing:border-box;//定义的width包含padding值和border值即：总宽度=width；背景图片占据padding部分。（伪类元素定义出来的是content-	box模型，即使通配符中已经定义了box-sizing:boder-box）。
box-sizing:border-box的前提下子元素相对于父元素定位是根据父元素的content的宽高来定位（border值，padding值不算）。
将一个元素定义为行内块时其会产生默认的外边距，即使在通配符中已经定义了margin为0px。
元素定位为relative时只能在样式中定义其宽度,其高度只等于它的子元素的高度加它的内边距加外边距之和(top，left等不算).
font-style:normal;去除`<em></em>`标签的斜体样式。
textarea禁止改变文本域大小：resize:none
自动换行：word-break：break-all或white—space：normal来实现自动换行。
引入外部文件中的资源地址不能用斜杠开头(一些浏览器不能识别)固定定位只相对于window窗口，无论该元素放到上面元素里。
[css中自带的字体。](https://www.cnblogs.com/fozero/p/6087513.html)
#### 2、鼠标样式：
el{
    cursor:pointer;//手指,提示可点击
    cursor:hand;//IE5使用的手指样式
    cursor:wait;//等待
    cursor:help;//帮助
    cursor:no-drop;//无法释放
    cursor:text;//文字，暗示为文字内容
    cursor:move;//提示可移动对象
    cursor:crosshair;//十字准心
    cursor:n-resize;//向上改变大小箭头
    cursor:s-resize;//向下改变大小箭头
    cursor:e-resize;//向右改变大小箭头
    cursor:w-resize;//向左改变大小箭头
    cursor:ne-resize;//向右上改变大小箭头
    cursor:nw-resize;//向左上改变大小箭头
    cursor:se-resize;//向右下改变大小箭头
    cursor:sw-resize;//向左下改变大小箭头
    cursor:not-allowed;//禁止
    cursor:progress;//处理中
    cursor:default;//提示可移动对象
    cursor:url();//引入外部文件作为鼠标样式，文件格式必须为.cur或.ani
}

边框样式：
el{
    border:1px dotted red;//dotted:点线
    border:1px dashed red;//dashed:虚线
    border:1px solid red;//solid:实线
    border:1px double red;//double:双边框
    border:1px groove red;//groove:3d凹槽
    border:1px ridge red;//ridge:菱形边框
    border:1px insert red;//insert:3d凹边
    border:1px outset red;//outset:3d凸边
}
textarea标签resize属性的的各个取值:
none：用户不能操纵机制调节元素的尺寸；
both：用户可以调节元素的宽度和高度；
horizontal：用户可以调节元素的宽度；
vertical：让用户可以调节元素的高度；
inherit：默认继承。
#### 3、超出隐藏：
多行超出省略
overflow: hidden;
text-overflow: ellipsis;
display: -webkit-box;
-webkit-line-clamp: 2; //设置行数
-webkit-box-orient: vertical;

overflow:hidden;text-overflow:ellipsis;white-space:nowrap;//3个属性一起设置可以让超出的文本变为省略号。
ele{
position:relative;
min-height:150px;   //子元素撑起的高度在150-360之间时可以自适应
max-height:360px;  
overflow-x:hidden;  
overflow-y:auto; //设置为auto时在元素高小于360时不会出现滚动条，超过360时才会显示
}
媒体查询器：@media only screen and (min-width: 300px) and (max-width: 768px) {}
#### 4、不常用：
scroll-behavier:smooth;//发生滚动时更平滑(锚点跳转、改变scrollTop值)
text-decoration:line-through;设置删除线。
text-indent:35px;//首行缩进两字符
letter-spacing:5px；//调整字间距

border-collapse:collapse;//将table元素中的表格间距取消。
让同一个父元素中的子元素两端对齐的方法:子元素之间添加空格或换行后使用	
text-align：justify;和text-align-last:justify;(一起使用)。最好将要对其
子元素设置为inline-block元素。

**背景图片设置**：
```
background:url(" ") no-repeat;
background-position:50% 0; //图片居中
background-size:cover; //占满
```
css所有选择器：http://www.w3school.com.cn/cssref/css_selectors.asp
(css选择器、js中的querySelect选择器、jquery封装的选择器中属性选择器
[dat~=src],[dat|=src]中要求这个属性中的值是以空格分割开的).
display：none将元素归为无(不占位置但其中内容任会解析)。
#### 5、尺寸单位：
- **em**：是根据当前元素字体大小而变化的,列入当前元素font-size:14px;width:10em,此时width为140px(每1em为字体大小)。
- **rem**：是继承根部元素(html)的字体大小的,例:html{font-size:16px;}.div{width:10rem;}//width为160px。用以下代码修改根元素大小。
```js
(function(win, doc) {
    var W = win.innerWidth;
    var UIW = 750;
    var RATIO = 100; // 1rem = 100px

    if (W < 1000) {
         doc.documentElement.style.fontSize = W / (UIW / RATIO) + "px";
    }
})(window, document)
```
- **vw**：视窗宽度,1vm相对于视窗宽度的1%。
- **vh**：视窗高度。
- vmin和vmax：vw和vh中选择最小/最大那个。
#### 6、引入外部文件夹中的字体：
[字体图标的使用]若是使用阿里图标库的话,头部link引入资源,元素中写上类名
iconfont,元素内容中写上对应的unicode编码。下载到本地使用的话引入下载的
iconfont.css和iconfont.js(那些eot,svg,ttf...文件也要放到项目中)
```
@font-face{
    font-family:sAir;// 自定义的字体名字
    src:url(../font/okj.otf);//一般是otf文件
}
div{font-family:"sAir";}//使用字体
```
#### 7、css3：
css3中的skew就是将元素迎着坐标轴拉伸，拉伸的角度就是元素对角线变化的度	
数。例：skewX（20deg）就是元素做对角线逆时针旋转20度，但元素高度不变。
background-size：需要做兼容
transition：all 1s linear;//需要对单个属性设置过度时(transition:background 1s,height 2s;)
transform,box-shadow,background-position,background-img；
做3Dhover效果时，加上perspection属性会更有真实效果。
在transform-origing 属性中添加第三个值即z轴方向坐标可以更改坐标原点位置
(2D，3D变换中均有效）。
3D转换中规定从上往下看逆时针方向是绕Y轴旋转的正方向；从左往右看逆时针方向	
是绕X轴选装的正方向；Z轴的正半轴一直是在图片正面的那边。从上往下看，顺时针
方向是 绕z轴旋转的正方向。
2D、3D变换中坐标轴中心点位于图片中心，x始终轴垂直于图上、下边，y轴始终垂直	
于图左右边，z轴始终垂直于图片,（坐标轴随着图片做同样的变换）。
css3中的变换操作作用于行内元素上无效。
css3倒影：
```css
el{
    box-reflect:below 1px linear-gradient();//box-reflect属性为元素添加倒影
    //效果，第一个值设置方向，第二个值为倒影与元素的距离，第三个值为线性渐变，将
    //渐变设为透明度逐渐增加的白色效果较好，做兼容处理时box-reflect前和渐变前
    //都加上前缀。
}

```
css3剪切：
```css
el{
    clip-path:polygon(50% 0,10px 100px,150px 100px);//多边形剪切，点位置
    clip-path:circle(50% at 50% 50%);//圆形剪切,半径，圆心坐标
    clip-path: ellipse(30% 20% at 50% 50%);// 椭圆剪切，宽，高，圆心位置
    clip-path:react();//矩形剪切，写入位置，宽高。
}

css3实现毛玻璃效果(高斯模糊)：
el{
    -webkit-filter:blur(10px);
    -moz-filter:blur(10px);
    -ms-filter:blur(10px);
    filter:blur(10px);
}
```
css3贝塞尔速度曲线：
```css
el{
    /*默认的贝塞尔速度曲线是从(0,0)到(1,1)的一条匀速直线，括号中的四个数值是
    //贝塞尔曲线中的两个点的位置，通过这两个点拉扯曲线，速度安装曲线弯曲度改变。
    transition:all 1s cubic-bezier(0.7,0.1,0.9,1);
}

```
user-select为css3属性，需要做兼容。
perspective-orign:50% 50%;//改变视角位置坐标
#### 8、一个让全局提示的写法：
```css
#tip{
      position: absolute;
      z-index: 100;
      top: 40%;
      left: 50%;
      width: 300px;
      margin-left: -150px;
      text-align: center;
      padding-top: 1px;
      >p{
        display: inline-block;
        position: relative;
        padding: 8px 20px;
        color: white;
        background: rgba(0,1,2,.6);
        border-radius: 8px;
        font-size: 14px;
        text-align: center;
      }
    }
```
#### 9、弹性布局：
```css
.box{
    display:flex;
    display:-webkit-flex;
    flex-direction:row;//排列方向
    flex-wrap:wrap;//转行类型
    justify-content:space-between;//对其方式
    align-items:center;//元素垂直居中,控制的是另一个轴
}
.child{
    // 其子元素对应align-item方向上的位置控制.
    align-self:flex-end;
    flex-bais:500px;    //控制单个元素所占宽度，代替width。
    flex-grow:2;    //设置该子元素所占比，主轴上。如果其余部分固定尺寸，则>=1时撑开剩下空间。
}
```
**一排固定几个元素**：使用justify-content:space-between且给子元素宽度时，这时宽度不起用，需要加上：flex-direction: row;flex-wrap: wrap;这样每行就能像想象的个数显示。

### 三、javascript
JavaScript由3部分组成：
ECMAScript：解释器。翻译兼容性：完全兼容
DOM：Document Object Model （文本对象）兼容性：部分不兼容。
BOM：Browser Object Model （浏览器对象）兼容性：不兼容（例如IE，谷歌，火狐，不可能兼容），核心是window，全局对象。
dom针对的是标准的客户端控件，html标记的这些浏览器展现的内容
bom针对的是浏览器，BOM是浏览器对象模型，DOM是文档对象模型，前者是对浏览器本身进行操作，而后者是对浏览器（可看成容器）内的内容进行操作。
#### 1、js数据类型操作：
javascript数据类型包括：数值、字符串、布尔、null(表示尚未存在的对象)、undefined(当声明的变量还未被初始化时，变量的默认值为undefined。)、对象(对象又包括列表、函数、字典)，6种。#alert(null == undefined); //output "true"  。ert(null === undefined); //output "false" 
<i class="label1">数值</i>
`parseInt("fjdk889")`//转为整型889,剔除字符串。`parseFloat()`//转为float型。`num.toFixed(2)`;//保留小数位数。
8进制，十六进制数也可直接写入：`var v = 070`#八进制的56。`var c = 0XA`#16进制的10。
**含e的数**：一般表示极大极小值`var m = 3.125e7`#等价于`3.125 * 10^7`。`var c = 3e - 7`#0.00....03。
**NaN**：用于表示一个本应该是数值，返回却是非数值的情况，如数值比上0，NaN与其它数值操作同为NaN，`NaN == NaN返回false`。用isNaN()可检测。
**转为字符串**：num.toString();
**浮点数计算精度丢失问题**：`console.log(24314310.3412 / 100000)>>243.14310341200002`。所有编程语言都存在的问题，这是由于计算机本身特性导致的。小数位数过长，或有时计算中小数点参与移动。所以前端尽量不要使用浮点数的计算。**解决思路**：将小数转为整数，按特别方法计算后再移动小数点。
数值与字符串的运算：`1 + "1" == "1" + "1" = '11'`#除了+是字符串连接，其它运算操作符情况会被先当做数值计算。
<i class="label1">字符串操作</i>
其它类型转为string：`String(val)`#无论val是什么类型都会转为对应的字符串。
`x.toString()`//转为字符串。`x.replace(/target/g,'')`//替换,g表示所有满足的都替换。`x.concat(“a”,”b”)`//可与x连接多个字符串。
`x.charAt(index)`//查找字符串的对应下标的值,`“justice”.charAt(1)=”u”`。
`"a".toUpperCase()`方法将小写字母转换为大写,`"A".toLowerCase()`#将大写字母转为小写。
`str.substring(start,end)`//提取字符串中介于两个下标间的字符串，一个参数时为start，截取后面所有。在源数据上操作。
`str.substr(start,length)`#第二个参数为选择从start起截取多少个长度字符。
`str.indexOf('aa')`#查找字符串位置。
`str.search('abc')`#找到子串开始位置。
```js
var str = '大米:2.57斤/元,白菜:3.65元/斤';
var arr = str.match(/\d+(.\d+)?/g); //match()方法找到所有匹配的项，返回一个数组。
```
<i class="label2">js的正则表达式</i>
```js
//i表示不区分大小写，g表示匹配全局，m表示可匹配多行。
var a = /e/i;
var b = new RegExp('e');
console.log(a.test('aaebc'));// 返回布尔值
console.log(a.exec('kke,mme'));//只能找到第一个匹配项，放回一个列表形式的记录（有匹配到的值）。
```
<i class="label1">列表</i>
- `list.indexOf(1)`//找到第一个1在列表中的位置，不在则返回-1。
- `list.incloud(1)`//是否包含1，返回布尔值。
- `list.join("-"`)//将各元素用字符链接。
- `list.push(1)`//在列表最后添加值。
- `list.pop()`//删除最后一个元素。
- `unshift()`//在数组最前端添加一个新的值。
- `arr.sort()`#不传参数的话，默认将arr中的值看成字符串来排序。

```js
var arr = [1,8,2,4,3,9,0];
//sort()实现的排序的思想，传入函数作为参数，以灵活的用于各种情况。
arr.sort(function(a,b){
    //火狐使用归并排序，google使用快速+插入。b在a之前，循环用a与b比较。
    if (a > b) {
        return 1;//1表示不变。
      } else if (a < b) {
        return -1;//表示a,b交换位置。
      } else {
        return 0;
      }
})
```
- `list.reverse()`//将数组倒置，[1,2,3].reverse();//[3,2,1]。
- `list.shift()`//移除第一个元素。
- `instanceof`//检查一个对象是否为了一个对象中的实例，Console.log(p1 instanceof p2);//p1是否为p2中的实例；
- 注意：按引用类型操作的值，其后面操作改变了值，但前面值打印出来和改变后是一样的。

**数组去重**：
```js
function unique (arr) {
  return Array.from(new Set(arr));//使用集和。
}
unique([1,1,'true','true',true,true])
```
<i class="label2">splice(位置,操作,值)</i>//splice()方法可以操作数组
```js
var arr = [1,2,3,4,5,6];
arr.splice(2)//删除2及之后的值。
arr.splice(0,2);//表示删除0,1位置的值，第二个参数表示删除的个数。
//插入、第三个参数表示在当前索引后插入的数。
arr.splice(1,0,7)//[1,7,2,3,4,5,6] ！！
arr.splice(1,1,7)//[1,7,3,4,5,6]

```
- **列表，字典均属于Object类型**，即：`[1,2] instanceof Object`#为true，但`{a:1,b:2} instanceof Array`#为false。

<i class="label2">映射操作</i>
map();//将数组中的每个元素调出来都执行一遍回调函数;`[10,20,5,8,99,4].map(ne);`//ne为函数，列表的每个值会被当作ne的参数一一传入。
forEach()//forEach()方法调用数组的每一个数传递给回调函数。
例：`arr.forEach(function(value,index,data){});`//对数组做循环遍历获取数组各项值当做参数传入到函数中便于函数用其做操作。对象不能使用。ie 1.9以 下不支持;
**undefined**：派生自null，因此`null==undefined`#返回true，使用全等符号才会返回false。已声明，未赋值的变量依然是undefined。但是没有声明的值使用，会直接报错。然而使用`typeof no(未声明值)`#得到的也是undefined类型，所以undefined不属于Object。
**数据类型检测**：`console.log(typeof val)`#有string、number、undefined、boolean、function、object（字典和null都显示这个）。
**null**：表示一个空对象指针，因此用typeof检测时返回object（但`null instanceof Object`返回false）。如果该变量之后用于赋值一个对象，那初始赋值可以置为null。
**布尔值**：`0，空字符串、null、undefined、false`都是当做false。
**隐式转换**：在进行变量比较时，js内部会对数据进行相应变换如下：（全等条件下回进行类型的比较，所以这些在**全等下不成立**）
- [] == true;  //false  []转换为字符串'',然后转换为数字0,true转换为数字1，所以为false
- [1,2,3] == '1,2,3' // true  [1,2,3]转化为'1,2,3'，然后和'1,2,3'， so结果为true;
- [1] == 1;  // true  `对象先转换为字符串再转换为数字，二者再比较 [1] => '1' => 1 所以结果为true
- '1' == true; // true。

#### 2、转码：
```js
encodeURIComponent("<svg>")#不会对 ASCII 字母和数字,标点字特殊符等进行编码
encodeURI('汉字');//url传参汉字时可以先encodeURI()对中文编码,浏览器会自动解码
decodeURI();// 再用decodeURI()转码，对汉字解码则不变。

escape()与unescape()://将url地址作为参数传参时可用
document.write(escape("Visit W3School!"))// Visit%20W3School%21
// escape()方法对输入内容进行编码转为机械码能让所有机型识别
document.write(unescape("?!=()#%&"))// %3F%21%3D%28%29%23%25%26
//unescape()方法对机械码进行转码，转为可识别码
btoa()和atob():
var str = "javascript";
console.log(window.btoa(str))//amF2YXNjcmlwdA==
console.log(atob("amF2YXNjcmlwdA=="))// 'javascript'
```
#### 3、H5 WebSocket:
WebSocket是一种在单个TCP连接上进行全双工通讯的协议，它允许服务端主动向客户端推送数据，浏览器和服务器只用完成一次握手两者之间即可创建持久性的连接，并进行双向数据传输。需要先安装pywebsocket支持websocket服务
```js
if(window.WebSocket){
    // 继承webscoket类，传入url,可选子协议
    var ws = new WebSocket("htt://url",[protocol]);
    ws.onopen = function(){// 连接建立时触发
        ws.send(data);//发送数据
    }
    ws.onmessage = function(res){alert(res);}// 接受到数据时触发
    ws.onclose = function(){//关闭时触发函数}
}
else{alert("连接错误")}
```
#### 4、H5 web Workers:
workers是让一个js文件在后台执行不影响页面执行速度的一种技术,对一些需要处理大型的数据是一个不错的优化选择，且主流浏览器都支持(除了IE）
// 一个js文件,a.js
```js
var i = 0;//postMessage()方法将传入其中的值返回给调用它的worker
function start(){postMessage(i);i += 1;setTimeout(start,1000);}
// 另一个js文件中
(function(){
    if(typeof(window.Worker)!='undefined'){
        // 浏览器支持Worker
        var w = new Worker('js/a.js');
        //res为postMessage()返回的对象，res.data获取其中数据
        w.onmessage = function(res){console.log(res.data);}
        w.terminate();//终止worker
    }
})()
```
#### 5、js一键复制功能:
```html
<button onclick="get()">点击复制</button>
<script>
    function get(){
        var int = document.createElement("input");
        int.value = "这是复制内容";
        document.body.appendChild(int);//添加到DOM中才能选择(使用select())
        int.select();//选择input中的内容
        document.execCommand("Copy");// 执行复制语句
        int.style.display = "none";// 复制完后才能隐藏
    }
</script>
```
#### 6、三元运算符：
三元运算符与if语句同样的作用，例：
      if(x>10 && x<50){alert("hello");}
      替为 x>10 && x<50?alert("hello"):alert("flase")。(两者等价
      问号前为判断条件，问号后为执行语句，冒号后为else时的语句)。
三元运算符用于赋值：val = val>20 ? 20 : 10;//表示如果val大于20val值就为20，否则为10；
三元运算符中写多条语句：a == 20 ? (a=15,alert(a)) : (a = 21,alert(a));

#### 7、原生js元素操作：
<i class="label1">获取元素位置、大小</i>
el.offsetHeight;//包括边框+内边距+内容尺寸
el.clientHeight;//内边距+内容尺寸
el.clientTop;//上边框
el.offsetTop;//距父元素左边距含margin值
el.scrollTop//元素当前内部滚动的距离
el.scrollHeight//元素内部可滚动的距离
在使用ele.offsetLeft获取元素在发生变换过程中的对应值时需要用
ele.style.left="";来重新写入该元素的位置，否则返回的永远都只是
该元素的初始位置，使用ele.getBoundingRect().left可实时获取元素位置。
<i class="label1">js元素节点</i>
p = document.createElement("p");//创建一个节点
document.createTextNode("text");//创建文本节点
el.appendChild(p);//添加孩子节点：末尾添加
<i class="blue">在添加完节点后可以用`p.setAttribute("style","width:10px;height:20px")`方法来动态改变该元素属性，直接用style则无效。</i>
fa.insertBefore(el,fa.lastChild);//插入节点：fa中插入节点el,在最后一个节点前插入。
el.parentNode;//父节点,选中el的父节点。
el.previousSibling;//选取上一个节点
el.nextSibling;//选取下一个节点
a.contains(b)/a.compareDocumentPosition(b)//判断一个元素是否包含另一个元素
el.removeChild(ak);删除元素节点//只能用父元素删除子元素的方式
el.cloneNode();复制元素//复制的元素会复制其所有属性,但并不会复制其文本内
容和html结构。
el.childNodes;//返回元素的所有子元素(两种不同情况返回的长度)
```html
<p><b>1</b><b>2</b><b>3</b></p>//p.childNodes.length>>3
<p>
<b>1</b>
<b>2</b>
</p>//p.childNodes.length>>4
```
el.childNodes[0].nodeName;//节点名,为间隙或文字则为#text为元素则为
大写的标签名,nodeValue;//节点中的文本内容(非html结构)
#### 8、网页中js调用摄像头：
```html
<video id="but" onclick="get()">调用摄像头</video>
<canvas id="canvas"></canvas>
<div onclick="show()"></div>
<script>
var width = window.innerWidth;
var height = window.innerHeight;
// 点击调用摄像头
function get() {
    var but = document.getElementById("but");
    // obj传到getUserMedia()方法中
    var obj = {
         // 设置视图大小，允许录制音频
                    video: {
                        width: width,
                        height: height
                    },
                    audio: true
                }
                // 兼容性处理
            let photo = navigator.mediaDevices.getUserMedia(obj) ||
                navigator.webkitGetUserMedia(obj) ||
                navigator.mozGetUserMedia(obj) ||
                navigator.msGetUserMedia(obj);
            // 会先获取权限(用户控制)，调用成功的话则运行then()方法
            photo.then(function(MediaStream) {
                but.srcObject = MediaStream; //图像显示到but元素中
                but.play(); // 显示
            });
            // 调用失败则运行catch()方法
            photo.catch(function() {
                alert("调用摄像头失败")
            });
        }
        // 点击拍照
        function show() {
            var canvas = document.getElementById("canvas");
            var ctx = canvas.getContext("2d");
            // 上面获取到的but是RGB数组对象。
            ctx.drawImage(but, 0, 0, width, height);
        }
</script>
```
https://www.zcfy.cc/article/choosing-cameras-in-javascript-with-the-mediadevices-api
https://blog.csdn.net/jvid_sky/article/details/53213898
#### 9、js获取改变内嵌样式、外联样式：
原生js中使用ele.style.property的方法只能获取内嵌样式中的style属性或在js		语句中写入的属性,使用:
window.getComputedStyle('元素','伪类').getPropertyValue('属		性')的方法可以获取元素的css中所写的样式,但这两个方法都是只读属性，不能用	来改变其中的css样式(getComputedStyle()方法中不能像选择器一样选中元素，而是要通过专门的元素选择器选好之后传进去)。
js写入内嵌样式的方式还可以是：ele.style["color"] = "red";可以使用这两种方法来改变其元素的css样式(但是会显示在内嵌样式中)：
(1)ele.style.cssText=”width:150px;height:200px;”;//重写其css样式表
(2)ele.style.setProperty(‘样式名’,’样式值’);//setProperty()方法设置属性是在style中的并不是一个直接的属性。
**原生js为元素添加类名或id名**：setATTribute(“class”,“new”)，element.className=””;setATTribute(“id”,”id”),element.id=””;
(原理其实是替换)。使用removeATTribute(“class”.”id”)（也可用来移除id名）或.classList.remove(“id”)来移除元素类名。
#### 10、选择本地图库中的图片显示并压缩：
input中的file属性提供了一个从本地图库选择图片文件的功能,以下代码将选中的图
片显示在页面上：
```html
<img id="img"/>
<input type="file" onchange="get(this)" multiple="multiple"/>
<!--multiple允许一次选择多张图片-->
<canvas id="can" width="500" height="300"></canvas>
<form id="form"></form>
```
```js
function get(self){
    // self是input元素
    var img = document.getElementById("img");
    var ctx = document.getElementById("can").getContext("2d");
    var cImg,w,h;
    //self.files.length;获取图片张数
    var fil = self.files[0];
    var read = new FileReader();
    read.readAsDataURL(fil);
    read.onload = function(){
        img.src=read.result;
        cImg = new Image();
        cImg.src = read.result;
 // 可直接将read.result直接传给后台
        cImg.onload = function(){
            // 获取原始图片大小
            w = cImg.width;
            h = cImg.height;
   //可以根据w,h的比列缩小画在canvas上再获取相应区域的像素数据传送
            ctx.drawImage(cImg,0,0);//不填入宽高值时是原始打下显示。
        }
    }
}
```
// 图片的上传建议放到form表单中再使用FormDat用原生ajax上传,上传的键名是
```js
// form表单中input的name
var form = document.getElementById("form");
var form_ = new FormDat(form);
//设置值，添加值，获取form表单中的值，但不建议这样来改变表单中的值而是建议直接
//将值写到表单里对应的元素的value值中来上传
form_.set('name',value),form_.append('name',vlaue),form_.get('name')
```
#### 11、js生成与扫描二维码：
需要下载qrcode.js库引入页面，然后:
var qrcode = new QRCode(ele,{width:80,height:80});//继承QRCode类，传入的第一个参数为选中的元素，第二个参数为对象设置该元素的大小。
`qrcode.makeCode("htto://www.xiazai.com");//makeCode()`方法传入放置的内容可以
是文字、下载地址...
https://www.jb51.net/article/148921.htm
https://blog.csdn.net/jamkier/article/details/43149411
https://blog.csdn.net/No_red/article/details/80093421
https://blog.csdn.net/xuewufeifang/article/details/49756099
#### 12、时间：
var dat = new Date();
dat.getFullYear();// 获取年份
dat.getMonth() + 1;// 获取月份,从0开始所以需要加1
dat.getDate();// 获取号数
dat.getHours();// 获取小时
dat.getTime();//获取从1970/01/01至今过去的毫秒数。
dat.toUTCString();// 将日期转换为字符串
dat.getDay();// 获取星期
var dt1 = new Date();
var dt2 = new Date(dt1);// 将dt1当参数传入
dt2.setDate(dt1.getDate()+5);//将今天的号数设置为5天之后的号数
#### 13、引入页面中刷新父页面更改浏览器url：
在`<iframe><embed><object>`标签中若是有用到跳转页面使用window.location.href或window.open()或a标签中的跳转，页面跳转后还是只是显示在\<iframe>...这些标签之中，但使用window.parent.frames.location.href = ""能让上一个页面跳转或直接window.parent.location.href,window.top.location.href让最外层的页面跳转，a标签中的跳转可用target="parent"和target="top"来实现。获取前一页url：document.referrer;//包括传参也会获取到

#### 14、js判断图片加载完毕:
凡带加载性质的元素均有onreadyStateChange事件，不过不同浏览器的支持不同，一
些浏览器可能会失效。
img.onload事件(最好用的判断加载的方法)：
```html
<img id="img" src="img/a.jpg"/><h2 id='h2'></h2>
<script>
    var img = document.getElementById("img");
    var image = new Image();
    image.src = 'https://www.baidu.com';
    if(image.width===0){//判断图片路径是否可用
        console.log('该图片不可用');
    }
    img.onload = function(){document.getElementById("img").innerHTML="ok";}
    img.onerror = funcion(){img.src='';}//图片不可用时触发
//readyStatechange事件(试过google，不支持)
img.onreadystatechange = function(){
    if(img.readyState=="complete"||img.readyState=="loaded"){
        document.getElementById("img").innerHTML="ok";
    }
}
</script>
```
https://www.cnblogs.com/snandy/p/3704938.html
#### 15、js的兼容性问题：
事件的兼容性处理：
```js
el.onclick = function(event){
    //ie中可直接用window.event/event读取事件，firfox中通过传参传入事件
    var eve = event||window.event;
}

```
**元素选择**：
document.idName/document.getElementById("");//IE
document.getElementById();//其它,统一使用此法
el.parentElement/el.parentNode;//IE,统一使用parentNode

**元素中写入内容**：
el.innerText = "";//多数支持
el.textContent="";//低版本的firefox使用，建议全部用innerHTML代替。
ajax兼容问题：
```js
if(window.XMLHttpRequest){
    var xml = new XMLHttpRequest();//IE7以上支持
}
else{
    var xml = new ActiveXObject("Microsoft.XMLHTTP");
}
contains与compareDocumentPosition
ela.contains(elb);//elb是否在ela中，是则返回true,IE
ela.compareDocumentPosition(elb);//是则返回20，否为10,低版本的firefox
```
https://www.jb51.net/article/81704.htm
https://www.jb51.net/article/84596.htm
#### 16、原生ajax及上传文件使用:
<i class="label1">原生ajax的写法</i>
```js
var xhr = new XMLHttpRequest();
//username和password为url所需要的授权提供认证资格一般不填
xhr.open('post','url',true，username,password);
//该函数会执行3次分别是readyState为2,3,4触发
xhr.setRequestHeader(name,vlaue);//设置请求头,放在open()之后send()之前
xhr.onreadystatechange = function(){
// 开始上传后触发,readyState是本地上传的一个状态，status是服务器返回的一个状态
    if(xhr.readyState==4 && xhr.status==200){
        var res = xhr.responseText;
       res = eval("("+ res +")");
    }
}
xhr.send(obj);//发送数据,必须使用

https://www.cnblogs.com/ssj-777/p/5364070.html
ajax中添加头部请求：
$.ajax({
    beforeSend:function(xres){
        xres.setRequestHead('token',"eyJhbGciOiJIUzUxMiJ9.eyJzdWIiOiIxOD")
    },
    //或
    headers:{'Access-Token':$.cookie('access_token')}
})
```
<i class="label2">两种数据类型</i>向服务端发送的数据有Form Data和Request Payload两种，这两种数据类型可以由请求头的Content-Type控制。
- Form Data类型：`Content-Type:"application/x-www-form-urlencoded"`#默认使用的类型，在浏览器/netWork/Headers/最下方可以看到。
- Request Payload：`Content-Type:"application/json"`#现在几乎使用这种数据类型，发送一个字典的话会默认将每个键值队拼在url后请求。使用JSON.stringify()将数据转为json在发送是常用的形式。

<i class="label1">使用原生ajax来上传文件</i>使用jquery封装的ajax和axios的ajax先用formdata封装文件再上传时发现浏览器的xhr/head项中没有显示FormData项数据，在请求头中修改Content-Type:'multipart/form-data'后发现head项出现FormData数据了，但是有报跨域问题，这可能跟axios源码中检测数据类型，做的特别处理有关。
```html
<form id='a'><input type="file" name="file"/></form>
<script>
var form = document.getElementById("file-form")
var _form = new FormData(form)
var xhr = new XMLHttpRequest();
xhr.open('post',_url,true)
// 不用设置请求头数据类型，反而直接成功。
xhr.send(_form)
xhr.onreadystatechange = ()=>{
    if(xhr.readyState==4 && xhr.status==200){
        var res = xhr.responseText;
        res = eval("("+ res +")")
          console.log(res)
         }
    }
</script>
```
[各种Content-Type对应的数据，但是试过，似乎不太有效。](https://www.jianshu.com/p/10cdbb35ac87)
<i class="label1">使用ajax注入分页</i>使用document.write(data)的方法要求分页里只有元素结构（没有meta,html,body等在主页中重复的标签）,可是这样仍会把主页<head></head>标签中的外链样式覆盖为无,我们可以再写一个分页专门用于装效head标签及其里面的外联样式（link,script等）;可是外联的js语句只执行一次就	无效了!!（弃）;若注入分页的js
代码用引入的方式则`<script async='async' src=''></script>`或在注入的ajax代码中将async改为false或ajax代码后加一个延时器延时绑定事件。(一些坑爹的后台框架会劫持所有ajax请求导致报错所以使用需谨慎,本地打开带有使用ajax的文件会产生跨域问题);
<i class="label2">ajax中地址为空情况</i>ajax中如果url地址为空在提交时会变成提交到当前页url路径。jquery的ajax中不填写dataType值时jquery会自动判断返回值的类型(所填写的data中的格式不能是json格式)。
<i class="label2">ajax中添加加载动画</i>使用jquery的Ajax是在beforeSend:function(){}中添加动画，在complete:function(){}中取消加载动画。在原生js的ajax中也可以自行在onreadystatechange = function(){}前后添加两个函数也可实现。但beforeSend函数只在第一次请求时触发,所以显示加载动画最好是在调用ajax之前,complete中隐藏加载动画可以加一个延时取消这样交互效果更好。
<i class="label1">ajax接口的处理</i>做项目中在使用到ajax或其它方式对接数据时对接的接口需要用"http://"+获取的本地域名+接口来充当请求数据的接口，这样更换域名后也不会出错。(也可直接写域名后的接口名，在运行时会被自动添加上当前域名)。

**ajax跨域问题**：https://www.cnblogs.com/lxwphp/p/8080188.html
https://blog.csdn.net/WRian_Ban/article/details/70257261
https://blog.csdn.net/xr510002594/article/details/81409426
https://blog.csdn.net/mooncom/article/details/52402836
https://blog.csdn.net/codingnoob/article/details/80879208
#### 17、拦截浏览器回退操作：
```js
// 拦截history模式的回退。
pushState()和popstate是H5的新属性。
history.pushState(null,null,document.URL);
// 添加popstate事件监听变化。
window.addEventListener('popstate',function(){
history.pushState(null,null,document.URL);
});
// 拦截hash模式的回退
function c(){var url = window.location.href;}//获取到的是变化后的地址。用正则表达式来监听是否是回退到了上一个页面。
window.onhashchange = c; //onhashchange可以今天hash模式的变化，触发函数c。
```
#### 18、js对象与json格式互转：
```js
var obj = {name:"wcs",id:21}
obj = JSON.stringify(obj);// {"name":"wcs","id":21}
var json = {"name":"mx","id":23}
// eval()方法和JSON.parse()方法都可将json转为js对象，推荐用后一种
json1 = eval("("+ josn +")");//{name:"mx",id:23}
json2 = JSON.parse(json);
```
若是使用动态的方法将js对象转为json格式的话对象中的数值型会变成字符串，需要先用parseint()方法处理后再转换。
强大的eval()方法：
```js
eval()方法可以将字符串转换为可执行的js语句，例：
eval('30>20?alert("ok"):alert("error")');//ok
eval("obj.a."+b+"["+ "'"+v+"'" +"]")//这种情况v两边加单引号。
var obj = {a:{c:1,n:2},b:[0,1,2]};
eval("obj.a.c")//1,eval("obj.a"+['c']])//1
```
#### 19、页面间传值的几种方法：
1、url传参。(域名或路径后将参数用?或#号分割,参数间用&分割)
2、cookie缓存。(格式建议与url传参写成一样的)
3、Storage缓存。(页面间调用storage中的值,将一个数组存入后会变为逗号分割)
4、window.open()+window.opener
```js
// 页面a：
var a = 55; // 页面a的对象
el.onclick=function(){window.open("b.html");}//打开一个新窗口
// 页面b:
console.log(window.opener.a);//window.opener会将前一个页面的所有对象封装为
//一个对象的形式，b页面可以使用，但对用户体验不好。

```
#### 20、判断各种环境
```js
var browser = {
    versions: function() {
        var u = navigator.userAgent,
            app = navigator.appVersion;
        return { //移动终端浏览器版本信息
            trident: u.indexOf('Trident') > -1, //IE内核
            presto: u.indexOf('Presto') > -1, //opera内核
            webKit: u.indexOf('AppleWebKit') > -1, //苹果、谷歌内核
            gecko: u.indexOf('Gecko') > -1 && u.indexOf('KHTML') === -1, //火狐内核
            mobile: !!u.match(/AppleWebKit.*Mobile.*/), //是否为移动终端
            ios: !!u.match(/\(i[^;]+;( U;)? CPU.+Mac OS X/), //ios终端
            android: u.indexOf('Android') > -1 || u.indexOf('Linux') > -1, //android终端或uc浏览器
            iPhone: u.indexOf('iPhone') > -1, //是否为iPhone或者QQHD浏览器
            iPad: u.indexOf('iPad') > -1, //是否iPad
            webApp: u.indexOf('Safari') === -1 //是否web应该程序，没有头部与底部
        };
    }(),
    language: (navigator.browserLanguage || navigator.language).toLowerCase()
};
console.info(browser);

if (browser.versions.mobile) { //判断是否是移动设备打开。browser代码在下面
    var ua = navigator.userAgent.toLowerCase(); //获取判断用的对象
    if (ua.match(/MicroMessenger/i) === "micromessenger") {
        //在微信中打开
    }
    if (ua.match(/WeiBo/i) === "weibo") {
        //在新浪微博客户端打开
    }
    if (ua.match(/QQ/i) === "qq") {
        //在QQ空间打开
    }
    if (browser.versions.ios) {
        //是否在IOS浏览器打开
    }
    if (browser.versions.android) {
        //是否在安卓浏览器打开
    }
} else {
    //否则就是PC浏览器打开
}
```
动画函数：
```js
function play(){
console.log(a);
window.requestAnimationFrame(play);
}
window.requestAnimationFrame(play);//开始第一帧
cancelAnimationFrame()//方法取消动画。
```

#### 22、jquery的使用：
ready()方法：下载好资源后浏览器先对html文件从上往下进行解析,当遇到css样式表时先解析形成CSSOM,然后DOM和cssom形成一颗渲染树进行渲染(先摆放元素位置大小再加样式)
如果遇到同步js文件(为设置async的script标签)会先解析js文件即:阻断对html的解析.所以推荐奖css样式文件放在头部,js文件放在html尾部。
将引入js文件的位置放在头部时若js文件中获取html中DOM元素就会失败,解决方法：
在`<script>标签中加上异步属性<script src='' async="async"></script>`；
js文件中使用DOMContentLoaded事件：
```
document.addEventListener('DOMContentLoaded',function(){
document.getElementById("ele").style.color="red";
});// ie6,7中使用onreadystatechange事件
```
但window.onload事件会在DOMContentLoaded事件之后加载。而jquery中的ready()方法等三种起手式中都封装了上面的事件，所以引用了jquery之后再在头部中引入其他包含操作DOM元素的js文件也不会报错。将js文件引入位置放在文档尾部</html>内，推荐这么使用。https://www.cnblogs.com/caizhenbo/p/6679478.html
https://developer.mozilla.org/zh-CN/docs/Web/Events/DOMContentLoaded
隐藏和显示：$("p").hide();$("p").show();
淡入淡出：$("#p").fadeIn(1000,callback);$("#p").fadeOut(1000,callback) //第一个参数是变化的时间，第二个参数是运行完成后的回调函数。
动画： $("div").animate({left:'250px'},2000,callback);//变换的属性、时间、运行完后的回调。
#### 23、es6语法大全
```js
let a = 10;//#######块级作用域let定义变量,只在定义的块或附近的块有用，如for循环中
let a = () => 1;
alert(a);// 报错 a已被清除。
const a = 20;//const定义常量，第一次赋值后不能被改变。但如果是用来定义一个对象的话是可以改变其值的。
/*#######箭头函数，this*/
let foo = () => 1;//建立一个名为foo的函数返回值1，传参数时就等号后就写括号，
// var f = (1,2) =>{};多个参数时的写法，单个参数可不写括号，箭头指向执行语句
()=>{};// 将无名函数作为一个参数时的写法
v => {this.a = 20};// 将一个有名函数作为参数传入时的写法。箭头函数中的this
//不是指向他的上一级而是指向它本身
/*---------------------面向对象---------------*/
class animal{// 父类
    construct(dat){this.x=20;}
    run(){alert('here run');}
    //不能直接animal.run()调取父类中的方法。
}
class dog extends animal{// 子类,extends继承父类
//construct中接收的参数是new时传来的参数。
    construct(i){super();this.x=23;}
    say(){alert('here say')}
}
var pig = new dog('av');dog.run();// here run
dog.say();// here say
/*construct为构造函数为该类私有方法被继承时无需调用直接运行，extends继承的
/*子类中需要先调用super()方法才能用this添加实例对象因为子类中没有this对象只能/*继承父类中的*/

//#------------------解构
var [a,b,c] = [1,2,3]//a=1,b=2,c=3;
var {a,b} = {a:1,b:2}//a=1,b=2;
for(var i of obj){console.log(i);}//for of方法与for in方法不同，for of是
//迭代对象，它循环中的of表示对象中的每一项。
// 模板字符串
var name = 'your name is' + f_name + l_name;
var name = 'your name is ${f_name} ${l_name}';// 变量写在${}中
//#######模块的使用
import {a,b} from 'pages/home'
import a from 'pages/home/index'
export default{
    a
}
//---------------- 对象属性简写：{name,age,pos}
//----------------------- 延展操作符：
var a = [1,2,3,4,5];
    function c(v){
        console.log(arguments);
    }
c(...a);// 将a中的每个元素拿出来放到c中。

//##-----------------promise
//常用情况：
function add(n) {
    return new Promise(function(resolve, reject) {
         if (n % 2 === 0) {
              resolve('ok nice');    //成功时使用resolve
         } else {
              reject(`error ${n}`); //失败使用reject，返回参数
         }
    })
}
add(3).then(res => {
   console.warn(res);    //res是resolve或reject中返回的。
}).catch(res => {
   console.info(res);
});

var waitSecond = new Promise(function(resolve, reject)
{
    setTimeout(resolve, 1000);
});
// 异步编程串行化。
waitSecond.then(function()
    {
      console.log("Hello"); // 1秒后输出"Hello"
      return waitSecond;
    })
    .then(function()
    {
        console.log("Hi"); // 2秒后输出"Hi"
    });
//#####******async的使用
//修饰一个函数，默认返回一个promise的resolve对象
async function av(){return 10;}
av.then(res=>{});
//####*****await的使用。一定要放在async内部，可修饰所有数据类型
async function funAsy() {
     const a = 1;
     // 等待promise的resolve的返回值，赋值给b。如果是reject的话则直接报错。
     const b = await new Promise((resolve, reject) => {
           setTimeout(function() {
               reject('time')
           }, 3000)
     })
     // 直接输出b的话得到：time
     console.log(b,a)//3s后才会输出。
     return b;
}
// 而将b返回使用的话则是一个promise对象。
funAsy().then(res => {console.log(res)});//3s后才会输出。
//！！！    async无法配合使用回调的函数使用，如下：
function a(arr){await c = new Promise...}
async a.call([1,2,3]); //不会报错，但并不会变成同步。所以forEach,map()方法中使用也是无效的。

//-----------------代理proxgy。与就的object方法集一样的作用，都用于监听对象的变化。
  let test = {
    name: "小红"
  };
  test = new Proxy(test, {
    get(target, key) {
      console.log('获取了getter属性');
      return target[key];
    }
  });
  console.log(test.name);
```
es6的兼容性问题：https://www.cnblogs.com/chris-oil/p/5931180.html。[ES6，7，8，9，10学习地址。](https://juejin.im/post/5ca2e1935188254416288eb2)

#### 24、Object方法集：
```js
Object.defineProperty与Object.defineProperties
var obj = {name:'wcs',age:21,hob:[1,2],at:{a:5,b:9}}
Object.defineProperty(obj,'name',{
    set:function(val){alert('你修改了值name'+val);},
    get:function(){alert('你获取了值name');}
});
Object.defineProperty(obj.hob,'0',{});// 监听改变对象中的数组值时
Object.defineProperty(obj.at,'a',{})

```
Object.defineProperty()方法可传有三个参数，第一个是要监听的对象，第二个是参数是该对象中已有的属性或未有的属性，第三个参数是对象的形式，里面可以写两个方法，set方法在改变目标对象中指定属性(第二个参数)时触发的函数，可传入一个参数表示被修改的值，get方法在目标对象指定属性值被获取时触发。set方法和get方法都是在对应的操作前就先触发的，比如：obj.name = 'jieke',是先触发set方法再运行obj.name='jieke'语句；第三个参数中也可以写访问器属性：
```js
Object.defineProperty(obj,'name',{
    configurable:true,//表示能否通过delete删除此属性,默认为true
    writable:true,//表示能否修改此属性值，默认true
    enumerable:false,//表示该属性能否被for in等方法枚举，默认true
    value:"wcs"//直接为该属性赋值
});
```
在第三个参数中写以上属性都不能与get,set一起使用。
```js
 Object.defineProperties(obj,{//defineProperties()方法同时设置多个值
     name:{
         value:'张三',
         configurable:false,
         writable:true,
         enumerable:true
     },
     age:{value:'李四'}
 });
 Object.getOwnPropertyDescriptor(obj,'name');//获取目标对象指定属性的描述
```
vuejs框架中的数据监听就是通过以上方法实现的。
https://www.cnblogs.com/xlys/p/8520676.html
https://www.cnblogs.com/canfoo/p/6891868.html
#### 25、异常：
```js
// try,catch()
try{
    aleet('fdd');//异常情况会触发catch()
}
catch(err){console.log(err.message);}
// 主动抛出异常
throw 'not a number';//控制台输出：Uncaught: not a number
```
try,catch用于预测一些自己觉得可能会因为语法错误、取值不存在或方法不存在等情况下使用(写在try后的{}中)，catch后可传一个参数值，err.message输出
错误提示(catch后的{}中写发生错误后运行的语句)。try模块中只要有一句语句被判有误就会立刻跳到catch模块中去执行。
#### 26、事件：
<i class="label1">事件流</i>事件流描述的是从页面中接收事件的顺序。事件发生时会在元素节点与根节点之间按照特定的顺序传播，路径所经过的所有节点都会收到该事件，这个传播过程即DOM事件流。事件传播的顺序对应浏览器的两种事件流模型：捕获型事件流和冒泡型事件流。
冒泡型事件流：事件的传播是从最特定的事件目标到最不特定的事件目标。即从DOM树的叶子到根。【推荐】
捕获型事件流：事件的传播是从最不特定的事件目标到最特定的事件目标。即从DOM树的根到叶子。（事件冒泡先发生）
<i class="label1">事件绑定</i>
```js
<p onclick="start()"></p>// 原生的事件绑定。
function start(){};
// js动态绑定事件
document.getElementById("myBtn").addEventListener("click", function(e){
    // 第一个参数是事件类型，第二个参数是一个函数，会为其传入一个参数为事件对象，可以用e.target
    document.getElementById("demo").innerHTML = "Hello World";
});
```
event.preventDefault():阻止默认行为；
event.stopPropagation():阻止冒泡；
<i class="label1">js事件冒泡与事件捕获</i>
![paopao](_v_images/20200424091838620_274839134.png =270x)
如上图所示，先发生事件捕获再发生事件冒泡，子元素绑定的事件会被层层传递，所以在点击其父元素时也会触发子元素绑定的事件。
在不同浏览器中，冒泡的程度不同：IE 6.0:div -> body -> html -> document。其他浏览器:div -> body -> html -> document -> window。
并不是所有的事件都能冒泡，以下事件不冒泡：blur、focus、load、unload。
解决办法：
```js
if(event && event.stopPropagation){ // w3c标准
event.stopPropagation();
}else{ // IE系列 IE 678
event.cancelBubble = true;
}
```
<i class="label1">事件委托/代理</i>与事件冒泡相反，我们想让用户点击一个块的每个子元素都触发一个事件，可以将该事件绑定再这些子元素的父元素上就可以不用每个子元素都去绑定了。
<i class="label1">获取鼠标事件目标的属性</i>
```js
  event.target.nodeName//获取事件触发的标签名
  event.target.className//获取事件触发的元素的类名
  event.target.id//获取事件所触发的元素的id名
  event.target.innerHTML//获取事件触发的元内容
e.currentTarget//指的是真正触发事件的那个元素;e.target：触发事件元素的父级元素。
```
**移动端手指事件**:
需要使用事件绑定函数：addEventListener()或on()；
touchstart:手指触摸屏幕;addEventListener('touchstart',function(){})
touchmove:手指在屏幕上移动
touchend:手指离开屏幕
```
event.touches[0].pageX,event.touches[0].pageY//手指坐标，touchend事件中不能用
event.changedTouches[0].pageX,event.changedTouches[0].pageY;//都可用支持多指触摸事件？？？
```
(手机上涉及到手指移动事件再用移动端手指事件，其余事件就使用pc端的吧)
并不能完美的控制元素滑动的位置(做滑动元素时还是多使用overflow:scroll属性做滑动，滑动结
束后改变scroll位置(若要平滑效果用动画的方法设置))。
添加手指事件的元素最好都添加颜色（即便是透明）遇到过这种情况。
参考地址：https://blog.csdn.net/qq_40238154/article/details/78724917。https://www.cnblogs.com/yangmengsheng/p/5973487.html
自定义事件：
```js
// 一个元素设置监听事件名可随意。
document.body.addEventListener('文章勿盗', (event) => {
    console.dir(event.detail);
});
// 为该自定义事件设置，要传参必须制定使用detail。
var k = new CustomEvent('文章勿盗', {
    detail: 55
});
// 触发该事件。
document.body.dispatchEvent(k);
```
ie14下没有detail值，兼容写入如下：
```js
(function () {
    if (typeof window.CustomEvent === 'function') {
        // 如果不是IE
        return false;
    }

    var CustomEvent = function (event, params) {
        params = params || {
            bubbles: false,
            cancelable: false,
            detail: undefined
        };
        var evt = document.createEvent('CustomEvent');
        evt.initCustomEvent(event, params.bubbles, params.cancelable, params.detail);
        return evt;
    };

    CustomEvent.prototype = window.Event.prototype;

    window.CustomEvent = CustomEvent;
})();
```
**onselectStart事件**：`<p onselectStart="return false">积分抵啊放假</p>`这里是禁止选中文字
#### 27、js原型：
**执行上下文，链式作用域**：
执行上下文有且只有三类，全局执行上下文，函数上下文，与eval上下文。在执行代码前，浏览器会先扫描代码生成执行的上下文，按照上下情况决定先执行的代码，如声明变量、数据类型计算，遇到函数的时候，因为函数内部是一个块的代码，这时候就是构建一个函数的执行上下文。<i class="green">函数在调用时，会被全局执行上下文决定其执行的顺序。而一系列函数相互调用的情况下就形成了一个链式作用域。这些上下文的执行是放到一个栈(后进先出)空间中进行的。</i>
**封装**：将一些js语句写到一个方法里面，只留下一些特定的借口供外部访问。
**继承**：每个函数中都有一个prototype属性，而这个prototype属性被称为函数 的原型，原型中的所有方法都是可以被外部继承的，而函数方法内（原型外 部）的对象是该函数的私有对象，不能被继承。继承的方法可以使用new 关 键字继承，继承的那个变量就变成了一个对象（是对象而不是函数），继承 之后我们可以使用el[‘name’]=’pro’的方法向其中添加新的属性名属 性值，在原型方法中也可以继承自己的父函数中的原型，这样就可以实现重 复循环的自调用了；也 可以使用call(),applay()方法来继承。
多态：传入不同的参数或者配合不同的函数使用可以得到不同的结果。
注:继承是一个类似复制的过程，原类中关于:类名.prototype.function()的含有原类名的语句都会被新的类所能使用，这似乎是一个指针指向该方法;将一个方法的变量名放到一个对象中当参数传到另一个函数中也可以使用这种方式调用：`info['func']();`
若用于继承的变量与原类放在同一级情况下需要将运行类中的语句写在原类后，但若是继承的变量比原类级别低(继承语句及执行类中方法的语句写在一个函数内)可以运行。

- 网页端js开发在相当一段时间bai，由于浏览器的js解释引擎性能并不高，而且网络带宽也比较小，因此绝大多数站点的代码规模并不大，主要针对页面duzhi一些简单交互逻辑，在此前提下，浏览器厂商以及工业界都没有强大的动力去实现面向对象版本的js。
- 考虑到到网页环境的特殊性，使用原型继承而不是类继承的方式，更节约bai存空间，而且解释器的实现更为简单。
```js
function a(){}
a.prototype = {b:function(){console.log('errror');}}
var c = new a();
c.b();//执行语句写在类a的后面
```
**this添加新属性与方法.原型添加属性：**
原型的方法中使用：this.val = 10;的方法添加属性及值被子类继承后是子类中独有的与另一个子类中继承的a在堆存储中不是同一个源。
但若是使用：a.prototype.val = 20;的方法项原型中添加属性那么这个属性将是父类私有的，这意味着在两个继承的子类中即使使用传参动态改变val值的方法前一个类赋予的val值会被后一个子类的val值所覆盖。在原型的方法中又涉及到事件添加或创建函数等操作则在这些新建函数中则无法用
this方法调用原型中的属性；一个解决方法如下：
```js
a.prototype = {
    sta:function(){
        this.el = document.getElementById("el");
        this.run(this.el);// 原型的方法中调用原型中的方法并将原型中的一个属性
        //当做参数传入。
    },
    run:function(el){
        function play(){
            el.style['background'] = "blue";//若不使用传参的方法则在play()中
            //需要使用a.prototype.el.style['background'] = "blue"
        }
    }
}
```
但这并不能解决在原型中设立全局私有变量的问题。
<i class="label1">原型链</i>由上面的分析可以看出任何一个对象(除null外)都会由原型这个属性，在使用时一般是一个函数，然后将其原型指向一个对象(类似一个字典)，此时这个对象就成了原型，函数成了构造函数，而在使用new func()时是将原型继承给一个新的对象，此时这个新的对象、构造函数、原型3者之间都有了关系。这就是一个原型链。
#### 28、函数的闭包：
在有些情况下我们需要一个函数外调用一个函数内的局部变量，我们要想办法实现它，方法如下：
```js
function a(){
    var nm = 1;
    function b(){
        alert(nm);
    }
    return b;
}
v = a();
v();// 1
/*当然如果，用到的时候往往不知是得到函数内部的值这么简单，而是还有其它复杂逻辑。*/
```
#### 29、监听页面刷新与离开：
- onunload：IE6，IE7，IE8 中 刷新页面、关闭浏览器之后、页面跳转之后都会执行；IE9 刷新页面 会执行，页面跳转、关闭浏览器不能执行；firefox(包括firefox3.6) 关闭标签之后、页面跳转之后、刷新页面之后能执行，但关闭浏览器不能执行；Safari 刷新页面、页面跳转之后会执行，但关闭浏览器不能执行；Opera、Chrome 任何情况都不执行。
- onbeforeunload：IE、Chrome、Safari 完美支持。Firefox 不支持文字提醒信息。**Opera 不支持**。
```js
// 刷新时调用。
window.onbeforeunload = function(event) {
    window.localStorage.removeItem('token');
    //event.returnValue = "我在这写点东西...";
    //return '提示信息';
};
```
#### 31、call()和apply()的使用：
apply和call的作用是回调，es6之前很多回调都是使用它们；**Function.apply(obj,args)方法能接收两个参数**obj：这个对象将代替Function类里this对象。args：这个是数组，它将作为参数传给Function（args-->arguments。call:和apply的意思一样,只不过是参数列表不一样。
```js
/*定义一个Person类*/ 
function Person(name,age) { 
     this.name=name; 
     this.age=age;
} 
 /*定义一个学生类*/ 
 function Student(name,age,grade) { 
    //Person.apply(this,arguments);//特点：this指代student对象，只接收2个参数，arguments为隐式类数组对象，用来接收传入的参数；
      Person.call(this,name,age);//特点：this指代student对象，可以接收任意多个参数
      this.grade=grade; 
 } 
 var student =new Student("zhangsan",22,"二年级");//方法Student()也是object的一个实例
 //测试，相当于是借用apply()或call()方法来实现一个简单的继承。
 alert("name:"+student.name+"\n"+"age:"+student.age+"\n"+"grade:"+student.grade);
```
//学生类里面我没有给name和age属性赋值啊,为什么又存在这两个属性的值呢,这个就是apply的神奇之处.
#### 32、js垃圾回收机制：
多数编程语言都带有垃圾回收机制。现在各大浏览器通常用采用的垃圾回收有两种方法：标记清除、引用计数。
减少JavaScript中的垃圾回收：
new关键字就意味着一次内存分配，例如 new Foo()。最好的处理方法是：在初始化的时候新建对象，然后在后续过程中尽量多的重用这些创建好的对象。
为了最大限度的实现对象的重用，应该像避使用new语句一样避免使用{}来新建对象。
使用delete x;手动删除一个变量。
#### 33、节流和防抖动：
所谓的节流就是指用户频繁操作同一个事件，但都是相同的请求，如重复提交表单中的数据，重复下拉刷新请求数据，这会频繁的消耗用户的流量但是无意义的，遇到这种情况做法：写一个定时器，规定时间内只允许操作一次。
而防抖动是指类似搜索框中要监听用户的输入实时获取将值传给后台获取相应的匹配项，但返回的候选项个数不一样会导致下拉展示条频繁变化抖动。解决：监听到用户输入后设定一个定义器，时间过后执行操作，如果期间接收到监听变化就取消前一个定是器，再重新创建一个，相当与只取最后一次操作，因为此时是最有效的操作。
这两种思想都类似，不过一个取第一次操作，一个取最后一次操作。[参考地址。](https://www.jianshu.com/p/11b206794dca)
#### 34、async validator的使用：
vue中也可作为插件使用，博客文章中的旧版本与新版本使用差异较大。
[validator官网git地址，里面有使用示例。](https://github.com/yiminghe/async-validator#start-of-content)
[表单验证async validator的使用。](https://www.cnblogs.com/zyxh630/archive/2013/02/21/2920489.html)
#### 35、formData的使用：
```js
const el = document.getElementById("form");
let fd = new FormData(el);    # 不传入元素时是一个空的表单。
formData.append("k1", "v2");
formData.delete("k1");
formData.has("k1"); // true
formData.set("k1", "1"); // 修改
formData.get("name"); // 获取key为name的第一个值
```
#### 36、console的使用：
console模块不只log()一个函数，全部如下：
- `console.log("%d年%d月%d日", 2017, 1, 8)`#打印，%是占位符。console.info()#信息。
- `console.warn()`#警告。
- `console.group("第一组信息");console.log("第一组第一条：我是张三");...console.groupEnd();`#作为一组展示出来。
- `console.error()`#打印错误。
- `console.dir()`可以显示一个对象所有的属性和方法。
- `console.dirxml()`用来显示网页的某个节点（node）所包含的html/xml代码。
- `console.assert(a===2)`用来判断一个表达式或变量是否为真。若为否会抛出异常。
- `console.table([[1,2,3],[4,5,6],[7,8,9]])`#打印表格
- console.time()和console.timeEnd()，用来显示代码的运行时间。
- `console.profile("性能分析器");...中间代码;console.profileEnd("性能分析器");`
### 四、库、框架、工具
#### 1、gitHub的使用：
**安装**： 进入gitHub官网先注册一个账号,进入菜鸟教程点击git本地命令工具下载链接下载。git Barsh安装成功后打开(是一个命令行工具),操作如下：
输入ssh-keygen -t rsa -C "1815161966@qq.com"回车会提示要在/c/Users/Administrator/.ssh/id_rsa生成秘钥，之后一直回车到生成为止,此时在该路径下找到id_rsa.pub文件用记事本打开复制里面的所有内容,再在gitHub官网用户设置中找到SSH和GPG项将复制内容粘到键文本域中(title随意),回到命令行工具输入SSH -T git@github.com若成功会有提示成功信息。
<i class="label2">把本地项目上传到github</i>在github上创建一个仓库(点击加号选择第一个New repository),复制第一项中的url地址,然后打开Git Bush进入一个想放项目的文件目录中使用cd进入(cd G:/web),使用语句：git clone https://github.com/master,之后会在该目录下生产一个与你的仓库名同名的一个文件夹,将代码文件复制到该文件夹中,然后命令进入该文件夹(cd GanMa)再输入git add .(把文件添加进来)再输入git commit -m"xiaoswuwei"读入完文件后输入git push -u origin master（传入到仓库中）.使用git clone +地址，也能下载别人仓库中的文件。http://www.runoob.com/w3cnote/git-guide.html

**合并冲突解决**：协商解决冲突的页面，然后git add /src/...将冲突的页面加入，git commit -m 'merge'提交即可。
**全局配置用户名和密码**：如果没使用sshKey或使用了但不生效，那么每次push时都要求输密码和用户名，使用全局配置，一次性搞定。
```js
//注意这里的用户名和密码是对应所在的平台，如马云、github、gitee
git config --global user.name "wcs-ai"
git config --global user.password "34342"
```
**手动添加.gitignore并使其生效**：git rm -r --cached . // 删除本地缓存，然后add,commit。
**.ignore文件格式**：
```js
# 此为注释 – 将被 Git 忽略
*.a # 忽略所有 .a 结尾的文件
!lib.a # 但 lib.a 除外
/TODO # 仅仅忽略项目根目录下的 TODO 文件，不包括 subdir/TODO
build/ # 忽略 build/ 目录下的所有文件
doc/*.txt # 会忽略 doc/notes.txt 但不包括 doc/server/arch.txt
```
**各种场景的令**：
git merge --abort //**合并过程中的撤销**合并
git reset --hard HEAD^ //**回退到前一个版本** ^^回退两个  ~100回退多个
git pull  //从远程更新代码到本地
git remote //查看远程信息
git remote -v //查看远程库信息
git push origin second //将本地分支推送到远程，远程也创建这个分支(远程未存在该分支的
情况，否则就是普通的提交信息)

- **新建分支**：git checkout -b main origin/main     //main是本地分支，第二个是指从哪条源拉取代码，不写的话默认是master。
- **分支跟踪**：git branch --set-upstream-to=origin/wcs //当前分支跟踪（提交时提交到该分支）远程分支wcs。
- 查看所有分支：git branch -a //，-r查看远程分支。
- 切换分支：git checkout master  
- 查看文件状态：git status
- 查看具体改动：git diff    (红色是改动前，绿色是改动后)
- 删除本地分支：git branch -D second
- **本地与远程分支关联情况**：git branch -vv
- git merge WCS    //合并WCS分支到当前分支，再git push origin master//更新，

合并情况若**合并发生冲突**的话会提示冲突的文件，找到该文件并处理标记了冲突的地方然后
git add filename 然后git commit -m 'merge'即可
git checkout -b origin/second //拉取second分支下的代码到本地

git branch -a //查看所有分支
git push origin --delete yc //删除远程分支
<i class="label3">.gitignore文件忽略设置(任何时候更改忽略文件都会有效)从主目录开始算路径。</i>
index.html //忽略文件
/dist/   //忽略整个dist文件夹
front/dist/  //忽略front文件夹下的整个dist文件夹
front/index.html  //忽略front文件夹下的Index.html文件
**非克隆项目关联到git仓库**：本地没有修改、连接等设置，步骤如下：
`giy init` #先将本地项目变为一个git仓库。
`git remote add origin https://xxxx.com`#关联远程仓库，
`git add .`>`git commit -m 'new'`>`git pull`#合并到本地。
此时会提示输入账号、密码，若输入错误，第二次可能不会再提示错误，而是直接报错(使用了第一次的缓存)。解决如下：
win10/控制面板/用户账户/凭据管理器/windows凭据。最下方找到git的缓存，删除。
<i class="label2">内网中使用git</i>
封闭的内网环境内无法访问到外部网络，这需要自己在内网内指定一个git服务，做远程仓库用于存放代码。这也是众多代码托管平台，但多数是基于git或svn的原因。
**git分支管理**：git官网给出的一个管理分支的规则，几乎多数开发者都会使用。策略如下：
- 将master作为正式发布的分支，开一个devl作为开发使用的分支，开发完成后合并到master，然后使用master发布。（因为此时devlopment也是最新的，使用dev发布也可）。
- 因为其它需要，dev上又可以延伸出其它3种功能的分支：预发布分支、缺陷分支、功能分支。
- 预发布分支：开发完后，预发布在公司内测试。一般命名为release-1.0之类，开发完后合并入dev。
- 缺陷分支：（预发布或正式发布后任有不过，对其进行修复的分支）。
- 功能分支：一个项目模块拿出来单独开发，开发完成后合并入dev。
- 功能、缺陷、预发布完成后合并入dev，dev合并入master。
[git分支管理学习地址。](http://www.ruanyifeng.com/blog/2012/07/git.html)
**项目资源搜索**：awesome 接想搜索的资源。
[merge时提示：refusing to merge unrelated histories解决](https://blog.csdn.net/lindexi_gd/article/details/52554159)
#### 2、mpvue:
支持 微信小程序、百度智能小程序，头条小程序 和 支付宝小程序。
教程地址：http://mpvue.com/mpvue/#_2
vue-cli安装：https://blog.csdn.net/u011320770/article/details/81281193
安装好vue-cli后用命令来初始一个项目,因为需要安装很多的配置文件和依赖，分为初始化创建一个小程序和初始化创建一个网站,两种命令不一样，如下：
小程序:vue init mpvue/mp-vue-quickstart wxObject    [安装期间会询问appid的一些信息...]web:vue init webpack web  [安装期间也会询问一些问题，但没有appid询问]
src文件中修改代码就能自动修改两个端代码？https://segmentfault.com/a/1190000015545555    https://www.v2ex.com/t/448121
[一套同时配置了H5和小程序的demo]https://gitee.com/shqjustin/mpvuedemo 【里面有相关博客】
<i class="label1">运行与打包命令</i>npm run dev,npm run devH5	npm run build,npm run buildH5
注意项：【这里写的是在上面demo中的注意项】
[样式]使用的布局样式要使用less语言(style标签中写上less),一些标签不支持转译如ul,li,h5...index.vue等项目页面中在template标签中必须用一个标签包含所有内容(template内只能有一个一级子元素);只能使用改变类名的办法控制元素,v-bind:style=‘obj’失效,使用v-bind:style="{ color:gre }",样式参数从data中获取；不要使用标签选择器,一些小程序中使用的标签也无法转译。选择器使用>时后面不能跟#
(小程序端不能编译),img标签设置mode属性‘widthFiex’(自适应高度),不然小程序端不能显示。[字体大小:小程序上的rem为屏幕宽度/20这与网站端不一样]https://blog.csdn.net/qq_31383345/article/details/52817807，
[img设置自加载高度:https://developers.weixin.qq.com/miniprogram/dev/component/image.html]
[less中文文档:所有css代码最后被放到一个css文件中，所以在布局是谨慎使用同名的东西最好指定其父级]https://www.html.cn/doc/less/features/#features-overview-feature-operations-
<i class="label1">小程序单位</i>
虽然mpvue可以开发小程序和H5但并不能一套代码多端运行，两者差异较大，无法做到很好的兼容。比如单位上web端需要使用px或rem，但打包为小程序后px会被转为rpx，或直接使用rpx，两者无法保证界面一样。
小程序默认是750rpx占满全屏宽度(1px=2rpx)，所以如果是750宽的设计稿直接将其量取的值加上rpx使用即可，设计稿不是这个尺寸的需要先进行换算：
设备 rpx换算px (屏幕宽度/750) px换算rpx (750/屏幕宽度)。
[公共方法配置]如一些本地存储、路由跳转需要在min.js和minH5.js中配置,分页中使用this调用.将一些公共配置文件放到main.js和mainH5.js中(css和js)。
[监听]有时编译错误时,监听代码的改变在编译会失效，重新npm run dev即可。
[新建页面]https://blog.csdn.net/weixin_39818813/article/details/80602637,每新建一个页面就要建一个文件夹里面包含index.vue,main.js文件(可直接复制其它页面的内容改改文件夹名字)再npm run dev即可将新建的文件生成到dist文件夹中。
[页面跳转]wx.navigateTo({url:'../pages/a/main'})//保留当前页不关闭跳到其它页可用navigateBack()
方法返回页面,wx.reLaunch({url:''})//关闭当前页再跳到其它页，不可返回。
<i class="label1">使用axios</i>
当前项目文件夹下：npm install axios #安装在node_modules文件夹下。
mainH5.js文件中直接导入：import axios from 'axios'
[axios使用简单教程。](https://www.cnblogs.com/zxk5211/p/web_21.html)
<i class="label1">更改标题</i>跳到一个新的页面的时候往往需要改变其顶部标题,在跳到的页面对应的min.js文件中加上
```js
export default{
    config:{
        backgroundTextStyle: 'light',
        navigationBarBackgroundColor: '#fff',//标题栏背景色
        navigationBarTitleText: '数独小游戏',
        navigationBarTextStyle: 'black'//字体颜色
    }
}
```
[获取元素信息]https://www.cnblogs.com/zjjDaily/p/9566234.html
[生命周期函数:created]每个页面中使用的created函数时在进入这个项目时就调用的(进入第一个页面就会执行所有页面中的created函数)。
[页面初始化函数mounted]希望在进入进入一个页面之后再调用的函数写在mounted函数中也可用onLoad()函数或onShow()函数等，函数与mounted函数为同一级。
https://www.cnblogs.com/imgss/p/9164924.html
<i class="label1">小程序页面返回不运行初始化函数问题</i>使用navigateBack()返回上一个页面后不会再运行前一个页面的初始化函数，可以在调用navigateBack()时运行前一个函数的初始化方法。
```js
var pages = getCurrentPages();//获取页面栈
var before_page = pages[pages.length-2];//获取倒数第二个页面
wx.navigateBack({
    success:function(){
        before_page.onLoad();//运行前一页面的onLoad()函数。
    }
});
```
[数据请求]使用fly,js做网络请求。https://www.cnblogs.com/fuzhengyi/p/9579804.html{注意：必须加上请求头,不然后台获取不到参数。[header: {'content-type': 'application/x-www-form-urlencoded'}]}.
[触屏时获取手指位置]绑定的函数中传入$event,event.touches[0].pageX;touchend事件触发中获取位置:event.mp.changedTouches[0].pageX获取。
[小程序中嵌套网页]https://www.jianshu.com/p/50657f9af5b4
[scroll-view的使用]元素绑定了scroll事件后在小程序端会变成scroll-view标签这时其内部所有子元素的css样式会失效，需要使用内嵌样式。scroll-view标签相关的事件函数也都用v-on:scrolltolower类似绑定。
**组件的使用：https**://blog.csdn.net/qq_35661041/article/details/81476606    https://www.cnblogs.com/yun1108/p/9755785.html
<i class="label1">子组件触发父组件事件</i>
```js
//子组件事件
operate(){
    this.$emit('chooes',value1,value2);
}
//父组件,@加触发的事件名对应子组件的'chooes'。chooes_event后不加括号
<choose :value='d.data' @chooes='chooes_event'></choose>
chooes_event(a,b){
    console.log(a,b);
}
```
https://www.jianshu.com/p/9bd7e1ffc13a
https://blog.csdn.net/qq_33408245/article/details/82430821
<i class="label1">强制刷新循环</i>在一些嵌套得比较深的数据结构中动态改变里面的值时会出现不能渲染到页面的问题，可使用this.$forceUpdate()方法刷新for循环的数据渲染。https://blog.csdn.net/weixin_33910385/article/details/91710105
[web页面配置title]在mainH5.js文件中添加如下代码:（router已在头部导入）
```js
router.beforeEach((to,name,next)=>{
    window.document.title = to.meta.title;
    next();
});
```
<i class="label1">小程序端转json为js对象</i>
```js
res_= res_.replace(/\ufeff/g,"");
if(typeof res_=='string'){
  res_ = JSON.parse(res_);
}
```
<i class="label1">小程序图片选择</i>
```js
wx.chooseImage({
  count:6,
  sizeType:['original','compressed'],
  success:function(res){
    d.files = res.tempFilePaths;
    vb = d.files.length<6-len ? d.files.length : 6 - len;
    for(var c=0;c<vb;c++){
      d.imgs.push(d.files[c]);
    }
  },
  fail:function(){
    self.small_hint('最多只能选择6张');
  }
});
```
<i class="label1">小程序端图片上传</i>
```js
for(var i=0;i<d.imgs.length;i++){//先循环把没张图片放到上传队列中
    wx.uploadFile({
        url:'',
        filePath:d.imgs[i],
        name:'file',
        formData:{//这里写其它要传的参数
            'token':d.token,
        },
        header:{
            "Content-Type": "multipart/form-data"//加上这个头部
        },
        success:function(res){
            var res;
            if(res.statusCode){res_ = res.data;}
            else{res_ = res;}
            //收到的是json转为js对象。
            res_= res_.replace(/\ufeff/g,"");
            if(typeof res_=='string'){
              res_ = JSON.parse(res_);
             }
        }
    });
}
```
<i class="label1">第三方UI组件库的使用</i>这里以iview组件库为例，npm install iview --save。安装的组件库、框架等都会出现在node_models文件夹下，也可以将其拿出放到其它文件夹下使用。两个端兼容使用还是象普通组件使用一样，各页面使用import .. from 导入再绑定到组件上，使用的css在App.vue和AppH5.vue
页面内的css中导入：@import '../../nodemodels/iview/dist/iview.css'
<i class="label1">小程序登录</i>先调用wx.login()获取用户code，然后让用户点击button授权按钮:
```
<!--小程序中的写法，绑定事件都有bind前缀-->
<button open-type="userinfo" bindgetuserinfo='getinfo'></button>
<!--mpvue中不加bind，编译后会自带,或@getuserinfo='getinfo'-->
<button open-type="userinfo" v-on:getuserinfo='getinfo'></button>
<!--获取用户电话号码,mpvue中：v-on:getphonenumber='phone'-->
<button open-type="getPhoneNumber" bindgetphonenumber="phone"></button>
```
https://www.jianshu.com/p/bccbffd582bd
[webpack manifest.js文件讲解]https://blog.csdn.net/lancewu0907/article/details/76513231/
16个优秀的vue相关的ui组件库：https://www.cnblogs.com/zdz8207/p/vue-ui-framework.html
【vuex的使用】https://blog.csdn.net/qq_33026699/article/details/83302890
<i class="label1">微信浏览器内非公众号网页使用微信支付</i>https://liaolongdong.com/2017/09/09/wxpay.html
https://pay.weixin.qq.com/wiki/doc/api/jsapi.php?chapter=7_3
<i class="label1">最外层页面渲染问题</i>路由页面或minH5.js内改变vue中注册的值无法渲染到最外层页面，可以：
```js
d = {show:'block'};//全局的d
Vue.mixin({
    data(){
        return{
            d:d
        }
    },
    method:{
        alter_show(){
            d.show = 'none';//改变全局d的值可以渲染到页面
        }
    }
});
```
\<div :style={display:d.show}>\</div>
https://www.cnblogs.com/yuyujuan/p/9846564.html
https://doc.vux.li/zh-CN/install/biolerplate.html
<i class="label1">打包后放服务器上webpack导致的错误</i>https://blog.csdn.net/sansan_7957/article/details/80241158
在webpack.baseH5.conf.js文件中module中加入noParse: [/ali-oss/]然后在webpack.prodH5.conf.js文件的new HtmlWebpackPlugin()下加入：
chunks:['manifest', 'vendor', 'app'],
chunksSortMode: 'auto'
<i class="label1">微信公众号开放文档</i>
https://developers.weixin.qq.com/doc/offiaccount/OA_Web_Apps/Wechat_webpage_authorization.html#0
https://segmentfault.com/q/1010000010881298/a-1020000010884089
https://www.jianshu.com/p/7302e2c7f4b7
#### 3、nodejs：
:::alert-info
**简介**：js只能运行在浏览器内，相比于其它python，java之类的编程语言可以运行在桌面环境，js弱了很多，而node提供了js可在系统运行的环境，内部加了一些内置api，提供文件io等功能。node.js的最大优点是处理并行访问，如果一个web应用程序同时会有很多访问连接，就能体现使用node.js的优势。另一个好处是，使用javascript作为服务器端脚本语言，可以消除答一些与浏览器端js脚本的冲突。甚至发挥javascript动态编程的特性，在服务器与浏览器之间建立直接的动态程序。而npm是其自带的一个包管理工具。
:::
**windows上安装**：官网下载node的zip包，解压后将路径添加到path路径即可。
**linux上安装**：官网上下载nodejs的linux压缩包，解压进入，将node_v...包拿出来放到相放的位置并重命名，然后建立软链接`ln -s /home/wcs/software/nodejs/bin/npm /usr/local/bin/ `(usr/local/bin下的命令是可直接访问到的，不然要加入环境变量才行)再`ln -s /root/hone/wcs/software/bin/node /usr/local/bin/`#然后node -v 安装成功。
**脚本语言**：又被称为扩建的语言，或者动态语言，是一种编程语言，用来控制软件应用程序，脚本通常以文本（如ASCII)保存，只在被调用时进行解释或编译。
<i class="blue">如果是windows系统的话，尽量使用管理员身份来运行cmd，然后进行npm操作。</i>
**配置淘宝安装源**：npm本身指定的安装源是外国的，`npm install -g cnpm --registry=https://registry.npm.taobao.org`#安装淘宝镜像,使用时直接cnpm install即可.
[参考学习地址.](https://www.cnblogs.com/onew/p/11330439.html)
<i class="label1">打包vue项目报错：javascript heap out of memory</i>node 打包vue项目提示该javascript运行导致内存溢出，这是node封装的v8引擎运行的javascript其限制了js能使用的内存，当打包的项目稍大一些的时候就会出现该错误，解决如下：
//在package.json文件加入：
```js
{
    ...
    "scripts":{
        ...
        "fix-memory-limit":"cross-env LIMIT-4096 increate-memory-limit"
    },
    "devDependencies":{
        ...
        "increase-memory-limit": "^1.0.6"
    }
}
```
删除node_module文件夹，重新npm install安装依赖，然后项目下：npm  run fix-memory-limit
//然后安装：`npm install -g increase-memory-limit`#接着进入项目目录执行：`increase-memory-limit`#结束后再试试运行项目。[参考学习地址(先尝试3，4)](https://www.jianshu.com/p/410e826506be)。
临时设置安装源：`npm config set registry https://registry.npm.taobao.org `。[npm安装包失败的问题(设置一下安装源，npm安装即可)。](https://blog.csdn.net/moxiong3212/article/details/79756553)
##### a、npm：
<i class="label1">npm指令</i>管理包的指令：
```cmd
npm install --save lodash  #--save表示生产环境的依赖，--save-dev表示开发环境的依赖。
npm cache clean -f    #清除缓存。
npm remove eslint    //移除包内的某个依赖。
```
**nvm**：[windows版nvm下载地址，下载nvm-setup.zip包](https://github.com/coreybutler/nvm-windows/releases)。安装后cmd使用nvm命令
`nvm install 8.16.0`#安装其它node版本。`nvm use 8.16.0`#切换node版本。`nvm uninstall 8.16.0`#卸载指定版本。
- **运行js文件**：node name.js
- **使用同级文件**：`const fl = require('./index')`。
- **使用同级目录下的文件**：`const fl = require('./config/multi')`
- __dirname：当前文件所在目录的绝对路径。
- __filename：当前文件的绝对路径
- process.argv#以一个列表的形式返回命令行所有参数，如：`node a.js -m cc`->`['node','a.js','-m','cc']`

<i class="label1">编写自己的npm包</i>可以自己按照npm包的规则来写一个包，然后发布到npm平台使用。步骤如下：
- [先到npm官网注册一个人账号。](https://www.npmjs.com/signup)
- 进入一个人文件夹，使用npm init，填写一些信息（会生成package.json文件），初始化一个npm包。其中**main指定入口文件**如：`./moment.js`。
- 安装依赖：如果自己的这个npm包需要其它依赖，直接该目录下npm i ... --save即可。
- 登录：npm login登录账号。
- 指定的入口js文件最后需要用：`module.exports = obj`//的形式导出一个模块。
- 发布：npm publish。撤销发布：npm unpublish

##### b、文件操作：
读写操作：
```js 
var fs = require('fs')
// 读取指定目录下的所有一级目录或文件。
fs.readdir(MODULE_PATH, function(err, files) {
    if (err) {
        console.error(err);
    } else {
        pages = files;
    }
})
/*几乎所有的这类放发都有Sync，为同步读取*/
var pages = fs.readdirSync(MODULE_PATH)

const option = {flag:'w',encoding:'utf-8',mode:'0666'}//flag指定使用的模式。
// 写
fs.writeFile('test.text','内容',option,function (err){
    if(err){console.log('写入错误'+err)}
    else{console.log('写入成功'+err)}
})
// 一般使用writeFileSync()完成文件复制操作。
// 读，readFileSync为同步读取。
fs.readFile('test.text',{flag:'r',encoding:'utf-8'},function(err,data){
    if(!err){console.log('文件数据'+data)}
})
```
##### c1、chalk的使用：
一个给字体添加样式的包，支持模板使用：
```js
const chalk = require('chalk')
//字体颜色、粗体、背景色。
console.log(chalk.red.bold.bgWhite('内容'))
//模板写法
console.info(chalk`{blue.bold 内容}`)
```
##### c2、输入，输出：
```js
//方法一
process.stdin.resume();
process.stdin.setEncoding('utf-8');    //设置字符集
process.stdout.write('请输入:'); //标准输出
process.stdin.on('data', function (data) {
    var str = data.slice(0, -2);    //slice选取字符。不使用也可
    process.stdin.emit('end');//输入结束，触发
    process.stdout.write('输入的:'+str);
});
process.stdin.on('end', function () {//    监听上面的end事件。
     process.stdin.pause();
});
// 方法二
const readline = require('readline');
const rl = readline.createInterface({
    input: process.stdin,
    output: process.stdout
});

rl.question('你认为 Node.js 中文网怎么样？', (answer) => {
    // 对答案进行处理
    console.log(`多谢你的反馈：${answer}`);
    rl.close();
});
rl.on('close', function() {
    process.exit()    //退出命令行。
})
```
#### 4、postman的使用：
(百度搜索下载postman安装)输入框左边选择请求方式，输入框中输入请求接口，下方Params项中输入要传的键值和value值，键值和value值的输入不需用单引号或双引号不然会出错,若报错可以在body项中选择form-data然后输入Params项中的键值和value值再点Send.
#### 5、vuejs：
[vuejs官网。](https://cn.vuejs.org/v2/guide/)
- sass的css样式中：`@import '../style/vv.sass'`#导入样式。
- less的css样式中：`@import url(../style/vv.less)`#导入样式。
##### a1、vuejs运行流程:
分文这几个阶段：初始化阶段(这个阶段主要是把普通对象转化为响应式对象)、编译阶段(编译阶段会把options.template编译成render函数，解析template中的数据，事件绑定等)、挂载阶段(这个阶段会执行render函数以获取vnode。然后模板引擎根据vnode去生成真实DOM)、监听阶段(挂载阶段之后，模板引擎已经渲染好网页，这时就进入了监听阶段。patch函数还会对比新旧vnode，并计算出更新DOM需要的操作。最后由框架更新到网页上)、注销阶段(注销过程会先触发beforeDestroy，然后注销掉watchers、child components、event listeners等，之后是destroyed钩子函数)。[具体介绍学习地址。](https://blog.csdn.net/weixin_34023863/article/details/87945630)
**vue生命周期**：生命周期函数运行顺序如下：[生命周期解释。](https://www.cnblogs.com/wzndkj/p/9612647.html)
- **beforeCreate**：new一个vue实例后，只有一些默认的生命周期钩子和默认事件，其他的东西都还没创建。<i class="gray">data和methods中的数据都还没有初始化。因此不能在此调用methods的方法和data的数据。</i>
- created：data 和 methods都已经被初始化好了。
- beforeMount：在内存中已经编译好了模板了，但是还没有挂载到页面中。
- mounted：Vue实例已经初始化完成了。进入运行阶段，页面渲染完成，可在此进行操作dom。
- beforeUpdate：页面中的显示的数据还是旧的，data中的数据是更新后的， 页面还没有和最新的数据保持同步。
- updated：页面显示的数据和data中的数据已经保持同步了，都是最新的。
- beforeDestory：进入到了销毁阶段，这个时候上所有的 data 和 methods ， 指令， 过滤器 ……都是处于可用状态。还没有真正被销毁。
- destroyed(组件已经被销毁)。
<i class="label1">使用vue-cli来初始化一个vue项目</i>
:::alert-info
**vue-cli**：是一个构建项目的工具，一个平台，也是一个npm包。它提供一套初始的项目模板，内部规定好哪些文件夹的功能。打包时使用的webpack，webpack的配置，vue-cli中也写了一些初始的配置，webpack做为项目的一个依赖而安装。其它安装的一些依赖都放在node_modules下，一些less-loader,file-loader的东西是在编译打包时运行的，其配置也作为webpack的plugin。这些工程化项目的过程中node只是作为一个让其独立运行的环境，当然这当中也使用node一些自带的功能。所以不使用vue-cli,自己定义一个目录，编写配置也是可以的，也由此有很多cli工具。**vue-cli中使用的服务时webpack的服务**。
:::

`npm install vue-cli -g`#全局安装vue-cli工具，安装后可以使用vue命令初始化项目。
<i class="label2">安装vue-cli后找不到vue命令问题</i>
- linux上：安装vue-cli后会在所的nodejs/bin下看到vue。(npm config list#可以查看这个文件的位置)。为这个vue建立一个软链接将其放到/usr/local/bin下，`sudo ln -s /home/wcs/software/nodejs/bin/vue /usr/local/bin/vue`
- windows上：将`C:\Users\wcs\AppData\Roaming\npm`#vue被下载到该文件，添加到环境变量即可。

<i class="label2">初始化</i>`vue init webpack test `#初始化一个名为test的项目，之后会询问一些设置上的问题，具体查看这个地址：[vue-cli初始化项目学习地址。](https://www.cnblogs.com/saint258/p/9621161.html)
<i class="label2">使用</i>进入项目文件夹npm install#会自动寻找文件夹内package.json文件，安装其中配置的依赖包，scripts项的键值就是可以运行的命令，如npm run dev。大致的目录结构：src/components下的.vue页面是各项目页面；src/router/index.js文件配置路游；与src文件夹平级的build,config,node_modules,static分别放置打包配置文件、运行配置文件、安装的组件、图片，字体等静态文件。
<i class="label3">页面跳转</i>this.$router.push("/home") //非关闭式的页面跳转。

<i class="label1">数据、事件、属性绑定</i>
```
<p v-html="info">//info可以是html代码
<input v-model="dat"/>//input专用绑定数据语法
<a v-bind:href="url v-on:click="get()"></a>//绑定属性，事件
```


##### a3、循环：
```vue
<li v-for="i in is">
<h5>{{ i }}</h5>
<div v-if="i == 0" v-html="a">这是i</div>
<div v-else-if="i == 1" v-html="b">这是else</div>
<div v-else v-html="c"></div>
</li>
// 常用情况
<p v-for="(val,idx) in phones" :key="idx">{{ val.text }}</p>
```
加了v-for属性的元素会根据目标对象循环当前元素,包括其内部的结构，若目标对象长度为0或不是数组，字典那么当前元素也会被清除(可在for循环中加if,else语句条件循环是否要插入的元素)使用vue封装的ajax：
要下载vue-resource.min.js，方法集中使用：
```
this.$http.get("url",dat).then(function(res){console.log(res.body);},
function(){alert('失败')}));

```
$http方法是已经被封装在method对象中的所以可以用this直接调用，第一个参数传入接口地址，第二个参数传入要传送的数据，取到的值被当做参数传入then()中then()中第二个函数参数是请求失败时调用的函数。但使用vue封装的ajax感觉很不容易将获取到的值赋值出去，所以推荐使用jquery的ajax和原生ajax。vue中的ajax返回的数据中封装了很多东西，有数据、头部、catch-control等的加密信息，使用res.body代表获取到的数据。可使用JSON.stringify(res)查看结构。
##### a4、方法集中改变数据集中变量：
```js
var v = new Vue({
    el:"#view",
    data:{name:"error"},
    method:{alter:function(){this.name = "vue"}},// 这里的this指向的是method
    //所以data中的数据已被逐一放置到method中
    component:{"template":'<h3>dkl</h3>'}
});
v.alter()//直接运行函数

```
调用方法集中的函数：
v.alter()直接调用，或原始中`<p v-on:click="alter()"></p>`，v-on绑定的事件是动态绑定的所以使用v-for循环出来也能使用。
##### a5、样式绑定：
```html
<div v-bind:class="{a:isa,b:isb}"></div><!--isa为true时将类名a绑定-->
<p v-bind:class="[a,b]"></p>// 绑定多个类名
<a v-bind:style="styObj"></a>//styObj是js中定义好的变量，内嵌样式
<b v-bind:style="{ width: w + 'px',color: col }">

```
##### a6、计算属性与监听属性：
与methods是一个函数集对象，不过computed中的函数可以直接放到模板中<b class="violet">computed一般用于页面渲染的数据，watch一般监听一个值改变影响较大情况。</b>：
```js
//<p>{{ name }}</p>// name对应cmputed中对应的函数名，会将函数返回值作为name值。也可以写成{{ name() }}
...
data:{
    b:22,
    vb:89
},
computed:{
    name:function(){
        a = this.b + 1;
        return a;// 这里的返回值a依赖于this.b，只有当this.b发生变化时才会重新运行该函数，
        //如果这里时一系列复杂庞大的数据操作，每次调用name时也能快速获取到值(所以这是一个缓存效果)。如果不希望缓存的话可以用methods中的方法。
    },
    age:{
        // 像上面的name函数在创建后，会被vue实例转化为一个对象，默认有一个get属性获取值。
        get:function(){return 35;},// getter该数据时触发。
        set:function(){// 可以以这样的方式来添加一个set操作。set该数据时触发。
            return this.b + 10;
        }
    }
},
watch:{// watch中的函数名对应data中想要监听的数据名。
    vb:function(newVal,oldVal){// 会传入两个参数。在vb这个数据变化时触发。
        this.b = 29;
    },
    a(){//a发生了变化},
    obj:{
        // 监听一个对象的变化，需要加deep属性。
        heandler(nw,old){
            //发生变化时触发
        },
        deep:true
    }
}
```
事件绑定中传入event参数：
```javascript
<p v-on:click="get($event)"></p>
function get(e){
    // 使用此法来获取当前元素
    e.target.style.color = "red";//若绑定事件的元素中有多个子元素请用
//currentTarget,因为可能点Z中的是子元素，触发事件的却是因为事件冒泡
}
```
##### a7、组件：
第三方的组件一般安装后可直接单个页面按需引入，对应的插件安装后也可以单页面直接引入使用。子组件使用的数据最好是在父组件mounted之前就生成。
```javascript
// 全局注册，写在main.js文件中
Vue.component("wcs",{
    template:'<h1>{{ info }}</h1>',
    props:['info'],
    data:{},
    props:[],
    methods:{}
});// 页面中直接<wcs></wcs>即
```
局部注册
```HTML
<!--av是子组件test中的props中定义的值，当是一个对象时可以直接v-bind。:av="nm"(mpvue中的简写)。
.async表示组件内修改值也改变组件外的值，两者同步。
-->
<test v-bind:av="nm" v-bind="post" :varray.async="datas"></test>
import test from '../component/test'
...
components:{test}
```
<i class="label2">prop验证</i>在父组件向子组件中的props传递值时，props的值可以预先写定一个类型数据来做验证，若传来的值不满足验证则会有warn提示。
```javascript
// 子组件中的props内容。
props:{
    age:Number,
    propB: [String, Number],// 多个可能的类型
    propC: {// 必填的字符串
      type: String,
      required: true
    },
    propD: {
      type: [Number,String],//接受多个类型的写法
      default: 100
    },
    propE: {// 带有默认值的对象
      type: Object,
      // 对象或数组默认值必须从一个工厂函数获取
      default: function () {
        return { message: 'hello' }
      }
    },
    propF: {    // 自定义验证函数
      validator: function (value) {
        // 这个值必须匹配下列字符串中的一个
        return ['success', 'warning', 'danger'].indexOf(value) !== -1
      }
    }
}
// 父组件内容
<test :age="age"></test>
data:{age:'fdsf'}//与子组件要求的数据类型不一致时会在控制台有warn提示。
```

<i class="label2">组件中使用插槽</i>有时候我们定义一个组件不能完全应付所有场景，比如一个底部弹出框，有的有选择项，有的是展示商品内容，如果靠传值来控制显示，会导致子组件内东西非常多。而分为多个组件来写，它们之间又有一些共用的东西，所以产生了插槽。
```vue
// 第一个子组件的内容
<template v-slot:head>// v-slot的值对应第三个子组件中slot的name属性。具名插槽可以缩写为#head
    <div>第一个子组件内容{{ name }}</div>
</template>
// 第二个子组件的内容
<template v-slot:[slotType]>// 只能用在template标签上。用[]时就是使用动态插槽名，改变slotType值可以改变要插入的插槽。
    <div>第二个子组件内容。</div>
</template>
// 第三个子组件的内容，设置了slot
<template>
    <div>
    <slot name="head"></slot>// 对应的v-slot值会放到对应的name值位置。
    <slot name="body"></slot>// 这种指明了插槽名的情况被叫做具名插槽。
    </div>
</template>
// 一个单页面中的内容
<template v-slot:head>
    <div>
        <hello> //这里的hello是子组件3
            <c1></c1> //这是子组件1，也可以这这个标签中写v-slot:head属性。
        </hello>
    </div>
</template>
```
<i class="label2">插槽作用域</i>用于子组件中的数据想提供给父组件任意展示。[学习地址。](https://blog.csdn.net/lzl980111/article/details/104783252/)
```vue
<!--子组件中-->
<template>
    <div><slot :data="dts"></slot></div><!--绑定一个数据上去-->
</template>
<script>
export default {
    name:"child",
    data(){return {dts:[1,2,3]};}
}
</script>

<!--父组件中-->
<template>
    <div>
    <child slot-scope="slot"><!--数据都在slot下-->
        <span>{{ slot.dts.join('-') }}</span>
    </child>
    </div>
</template>
```

<i class="label2">动态组件和异步组件</i>使用component标签和v-bind:is属性来切换组件。
```VUE
<keep-alive>// 外面套上keep-alive标签后，加载过的组件会被缓存下来，再切回去的时候不会重新渲染。
  <component v-bind:is="name"></component> //component是vue内部自带的已注册的标签名，修改name值(对应组件名称)来在这个位置切换组件。
</keep-alive>
data:{
    name:'test'
},
components:{
    test,
    vv:()=>import("../components/vv")// 这是一个异步组件，在使用到时才会导入，相当于一个延迟加载。
    cc:() => ({    //定义异步组件加载时的一些其它行为。
      // 需要加载的组件 (应该是一个 `Promise` 对象)
      component: import('./MyComponent.vue'),// 异步组件加载时使用的组件
      loading: LoadingComponent,// 加载时使用的组件
      error: ErrorComponent,// 失败时使用的组件。
      delay: 200,// 如果提供了超时时间且组件加载也超时了，
      // 则使用加载失败时使用的组件。默认值是：`Infinity`
      timeout: 3000 //超过该时间不再加载。毫秒
    })
}
```
<i class="label2">边界情况</i>官网中将以下子组件访问父组件，父组件访问子组件数据等称为边界情况。
<i class="label3">访问根实例</i>
```
// 在子组件中用$root访问根组件的data或computed中的数据。
a = this.$root.foo;
this.$root.foo = 5;// 修改数据。
```
<i class="label3">访问父组件实例</i>
```
// 与访问根实例，类似。
var map = this.$parent.map || this.$parent.$parent.map
```
<i class="label3">父组件访问子组件数据、事件等</i>
一个vue内置的一个元素选择器，`<p ref="aa"></p>` ref标记元素，this.$refs.aa选中元素，如果绑定的是一个组件还可以继续this.$refs.aa.get()调起组件内的方法。
<i class="label3">依赖注入</i>类似访问父组件实例的情况，不过依赖注入可以在后代组件中都访问到，而且不用暴露所有父组件实例。
```
// 父组件内容。
data:{},
provide: function () {
  return {
    getMap: this.getMap
  }
}
//子组件内容
props:{},
inject: ['getMap']
```
依赖注入还是有负面影响的。它将你应用程序中的组件与它们当前的组织方式耦合起来，使重构变得更加困难。同时所提供的属性是非响应式的。这是出于设计的考虑，因为使用它们来创建一个中心化规模化的数据跟使用 $root做这件事都是不够好的。
<i class="label3">自定义组件上使用v-model与sync修饰符</i>
```vue
<!--父组件-->
<pop v-model="stateContent" :cs.sync="[1,2,3]"/><!--sync修饰的数据其子组件内可以直接更改，且父组件也会跟着变化-->
<!--子组件-->
<template>
  <div class="pop">
    <div><input :value="state" v-on:input="alt($event)" placeholder="请输入"/></div>
  </div>
</template>
<script>
export default {
  props:{
    state:{default:""},
    cs:Array
  },
  model:{    // model中需要指定改变的props中的值和使用哪个事件改变。
    prop:'state',
    event:'change'
  },
  methods:{
    alt(e){
      let c = e.target.value;
      this.cs.push('h');
      this.$emit('change',c);    // 子组件中使用触发事件更改父组件的值，即props中的值。
    }
  }
}
</script>
```
<i class="label3">第三方组件库安装</i>多数组件库都支持全局注册和按需使用，两者方式稍有区别。
全局引入：较为简单，安装后直接入口文件引入，Vue.use()使用插件，然后倒入相关样式文件，各组件内直接按语法使用即可。
按需引入：如果支持babel中配置的可以在babel-loader的配置项中写入（入口js文件中也要导入样式文件）：
```js
{
"plugins": [
    ...
    ["import", {    // 一些组件库是使用babel-plugin-component。
      "libraryName": "muse-ui",    //对应node_modules下的包名
      "libraryDirectory": "lib",// 包名下，导入的资源的所在目录。
      "camel2DashComponentName": false
    }]
  ]
}
// 页面如下使用
import {Button} from "muse-ui";
...
components:{[Button.name]:Button}//然后按照文档语法使用即可。
```
主题配置：同样在入口文件按照其文档配置全局的主题色、元素尺寸即可。

<i class="label3">程序化的事件倾听器</i>具体用法暂未了解！
通过 $on(eventName, eventHandler) 侦听一个事件
通过 $once(eventName, eventHandler) 一次性侦听一个事件
通过 $off(eventName, eventHandler) 停止侦听一个事件
<i class="label3">通过 v-once 创建低开销的静态组件</i>在组件的`<template v-once>`中添加，加载过后里面的内容会被缓存起来。
<i class="label1">阻止事件冒泡</i>v-on:click.stop='get()'

##### a8、vuex的使用：
一个全局变量管理控件。[vuex使用学习地址。](https://segmentfault.com/a/1190000015782272)[vuex官网。](https://vuex.vuejs.org/zh/guide/)
安装：`npm install vuex --save`#然后在src文件夹下新建一个store文件夹，store内再建一个Index.js文件，文件内容如下：
```js
import Vue from 'vue';
import Vuex from 'vuex';
Vue.use(Vuex);

const state={   //要设置的全局访问的state对象
     showFooter: true,
     changableNum:0
     //要设置的初始属性值
   };
const getters = {   //实时监听state值的变化(最新状态)
    isShow(state) {  //承载变化的showFooter的值
       return state.showFooter
    },
    getChangedNum(){  //承载变化的changebleNum的值
       return state.changableNum
    }
};
const mutations = {
    show(state) {   //自定义改变state初始值的方法，这里面的参数除了state之外还可以再传额外的参数(变量或对象);
        state.showFooter = true;
    },
    hide(state) {  //同上
        state.showFooter = false;
    },
    newNum(state,sum){ //同上，这里面的参数除了state之外还传了需要增加的值sum
       state.changableNum+=sum;
    }
};
const actions = {//异步运行
    hideFooter(context) {  //自定义触发mutations里函数的方法，context与store 实例具有相同方法和属性
        context.commit('hide');
    },
    showFooter(context) {  //同上注释
        context.commit('show');
    },
    getNewNum(context,num){   //同上注释，num为要变化的形参
        context.commit('newNum',num)
     }
};
const store = new Vuex.Store({
       state,
       getters,
       mutations,
       actions
});
export default store;

// main.js文件中。
import store from './store'//引入store
 
new Vue({
  el: '#app',
  router,
  store,//使用store
  template: '<App/>',
  components: { App }
})
// 使用
this.store.state.changebleNum//可直接获取到值。
this.store.commit('newNum',6);//运行mutation中定义的函数。
this.$store.dispatch('hideFooter')//运行actions中定义的函数。
```
大多数的项目中，我们对于全局状态的管理并不仅仅一种情况的需求，有时有多方面的需求，比如写一个商城项目，你所用到的全局state可能是关于购物车这一块儿的也有可能是关于商品价格这一块儿的；像这样的情况我们就要考虑使用vuex中的 modules 模块化了。在store文件夹下面新建一个modules文件夹，然后在modules文件里面建立需要管理状态的js文件
```js
// main.js入口文件。使用时稍做改变。
import Vue from 'vue';
import Vuex from 'vuex';
// 这些单独的js文件导出的是字典，而不是vuex对象。export default {state,mutations,actions.getters}
import footerStatus from './modules/footerStatus'
import collection from './modules/collection'
// 需要在创建实例前use()
Vue.use(Vuex);

const store = new Vuex.Store({
    modules:{    //    放到模块中。
         footerStatus,
         collection
    }
})

new Vue({...,store})
// 页面中使用
<span class="joinStatus" @click="invokePushItems(item)"></span>
import {mapState,mapGetters,mapActions} from 'vuex'; //先要引入
computed:{
    //这里的...是超引用，ES6的语法，意思是state里有多少属性值我可以在这里放多少属性值
    ...mapState({
    // 一般不适应mapState来取值。
         isShow:state=>state.footerStatus.showFooter //注意这些与上面的区别就是state.footerStatus,
                                                      //里面定义的showFooter是指footerStatus.js里state的showFooter
      }),
      //你也可以用下面的mapGetters来获取isShow的值，貌似下面的更简洁
       ...mapGetters('footerStatus',{ //footerStatus指的是modules文件夹下的footerStatus.js模块
         isShow:'isShow' //第一个isShow是我自定义的只要对应template里v-if="isShow"就行，
                         //第二个isShow是对应的footerStatus.js里的getters里的isShow
      }),
      //使用this.store.dispatch()有时会牵扯的事件的触发及传值，那就会有下面的mapActions用法了
      ...mapActions('collection',[ //collection是指modules文件夹下的collection.js
          'invokePushItems'  //collection.js文件中的actions里的方法，在上面的@click中执行并传入实参
      ])
   }
```
##### a9、路由的使用：
在router文件夹下的index.js文件中为每个页面添加路由。路由还提供一些钩子函数供控制跳转页面使用：
单个路由里的钩子函数：
```js
{// 这是Index.js文件中配置路由时的一个页面。
    path:'/',
    name:'aa',
    component:'',
    keepAlive:true,//设置后页面跳转后可以有缓存，包括传入的参数。
    beforeEnter:(to,from,next)=>{    //钩子函数。准备进入路由时触发
        console.log(from,to);//from，to分别是当前页，要跳转的目标页，的信息。可以获取其中信息做一些限制。
        next(false);//传入false的话则不能跳转。
    },
    alias:'/b' //别名，跳转到该页时使用的路径名
}
```
组件路由：和上面的钩子函数类似，不过这个是写在每个页面的组件里的：
```js
export default {
    name:'ww',
    data:{},
    beforeRouteEnter:(to,from,next)=>{
        //这些参数和上面的一样。准备进入路由时触发
    },
    beforeRouteLeave:(to,from,next)=>{
        //准备离开路由组件时触发。
    }
}
```
全局路由钩子：在main.js页面添加。
```js
// main.js添加
router.beforeEach((to,from,next)=>{
    //每个页面跳转时都会调用。改变标题
    window.document.title = to.meta.title;
    next();
})
```
跳转路由时缓存页面，避免被再次渲染。
<i class="label1">router的两种模式：</i>hash模式背后的原理是onhashchange。因为hash发生变化的url都会被浏览器记录下来，从而你会发现浏览器的前进后退都可以用了，同时点击后退时，页面字体颜色也会发生变化。这样一来，尽管浏览器没有请求服务器，但是页面状态和url一一关联起来，后来人们给它起了一个霸气的名字叫前端路由，成为了单页应用标配。[学习地址。](https://www.cnblogs.com/imgss/p/7492333.html)
```js
 // history=>history.pushState 浏览器历史纪录添加记录。history.replaceState 修改浏览器历史纪录中当前纪录。history.popState 当history 发生变化时触发
 // 使用时将state去掉，如：this.$router.push(url)
```
**hash模式**：hash模式url中会带有#号，破坏url整体的美观性, history 需要服务端支持rewrite, 否则刷新会出现404现象。
```js
window.onhashchange = function(event){
    console.log(event.oldURL, event.newURL);
    let hash = location.hash.slice(1);
    document.body.style.color = hash;

}
```
**模式切换**：historm模式是配合服务端渲染使用的。
```js
export default new Router({
  mode:'history', // 默认是hash
  routes: [
    {
      path: '/',
      name: 'HelloWorld',
      component: HelloWorld,
      // 重定向也可以使用函数，做假跳转。！！！如果对应的重定向路径也是一级路由，那么会直接跳转该页。
      direct:'/child', //访问该页面时路径变为/index（得在children配置），但router-view显示的是component的。
      children:[{path:'/index',name:'index'}]
    }
  ]
})
```
**声明式路由**：页面使用`<router-link :to="{path:'/test',query:{}}"/>`跳转。
**编程式路由**：如下。
```js
this.$router.push('/home');
this.$router.push({name:'home',params:{uid:33}}); //得到：/home/33  #刷新页面后，33会消失。
this.$router.push({path:'/home/login',query:{uid:23}}); //得到：/home/login?uid=23#path存在时params不生效。
//---另一个页面获取参数：this.$route.params.uid，或对应的使用this.$route.query.uid。
//***页面栈中跳转路由：
this.$router.go(n); //n可正可负
this.$router.replace('/home');//与push用法一致，不过是替换当前页面。
this.#router.back(-1);
// *****返回上一个页面传参只能用一些特别的方法。

//------****动态路由，路由配置页面如下
{
    path:"/book/:id",// :id为占位。必须用name跳转，
    name:"book",
    component:()=>import('../book')
}
this.$router.push({name:"book",params:{id:110}}); //页面地址变为/book/110。注意这些页面使用的是同一个页面。
```
##### b1、混入：
混入 (mixin) 提供了一种非常灵活的方式，来分发 Vue 组件中的可复用功能。
```js
// 局部混入。mixin中的像建立一个vue实例时那样创建created,mounted等属性，这些会被合并到vue实例中，发生冲突时与组件中定义的为准。
var mixin = {
  created: function () {
    console.log('混入对象的钩子被调用')
  }
}

new Vue({
  mixins: [mixin],
  data:{},
})
// 全局混入
Vue.mixin({
  created: function () {
    var myOption = this.$options.myOption
    if (myOption) {
      console.log(myOption)
    }
  }
});
```
自定义选项合并策略：暂未学习！
##### b2、自定义指令：
有的情况下，你仍然需要对普通 DOM 元素进行底层操作，这时候就会用到自定义指令。
```js
<input v-focus />
// 注册一个全局自定义指令 `v-focus`
Vue.directive('focus', {
  // 当被绑定的元素插入到 DOM 中时……
  inserted: function (el) {
    // 聚焦元素
    el.focus()
  }
})
// 局部自定义指令
directives: {
  focus: {
    // 指令的定义
    inserted: function (el) {
      el.focus()
    }
  }
}
```
除了inserted，一个指令定义对象可以提供如下几个钩子函数 (均为可选)：
bind：只调用一次，指令第一次绑定到元素时调用。在这里可以进行一次性的初始化设置。
inserted：被绑定元素插入父节点时调用 (仅保证父节点存在，但不一定已被插入文档中)。
update：所在组件的 VNode 更新时调用，但是可能发生在其子 VNode 更新之前。指令的值可能发生了改变，也可能没有。但是你可以通过比较更新前后的值来忽略不必要的模板更新 (详细的钩子函数参数见下)。
componentUpdated：指令所在组件的 VNode 及其子 VNode 全部更新后调用。
unbind：只调用一次，指令与元素解绑时调用。
钩子函数参数，指令钩子函数会被传入以下参数：
el：指令所绑定的元素，可以用来直接操作 DOM。
binding：一个对象，包含以下属性：
name：指令名，不包括 v- 前缀。
value：指令的绑定值，例如：v-my-directive="1 + 1" 中，绑定值为 2。
oldValue：指令绑定的前一个值，仅在 update 和 componentUpdated 钩子中可用。无论值是否改变都可用。
expression：字符串形式的指令表达式。例如 v-my-directive="1 + 1" 中，表达式为 "1 + 1"。
arg：传给指令的参数，可选。例如 v-my-directive:foo 中，参数为 "foo"。
modifiers：一个包含修饰符的对象。例如：v-my-directive.foo.bar 中，修饰符对象为 { foo: true, bar: true }。
vnode：Vue 编译生成的虚拟节点。移步 VNode API 来了解更多详情。
oldVnode：上一个虚拟节点，仅在 update 和 componentUpdated 钩子中可用。
##### b3、渲染函数&jsx：
Vue 推荐在绝大多数情况下使用模板来创建你的 HTML。然而在一些场景中，你真的需要 JavaScript 的完全编程的能力。这时你可以用渲染函数，它比模板更接近编译器。
```js
Vue.component('anchored-heading', {
  render: function (createElement) {// render渲染函数，在生命周期函数中也是使用该函数来解析组建的。
    return createElement(
      'h1',   // 标签名称
      {//这个对象内部定义一些模板的事件、指令、插槽类的东西。
      // 与 `v-bind:class` 的 API 相同，// 接受一个字符串、对象或字符串和对象组成的数组
      'class': {foo: true,bar: false},
      // 与 `v-bind:style` 的 API 相同，// 接受一个字符串、对象，或对象组成的数组
      style: {color: 'red',fontSize: '14px'},
      // 普通的 HTML attribute
      attrs: {id: 'foo'},
      // 组件 prop
      props: {myProp: 'bar'},
      // DOM 属性
      domProps: {innerHTML: 'baz'},
      // 事件监听器在 `on` 属性内，// 但不再支持如 `v-on:keyup.enter` 这样的修饰器。// 需要在处理函数中手动检查 keyCode。
      on: { click: this.clickHandler},
      // 仅用于组件，用于监听原生事件，而不是组件内部使用/ `vm.$emit` 触发的事件。
      nativeOn: {click: this.nativeClickHandler},
      // 自定义指令。注意，你无法对 `binding` 中的 `oldValue`// 赋值，因为 Vue 已经自动为你进行了同步。
      directives: [{
      name: 'my-custom-directive',
      value: '2',
      expression: '1 + 1',
      arg: 'foo',
      modifiers: {bar: true}
        }],
      // 作用域插槽的格式为// { name: props => VNode | Array<VNode> }
      scopedSlots: {default: props => createElement('span', props.text)},
      // 如果组件是其它组件的子组件，需为插槽指定名称
      slot: 'name-of-slot',
      // 其它特殊顶层属性
      key: 'myKey',
      ref: 'myRef',
      // 如果你在渲染函数中给多个元素都应用了相同的 ref 名，// 那么 `$refs.myRef` 会变成一个数组。
      refInFor: true
      },
      [
        '先写一些文字',// 这是h1标签的一个文本节点。
        createElement('h1', '一则头条'),
        createElement(MyComponent, {// 相当于创建一个组件的子组件。
            props: {
                someProp: 'foobar'
            }
        })
      ])
  }
})
```
##### b4、插件：
vuejs的插件是与vue实例分开的，使用时与vue原型绑定在一起。
```js
vue.use(vuex)//使用use方法来导入插件。
// 单独开发插件步骤。
MyPlugin.install = function (Vue, options) {
  // 1. 添加全局方法或属性
  Vue.myGlobalMethod = function () {
    // 逻辑...
  }
  // 2. 添加全局资源
  Vue.directive('my-directive', {
    bind (el, binding, vnode, oldVnode) {
      // 逻辑...
    }
    ...
  })

  // 3. 注入组件选项
  Vue.mixin({
    created: function () {
      // 逻辑...
    }
    ...
  })
  // 4. 添加实例方法
  Vue.prototype.$myMethod = function (methodOptions) {
    // 逻辑...
  }
}
```
##### b5、过滤器：
允许你自定义过滤器，可被用于一些常见的文本格式化。过滤器可以用在两个地方：双花括号插值和 v-bind 表达式
```js
// 局部定义过滤器
filters: {
  capitalize: function (value) {    //把传入值变为想要的。
    if (!value) return ''
    value = value.toString()
    return value.charAt(0).toUpperCase() + value.slice(1)
  }
}
// 全局定义过滤器。
Vue.filter('capitalize', function (value) {
  if (!value) return ''
  value = value.toString()
  return value.charAt(0).toUpperCase() + value.slice(1)
})
<!--使用示例： 在双花括号中 -->
{{ message | capitalize }}
<!-- 在 `v-bind` 中 ，后面可以继续加过滤器：| capitalize-->
<div v-bind:id="rawId | formatId"></div>
```
##### b6、过渡，动画：
vuejs有提供元素在插入，移除时做动画封装，使用起来还算方便。
```js
//fade开头的类名控制动画。
.fade-enter-active, .fade-leave-active {
  transition: opacity .5s;
}
.fade-enter, .fade-leave-to /* .fade-leave-active below version 2.1.8 */ {
  opacity: 0;
}
<transition name="fade">    //transition是自带的已注册组件，说功能更贴切。
    <p v-show="show"></p>    //在show状态改变后，会触发过渡效果(name指定的类名的开头)
</transition>
// 列表的过渡，使用transition-group
<transition-group name="list" tag="p">
    <span v-for="item in items" v-bind:key="item" class="list-item">
      {{ item }}
    </span>
</transition-group>
```
在进入/离开的过渡中，会有 6 个 class 切换。
v-enter：定义进入过渡的开始状态。在元素被插入之前生效，在元素被插入之后的下一帧移除。
v-enter-active：定义进入过渡生效时的状态。在整个进入过渡的阶段中应用，在元素被插入之前生效，在过渡/动画完成之后移除。这个类可以被用来定义进入过渡的过程时间，延迟和曲线函数。
v-enter-to：2.1.8 版及以上定义进入过渡的结束状态。在元素被插入之后下一帧生效 (与此同时 v-enter 被移除)，在过渡/动画完成之后移除。
v-leave：定义离开过渡的开始状态。在离开过渡被触发时立刻生效，下一帧被移除。
v-leave-active：定义离开过渡生效时的状态。在整个离开过渡的阶段中应用，在离开过渡被触发时立刻生效，在过渡/动画完成之后移除。这个类可以被用来定义离开过渡的过程时间，延迟和曲线函数。
v-leave-to：2.1.8 版及以上定义离开过渡的结束状态。在离开过渡被触发之后下一帧生效 (与此同时 v-leave 被删除)，在过渡/动画完成之后移除。

##### b7、报错问题集：
npm run dev时报`Cannot found module 'xxx'`的问题：一般直接npm install xxx --save即可解决，这些包都是package.json文件中配置要下载的包，会被下载到node_modules文件夹下，如果显示安装成功但依然报类似错误的话可以尝试清空node_modules文件夹，然后npm install 重新下载所有包。

#### 6、资源收集：
webpack学习：https://blog.csdn.net/eeeecw/article/details/80453899
前端技术文档大全：https://developer.mozilla.org/zh-CN/docs/Web/API/MediaDevices/ondevicechange
直播功能：https://www.cnblogs.com/liuxin-673855200/p/9948100.html
移动端网页上调用手机app：https://www.jianshu.com/p/3d1e48b9ec7c
调用电话：https://www.cnblogs.com/lilin1995/p/5640684.html
`<marquee></marquee>`标签属性大全：https://blog.csdn.net/bright_101/article/details/52124278
张鑫旭空间：https://www.zhangxinxu.com/
支付宝H5开放文档：https://myjsapi.alipay.com/alipayjsapi/index.html#3__E5_BF_AB_E9_80_9F_E5_BC_80_E5_A7_8B
javascript所有事件集：http://www.w3school.com.cn/html5/html5_ref_eventattributes.asp
HTML标签大全：http://www.w3school.com.cn/tags/index.asp ；(还有很多不错的标签没用过)。[axure各破解版本下载地址。](https://www.axure.com.cn/78629/)
[很多实用前端工具。](https://www.zhihu.com/question/20241338?sort=created)
[plotly.js起始教程地址，里面有下载地址(dist文件夹下)。和源码文档。](https://www.kutu66.com//GitHub/article_132050)

#### 7、微信公众号开发注意项：
先用超级管理员账号登录微信公众号平台，开发>开发者工具>微信开发者工具>绑定开发者(将自己的微信号绑定为开发者账号)。
开发>接口权限>网页服务>网页授权>修改下把目标网站域名添加为公众号授权网页(先上传那个txt文件到服务器项目根目录)。
然后按照微信公众号开放文档步骤获取用户信息，注意：url地址处理使用encodeURIComponent(url)函数处理,这个url中不能加端口号，所以只能是刚才配置的授权网页域名。
[配置、获取openid、授权登录。](https://www.jianshu.com/p/b7e2100b56e4)
#### 8、【集成网易云信IM】
下载demo(下载后先npm i 安装必要插件)
在login.js文件中，先将对应的appkey换成自己的。然后在获取到登录界面输入的账号，密码后添加一个网络请求，向自己的服务器获取用户在本应用下(对应的appkey应用下)的im用户id和云信服务器反给后台的云信token,然后调用cookie.setCookie()按格式放入到cookie中。
每次更改调试需要先npm run dev打包再node server启动本地服务。
要放到服务器使用的话直接将打包后的dist文件夹、regist.html,login.html,index.html文件放到服务器即可，主入口是index.html文件，在自己的项目中直接访问该路径+路由，然后带上uid,yxtoken两个参数(在指定im页面获取参数调用setCookie()登录，不然会报错)。
https://www.jianshu.com/p/2a601fe11bf0
https://www.jianshu.com/p/d56de7ea9736
#### 9、真机调试：(使用谷歌浏览器)
**方法一**：同一局域网内，用手机直接访问node开启的web服务地址(ip地址使用电脑ipv4地址，而不是localhost)。
**方法二**：使用google浏览器。
pc端和手机端都下载google浏览器，手机上打开开发者选项并允许使用usb调试(可按链接中教程一样使用安装驱动也可以pc端下载手机助手),手机和pc用数据线连接,然后打开手机端chrome浏览器(确认连接,连接成功后手机助手会显示手机页面),在pc端google浏览器地址栏中输入chrome://inspect进入如下
![google_phone](_v_images/20200419110535134_1308380564.jpg)
若下面没有显示手机型号可以多等待一会试试，输入框中输入要打开的网页,如果是打开自己做的项目地址要写成pc地址加文件名(例:浏览器中带服务打开网页为
127.0.0.1:5500/self.html,需要输入192.168.1.12:5500/self.html)这里的192.168.1.12是你pc的ipv4地址。(注:虽然在手机浏览器上能看到效果但其实在pc端浏览器上运行的效果,并不是在手机端浏览器环境下运行出来的)。[参考地址1。](https://www.cnblogs.com/meakchen/p/5665887.html)[参考地址2。](https://www.cnblogs.com/imwtr/archive/2016/09/18/5881039.html)
**问题**：如果方法一无法打开页面，那么可以尝试设置防火墙，设置里有控制各服务允许通过防火墙的设置，找到node,javascript相关字样的，勾选允许即可。
[解决该问题参考地址。](https://www.cnblogs.com/AwenJS/p/12840924.html)
#### 10、webpcak：
:::alert-info
**简介**：当项目变得很大之后再按照之前的资源引入方法会很难管理项目，不容易理清其依赖、加载顺序。webpack能自动找到所有依赖，将它们按顺序都打到一个js包中，最后引入。用Loader转换文件、plugin注入钩子。
**模块化规范**：commonJS：需要通过转换位es5才能在浏览器环境运行。AMD：异步方法加载依赖模块，用于解决浏览器环境模块化问题。现在使用es6也有模块化(但大部分浏览器还不支持)，也需要转换为es5。
:::
##### a1、原理：
Webpack 的构建流程可以分为以下三大阶段：在每个大阶段中又会发生很多事件，Webpack 会把这些事件广播出来供给 Plugin 使用。
- 初始化：启动构建，读取与合并配置参数，加载 Plugin，实例化 Compiler。
- 编译：从 Entry 发出，针对每个 Module 串行调用对应的 Loader 去翻译文件内容，再找到该 Module 依赖的 Module，递归地进行编译处理。
- 输出：对编译后的 Module 组合成 Chunk，把 Chunk 转换成文件，输出到文件系统。如果只执行一次构建，以上阶段将会按照顺序各执行一次。
- 注解：vue项目配置中看到的那些require(),module方法是node内置的，但程序是供webpack运行使用的。配置文件中都有`module.exports = {}`#里面写的配置都是最后导出使用的，内部使用的键值是webpack指定的有固定作用的。
- [原理学习地址。](https://www.jianshu.com/p/44e6741e3b7e)[webpack中文文档地址。](https://webpack.docschina.org/concepts/)
```js
//commonJS的导入导出。
const moduleA = require('./moduleA');
moduleA.exports = moduleA.someFun;

//AMD的模块定义，和导入使用。
define('module',['dep'],function(dep){return exports;});
require(['module'],function(module){});
```
**安装**：npm install webpack -g#全局安装。目录下使用：npm init#会在当前路径下生成一个mypackage文件夹，里面有package.json文件、webpack.config.js文件和src文件夹。
**项目中使用别名**：可以在build目录下的配置文件中使用
```js
//例如/build/webpack.dev.conf.js配置如下
const merge = require('webpack-merge')
const baseWebpackConfig = require('./webpack.base.conf')
// merge将其它文件的配置合并过来。
const devWebpackConfig = merge(baseWebpackConfig, {
    resolve:{
        alias:{"@c":"src/common/tools"}//别名对应路径。
    }
});
```
**require与import**：require 是赋值过程并且是运行时才执行，也就是异步加载。import 是解构过程并且是编译时执行，性能稍好。
**配置**：[webpack详细配置学习地址。](https://blog.csdn.net/c_kite/article/details/71279853)。[devserver属性学习地址。](https://blog.csdn.net/franktaoge/article/details/80083317)
##### a2、常用loader作用：
- vue-loader：解析vue文件。
- css-loader：一般vue-loader解析过后结果css-loader,处理过后会把样式都变成 module 形式，然后直接导出这个模块，模块中包含了 css 的源码跟模块的 id。
- style-loader：会引用css-loader生成的模块，然后在Html的head中加入style标签，当然也支持link引入等其它方式。
- vue-style-loader：在style-loader上的一层封装，不过还加了一些支持服务端的渲染。
- postcss-loader：把 CSS 解析成 JavaScript 可以操作的 AST，第二个就是调用插件来处理 AST 并得到结果。所以一般是放在css-loader之后，less-loader等之前。
- less-loader,sass-loader,scss-loader：css的预处理使用。scss是sass的3.0版本引入的语法，去除了之前的一些严格规则，且规则与css一致。
- style-resource-loader：向样式文件中添加全局的样式属性。

```js
//这三个loader均可以类似如下配置。
{
    test:/\.less$/,
    use:[
        'vue-style-loader',
        { loader: 'css-loader', options: { sourceMap: true } },
        { loader: 'postcss-loader', options: { sourceMap: true } },
        { loader: 'less-loader', options: { sourceMap: true } }
    ]
},{
    test:/\.scss$/,
    use:[{loader:'style-resource-loader',options:{patterns:"全局样式文件路径"}}]
}
```
样式写法部分注意：
```css
/*scoped表示该块css样式不做全局使用，编译后对应标签上会加上一个data-v-32423之类的标志，css样式会多在后面加一个
属性选择器，与全局区分，不至于污染全局样式。
lang指定使用的语言，不写时为普通css。*/
<style scoped lang="less">
.test{
    font-size:30px;
    /deep/.ac{color:red;}
    /* 子组件的最外层编译后才会被加上scoped标志，而内部元素不会，若是使用了第三方组件库时，其样式
    会被全局的覆盖，此时可以用/deep/来改变。*/
}
/* >>>也和/deep/一样作用，不过只有普通css中可用*/
.k >>> .a{width:500px;}
</style>
```
##### a3、常用的webpackPlugin：
这些plugin除了webpack自带的，其它插件还是需要npm安装的。
- **DefinePlugin**：用于配置可用的全局变量。也可以额外npm install -D dotenv然后根目录下创建.env文件编写，配置中使用require('dotenv').config()，然后一样插件中配置。
- **HtmlWebpackPlugin**：根据原html文件配置，打包后生成一个html文件，里面可以配置一些生成明细相关。[详细参数](https://www.cnblogs.com/wonyun/p/6030090.html)。
- **CopyWebpackPlugin**：用于将指定文件放到编译或打包后的文件中去，然后html页面可以引入使用：`<script src="<%=htmlWebpackPlugin.options.prefix %>static/jquery.min.js"></script>`。然后单页内可直接使用$()方法。
- FriendlyErrorsPlugin：友好提示插件，允许webpack编译成功和失败后输出的信息。
- HotModuleReplacementPlugin：热更新使用插件。
- CommonsChunkPlugin：分离公共模块使用的插件，具体见f。
```js
const webpack = require('webpack')
const HtmlWebpackPlugin = require('html-webpack-plugin')
const CopyWebpackPlugin = require('copy-webpack-plugin')
module.exports = {
    ...
    plugins:[
        new webpack.DefinePlugin({'process.env':require('../config/dev.env')}) //使用dev.env文件导出的环境变量。
        new HtmlWebpackPlugin({    //配置多页时需要使用多个该plugin。
            title:"测试app",//网页title，相应的html文件中使用<title>{%= o.htmlWebpackPlugin.options.title %}</title>才会有效
            filename: 'index.html',//输出后的名字
            template: '../src/index.html', //原html路径
            inject: true,
            chunks:'all' //指定导入的模块，多个写法》['vendor']
       }),
       new CopyWebpackPlugin([{    //一个数组的形式，所以可以写成多项。
        from: path.resolve(__dirname, '../static'),// from与to都可以是指定的文件或目录。
        to: 'static', //编译或打包后的项目下的目录。
        ignore: ['.*'] //可忽略匹配到的文件。
      }])
    ]
}
//###-----dev.env文件如下内容
module.exports = {NODE_ENV:'"development"',NUM:'20'}//注意对应变量是字符串的话需要 '"字符串"',而'20'则该变量是数值。
```
a4、eslint及vscode一套配置：
[eslint配置大全。](https://blog.csdn.net/p358278505/article/details/77429251)
##### a5、resolve与output：
```js
{
    // 只能有一个output
    output:{
        filename:"[name].js",//文件名，name为占位，[fullhash]为使用hash。
        path:__dirname + '/dist',// 输出位置
        publicPath:"/" //各个资源路径前面添加的前缀。
    },
    // 项目中
    resolve:{
        extensions:['.js','.vue','.json'],
        alias:{'vue$':"vue/dist/vue.esm.js"}
    }
}
```
##### a6、devtool：
为便于调试的设置。编译打包后的代码出错时难以找到编译前的位置调试，设置devtool可以让其找到编译前报错位置。
```js
{
    //有5个值：cheap,eval,module,inline,source-map。这些可以互相组合
    devtool:"cheap-module-eval-source-map"
}
```
- eval：不生成.js.map文件，仅仅是在每一个模块后，增加sourceURL来关联模块处理前后对应的关系。
- source-map：打包后有map文件，相应的要在浏览器设置中开启：设置齿轮/preference/Sources/Eable javascript sources。
- inline：该属性不会生成独立的 .map文件，而是将 .map文件以dataURL的形式插入。
- cheap：该属性在打包后同样会为每一个文件模块生成 .map文件
- module：该属性的配置也是生成一个没有列的信息的sourceMaps文件，同时loader的sourcemap也被简化成为只包含对应行的。
- 开发环境常用：cheap-module-eval-source-map。
- 生产环境常用：cheap-module-source-map。
- [详细学习地址。](https://www.cnblogs.com/jkr666666/p/11067189.html)
##### b、devServer部分(配置反向代理)：
**正向代理**：代理是处于客户端和服务器中间的一台计算机，正向代理是接受客户端的链接，然后向目标服务器请求资源，逐步返回给客户端。正向代理的服务器与目标服务器不在同一网段内，面向服务器。如vpn。
**反向代理**：面向的是客户端，对外表现为一台服务器，目标服务器放在内网，而反向代理服务器作为网关，访问内网中的服务器需要经过代理服务器，<i class="green">所以目标服务器更安全且压力变小，代理服务器还负责分发内容，缓存前端资源，因此也能优化前端性能。</i>
vue中使用代理来处理跨域，在config文件夹下的Index.js文件中配置，这个文件是配置运行、打包的一些具体属性的，exports中对应的键值与package.json中的scripts里设置的运行命令对应，用vue-cli初始化的项目则默认是dev和build。
**webpack-dev-server参数**：--hot#热更新，修改代码后，只会替换原来块的代码，而不会整个刷新页面。--open#启动后打开浏览器。--config#指定使用的配置文件。

```js
// 一般在webpack.base.config.js文件。注意是使用0.0.0.0而不是Localhost，不然无法ipv4访问。
const HOST = process.env.HOST || '0.0.0.0';

const devWebpackConfig = merge(baseWebpackConfig, {
  devServer: {
      host:HOST,  // 设置可访问的地址。process.env.HOST表示本机ip可访问。
      port:3320, //访问网页的端口号。
      // 浏览器访问的是，本机ip:端口+路径。终端会显示代理访问记录
      proxy:{
          "/api": {
				target: "'http://10.18.110.107",//代理地址，反向代理的服务器不需要端口。
				changeOrigin: true,// 是否跨域
                secure: false,// https请求需要该设置
				ws:true,// 是否使用https，！！如果target中使用https的话依然还是会使用。
				pathRewrite: {// 设置此项。将满足'^/api'的替换为空。
					'^/api': '', //如请求http://localhost:3000/main时写成=》/api/main即可。
				}
			}
      },
      // dev环境一般使用‘/’
      publicPath:"/" //引用静态资源的公共路径。静态资源最终访问路径 = output.publicPath + 资源loader或插件等配置路径
  },
  build:{}
}
//     axios.get('/api/tasktime')
```
node中的另一种代理是解决跨域使用的代理，node本地自启一个服务用于接受本地请求，然后向服务端请求，这样就变成了服务端向服务端请求，不受跨域限制。<i class="green">不过这只是在开发时使用，打包后失效，所以记得生产环境将代理地址改为服务器域名。这种普通代理也使用上面的方法。</i>
[vuejs设置跨域方法学习地址。](https://www.cnblogs.com/wangqiao170/p/9288160.html)[publickPath解释相关。](https://juejin.cn/post/6844903601060446221)
##### c、vue多页面应用配置：
`/build/webpack.base.config.js`文件添加多个主js文件入口，形如：
```js
module.exports = {
    entry:{
        app:'./src/pages/home/min.js',
        one:'./src/pages/game/min.js'
    }
}
```
`/build/webpack.dev.conf.js`文件添加如下配置。
```js
const devWebpackConfig = merge(baseWebpackConfig, {
    plugins:[
        // 第一个页面的。
        new HtmlWebpackPlugin({
            filename: 'home.html',//这个文件名在访问多页路径时有用，所以不能重名。
            template: './src/pages/home.html',//这里指定的是文件位置，要注意！！
            inject: true,
            //chunks指定页面要使用哪些js代码块，多页面时要指定一个唯一的主js块
            //不写的话会默认导入所有，这回导致一个html页面导入其它模块的所有js块。
            chunks: ['manifest', 'vendor', home]
        }),
        // 其它页面的复制，更改相应名称即可。
});
```
`/build/webpack.prod.conf.js`文件添加如下配置。
```js
const webpackConfig = merge(baseWebpackConfig, {
    plugins:[
        // 其它页面复制，相应的更换index，app即可。
        new HtmlWebpackPlugin({
            filename: config.build.index,
            template: 'index.html',
            inject: true,
            minify: {
                removeComments: true,
                collapseWhitespace: true,
                removeAttributeQuotes: true
            },
            chunksSortMode: 'dependency',
            //(在这里和你上面chunks里面的名称对应)
            chunks: ['manifest', 'vendor', 'app']
        }),
    ]
});
```
`/config/index.js`文件添加：
```js
module.exports = {
    build:{
    //build时导出的文件。
        index: path.resolve(__dirname, '../dist/index.html'),
        one: path.resolve(__dirname, '../dist/one.html'),
        two: path.resolve(__dirname, '../dist/two.html'),
    }
}
```
根据上面相应的位置创建js、vue、html文件。home.vue和home.html文件种将id更改。
```js
//one.js文件。
import Vue from 'vue'
import one from './one.vue'
import router from './router'

Vue.config.productionTip = false
/* eslint-disable no-new */
new Vue({
    el: '#one',
    router,    //加上路由的话可以在路由页
    render: h => h(one)
})
```
**访问**：http://127.0.0.1:8080/home.html#/[vue多页面应用配置教程。](https://blog.csdn.net/weixin_44135121/article/details/94445734)
##### d、当前shell添加环境变量：
```bash
// windows中使用set设置一个临时的环境变量
"dev": "set NODE_ENV=development &&  webpack-dev-server --open --hot"
// mac中使用：export
"dev": "export NODE_ENV=development &&  webpack-dev-server --open --hot",
// ————————为了统一两个系统，便于开发，使用一个第三方包:cross-env
"dev":"cross-env DEV_ENV=test webpack-dev-..."
#但是运行程序中虽然能拿到变量名，但无法匹配到，进行如下设置：
#webpack.dev.conf.js的插件中
plugins: [
        new webpack.DefinePlugin({
            "process.env": require("../config/dev.env"),
            "process.env.DEV_ENV": JSON.stringify(process.env.DEV_ENV),#添加该项!!猜测其它地方如此使用也可。
        }),
        ...
        ]
```
使用vue-cli-server还可以在最外层文件中添加环境变量。
##### e、module项配置：
顾名思义，module是模块，而webpack中将每个文件当做一个块，所以，module项配置是处理每个文件的一些配置，大体如下：
- [多种loader的安装及配置使用参考地址。](https://www.webpackjs.com/loaders/less-loader/#安装)
- 编译运行时一直卡住的问题：可能是相应的loader版本较高，尝试安装低版本。
```js
module: {
    // 定义多项规则
  rules: [{
      test: /\.js$/,    // 匹配指定的文件类型。
      //use: ['babel-loader?cacheDirectory'],//use指定对文件使用的插件，可以多项，配置规则。
      use: [{
          loader:'babel-loader',//指定使用的插件。
          options:{
              // 这里可以写.bablesrc中的格式配置。
              cacheDirectory:true,
          },
          // enforce:'post' 的含义是把该 Loader 的执行顺序放到最后。还可以是 pre，代表把 Loader 的执行顺序放到最前面
          enforce:'post'
      }],
      // 只命中src目录里的js文件，加快 Webpack 搜索速度
      include: path.resolve(__dirname, 'src'),
      exclude:/node_modules/ //指定不需要编译的目录。
    }]
}
```
##### e1、px转rem配置：
使用插件postcss-plugin-px2rem，安装：npm i postcss-plugin-px2rem -D。然后在vue-loader下配置。！移动端使用。
```js
var px2rem = require('postcss-plugin-px2rem');
modules:{
    rules:[{
        test: /\.vue$/,
        loader: 'vue-loader',
        options: {
            // 配置，rootValue值为1rem转换为px的大小。
            postcss:function(){return [px2rem({ rootValue: 100 })];}
        }
    }]
}
```
该插件只负责转换尺寸和单位，根元素字体大小在html文件用js去改变，两者配合使用。
##### f、代码分割：
用于将更多的公共模块从大的模块中分离出来。
- 添加入口的方法来分离代码块：entry多加一个想要分离的js文件，如果这个文件也使用了一些其它公共的模块，同样会同这个js文件进入一个bundle中。
- 使用CommonsChunkPlugin：插件部分添加该插件和规则，示例如下：
```js
{
    plugins:[
        new webpack.optimize.CommonsChunkPlugin({
            name: 'tools',
            // minChunks可以是数值，Infinity时表示无限制。
            minChunks(module,count) {
                // module.resource为文件路径，count是引用的次数。
                // 将/utils下的tools.js文件分离出来。    ！！为true时表示进入该chunk。
                return (module.resource && /\.js$/.test(module.resource) && module.resource.indexOf('/utils/tools.js') !== -1)
            },
            chunks:[], //也可以直接指定哪几个chunk在这个bundle
            minSize:3 //最小包含的模块数量
        }),
    ]
}
```
- 使用CopyWebpackPlugin将js文件直接从html引入，将js文件放到对应的静态资源文件夹中即可。[Index.html文件引入js文件。](https://blog.csdn.net/qq_15253407/article/details/89491255)
<i class="label1">问题集</i>
- 解析less文件时提示：TypeError: loaderContext.getResolve is not a function：换使用较低的less-loader版本。4.1.0
- 解析less，sass等文件时提示：Module build failed: Unrecognised input。按a2中方法配置loader即可，一般用默认模板的话，utils中是已经配置好的，安装好loader即可用。
#### 11、uni-app的使用：
**介绍**：uni-app 是一个使用 Vue.js 开发所有前端应用的框架，开发者编写一套代码，可发布到iOS、Android、H5、以及各种小程序（微信/支付宝/百度/头条/QQ/钉钉/淘宝）、快应用等多个平台。结合Hbuilder x使用，文件新建一个项目选择uni-app项目(网站、app、小程序都选这个)。[uni-app官网。](https://uniapp.dcloud.io/)[插件市场](https://ext.dcloud.net.cn/search?q=uni-ui)。
**项目目录结构**：pages文件夹存放业务页面，pages/index/index.vue页面是app打开时的引导页面。创建其它页面时新建一个文件夹然后在文件夹内建页面，可以多个页面放一个文件夹。
static文件夹存放静态资源文件。main.js文件是vue实例化入口。APP.vue页面写全局样式，生命周期函数。manifest.json文件配置应用名、appid、图标等。package.json配置路由，选项卡、插件、导航条等。
**插件、组件的使用**：在插件市场中可以搜索想要的插件，点击hbuildx导入能直接调用hbuilderx安装插件，安装好后会放在目录下的components中，当作组件调用即可，示例：
```
<pop type="text"></pop> //不用:来表示绑定。
import pop from "@/components/load.vue"    //导入。
export default{
    data(){
        return {text:'hh'}
    }
}
```
一些常用插件地址：[弹出框(顶、中、底弹出)。](https://ext.dcloud.net.cn/plugin?id=329)[头部导航插件。](https://ext.dcloud.net.cn/plugin?id=52)[时间、日期、城市联动选择器。](https://ext.dcloud.net.cn/plugin?id=273)[cool组件库文档地址，功能还算比较全面。](http://uni.cooljs.vip)
cool组件库的大体使用：从[git地址](https://github.com/cool-team-official/cool-uni)下载到本地，把里面的src/cool文件夹复制到项目根目录中，然后pages.json文件加入以下配置：
```
{
    "easycom": {
        "autoscan": true,
        "custom": {
            "cl-(.*)": "@/cool/ui/components/$1/$1.vue"
        }
    },
    pages:[]
}
```
然后在APP.vue页面的style引入它的css文件，如下：
```
<style lang="scss">
@import "cool/ui/static/css/index.scss";
</style>
// 其它单页面中导入组件：然后可以按照文档中的教程使用了。
import clButton from "@/cool/ui/components/button/button"
```
**app唤醒页和引导页**：app中打开都有一个广告页面，第一次使用app都有一个引导页面，在uni-app开发app时需要新建一个页面来放置它们=》在index文件夹下新建一个Introduct.vue页面，然后在package.json文件设置如下：
```
{
    "pages":[{
        "path":"pages/index/introduct",
        "style":{
            "app-plus":{"titleNView":false} //静用掉自带的顶部，这样才能全屏显示。（index页面首页也可以设置这个）
        }
    }]
}
```
建议将唤醒页和引导页放在同一个页面。在生命周期函数中写一个定时器，3秒后跳到首页。
```
onReady(){
	setTimeout(()=>{
		this.$router.replace('../index/index')
	},3000);
},
```
**页面生命周期函数**：
onLoad	监听页面加载，其参数为上个页面传递的数据，参数类型为Object（用于页面传参
onShow	监听页面显示
onReady	监听页面初次渲染完成
onHide	监听页面隐藏
onUnload	监听页面卸载
onPullDownRefresh	监听用户下拉动作 ，一般用于下拉刷新
onReachBottom	页面上拉触底事件的处理函数
onPageScroll	监听页面滚动 ，参数为 Object
onTabItemTap	当前是 tab 页时，点击 tab 时触发。
onShareAppMessage	用户点击右上角分享
**尺寸单位**：uni-app中使用upx为自适应单位，与小程序一样，750upx占满屏宽，设计稿不是750大小的需要与750算一个比例，然后在量一个元素大小时乘以该比例转化为upx大小即可。动态的写入upx单位不会生效，需要转为px再写入。如果要转换upx，只要在manifest.json里配置下面"transformPx" : true。
[uni-app中的跨域解决。](https://blog.csdn.net/paopao79085/article/details/91948809)
#### 12、页面中引入富文本编辑器：
web中使用的富文本编辑器比较多，这里是两个自己尝试过的：
wangeditor：比较轻便，所以功能没有其它几样多，因为简便所以比较容易引入，几乎不会报异常错误。[wangeditor使用参考地址。](https://www.jianshu.com/p/52852d39f869)
vue项目中安装：`npm i wangeditor -S`#使用配置如下：
```
<template>
  <div id="wangeditor">
    <div ref="editorElem" style="text-align:left;"></div>
  </div>
</template>
<script>
import E from "wangeditor";
export default {
  name: "Editor",
  data() {
    return {
      editor: null,
      editorContent: ''
    };
  },
  mounted() {
    this.editor = new E(this.$refs.editorElem);
    // 编辑器的事件，每次改变会获取其html内容
    this.editor.customConfig.onchange = html => {
      this.editorContent = html;
      this.catchData(this.editorContent); // 把这个html通过catchData的方法传入父组件
    };
    this.editor.customConfig.menus = [
      // 菜单配置
      'head', // 标题
      'bold', // 粗体
      'fontSize', // 字号
      'fontName', // 字体
      'italic', // 斜体
      'underline', // 下划线
      'strikeThrough', // 删除线
      'foreColor', // 文字颜色
      'backColor', // 背景颜色
      'link', // 插入链接
      'list', // 列表
      'justify', // 对齐方式
      'quote', // 引用
      'emoticon', // 表情
      'image', // 插入图片
      'table', // 表格
      'code', // 插入代码
      'undo', // 撤销
      'redo' // 重复
    ];
    this.editor.create(); // 创建富文本实例
  }
}
</script>
```
**tinymce**：国外的，默认是英文，中文版的需要下载语言包。[参考学习地址。](https://www.cnblogs.com/wisewrong/p/8985471.html)[语言包下载地址。](https://www.tiny.cloud/get-tiny/language-packages/)
引入后报..dont support (text/html) ..css的错误：在`<style></style>`中用@import url("");引入css样式。
出现找不到中文语言包的问题：！暂未解决。
[百度umeditor下载地址(选择jsp)。](http://ueditor.baidu.com/website/download.html)[使用参考学习地址。](https://blog.csdn.net/fanhu6816/article/details/81223909)
#### 13、axios：
内部依然封装的ajax使用。npm install axios
```js
import axios from "axios";
const URL = require("./index");
// 响应时间
axios.defaults.timeout = 5000;
// 请求头设置
axios.defaults.headers.post["Content-Type"] =
    "application/x-www-form-urlencoded;charset=UTF-8";
// 不同的环境可以设置不同的地址。
if (process.env.NODE_ENV === "production") {
    axios.defaults.baseURL = "https://nb.com";
} else {
    axios.defaults.baseURL = URL.dev.requestUrl;
}

// 请求拦截器
axios.interceptors.request.use(
    config => {
        // 这里添加加载动画
        if (config.method === "post") {
            config.data = JSON.stringify(config.data);
        }
        return config;
    },
    err => {
        // 加载动画关闭
        console.info("请求错误");
        return Promise.reject(err);
    }
);

// 响应拦截器
axios.interceptors.response.use(
    res => {
        // 关闭动画，一些公共的错误，可以在这里处理。
        if (res.errorCode !== "0") {
            console.info("返回失败", res);
        }
        return Promise.resolve(res.data);
    },
    err => {
        // 关闭动画
        console.info("返回错误");
        return Promise.reject(err);
    }
);
export default axios;
// ...main.js将其绑定到原型上：vue.protetype.$rpc = axios;
```
返回的内容如下：`{config:{},data:{},headers:{},request:{},status:200,statusText:'ok'}`
- config中包括设置axios时的url、请求方式、headers、baseUrl等。
- data是服务端返回的数据内容。
- headres是请求中使用的头部内容。
- request：包含custom、onerror、onabort等。
[axios配置，学习地址。](https://www.cnblogs.com/mica/p/10795242.html)
#### 14、NUXTJS：
[NUXTJS中文网。](https://www.nuxtjs.cn/guide/configuration)
#### 15、mock数据的使用：
1、使用mockjs
- 安装：npm i mockjs -D。建立一个放置数据的目录，用json文件存放数据，新建一个mock.js文件。
- mock.js文件配置请求的路径和对应的数据：
```js
const Mock = require("mockjs");
const _url = "https://nb.com";    //如果使用了axios，这里路径要与axios配置的baseUrl一致。
//请求路径、请求类型、数据。
Mock.mock(`${_url}/index/test`, "get", require("./moc.json"));
Mock.mock(`${_url}/index/use`, "post", require("./moc.json"));
```
- main.js将其导入即可：`import Mock from "../../../mock/index";`#使用mock数据时不要与代理路径冲突。

2、利用ajax可请求文件的方法。
3、使用node在开一个本地服务用于返回mock数据，让代理目标地址更改为该服务地址。
[使用本地mock数据。](https://blog.csdn.net/zhushikezhang/article/details/104447438)
**mock与测试环境切换**：可以在运行命令多添加一个参数，用于判断是否mock环境。
`"dev:mock": "cross-env DEV_ENV=mock webpack-dev-server --inline --progress --config build/webpack.dev.conf.js mock"`
config/index.js文件中检测环境，修改url，然后axios配置文件中使用该文件的url，mock.js文件中的地址写为固定即可。
```js
// process.argv获取传入的所有参数。
if (process.env.DEV_ENV==='mock') {
    // mock数据地址。
    url = "http://mock_test.com";
} else if (process.env.DEV_ENV==='sit') {
    // 测试环境
    url = "http://test_env.com";
} else {
    // 正式环境
    url = "http://127.0.0.1:3000";
}

module.exports = {
    dev: {url:url,}
}
```
#### 16、vconsole插件：
移动端上网页调试颇为不便，使用vconsole模拟控制台功能进行调试。
- 安装：npm install vconsole
- main.js中使用：
```js
import Vconsole from "vconsole";
// 开发环境中使用。
if (process.env.NODE_ENV === "development") {
    let vConsole = new Vconsole();
    Vue.use(vConsole);
}
```
#### 17、bable插件：
webpack只能将一部分es6语法转换为es5，而一些高级的es6语法，和部分es7语法无法转译，这就需要bable。bable包含：preset-env、plugin-component、polyfill等多个子插件。
<b class="violet">项目中的.bablelr是bable的配置文件，而需要使用的话需要在webpack的modules中引入bable-loader。</b><b class="gray">babel中引入的分为转换插件（转换代码，编译）和语法插件（解析特定类型的语法，如果你已经使用了相应的转换插件，则不需要指定语法插件。）</b>
使用前先安装：`cnpm i babel-core babel-loader babel-plugin-transform-runtime -D`
**bable中常用的插件**：7.0以下的版本插件几乎以abel-plugin-开头，7.0以上的以@babel/开头，两个版本混用会导致解析失败。
<i class="lable2">preset部分</i>
- @babel/env对应6.0+的babel-env：为目标浏览器中没有的功能加载转换插件。不太推荐preset-env。
- @babel/polyfill：可以使用诸如 Promise 和 WeakMap 之类的新的内置组件、 Array.from 或 Object.assign 之类的静态方法，不过是全局的，所以会对全局变量造成污染，现在已经不建议使用。安装时使用`--save`
- transform-vue-jsx：可以支持jsx语法（ts）。
- [制作可在babel中配置的插件。](https://github.com/jamiebuilds/babel-handbook/blob/master/translations/zh-Hans/README.md)
- stage系列插件：它们用于解析es6,7等版本js语法的方案，包含0-4，功能逐渐降低，对最新语法处理的程度，一般使用stage-2。
- transform-runtime：只用于开发环境，由于webpack的打包机制会将模块中导入的都打包到一起，然而一些较大的公共包也会有被打入多个chunk组的情况，transform-runtime可以提取分离它们

```js
{
　　// 此项指明，转码的规则
  "presets": [
    [
      "@babel/env",
      {
        "targets": { //列出一个最小支持版本。或"targets": "> 0.25%, not dead"
          "edge": "11",
          "firefox": "60",
          "chrome": "67",
          "safari": "11.1",
        },
        "useBuiltIns": "usage",//usage会有一些优化作用。
      }
    ],
    "stage-2"
  ],
  "plugins": [
    // 下面这个选项是引用插件来处理代码的转换，transform-runtime用来处理全局函数和优化babel编译
     "transform-runtime",//transform-runtime为node_modules中已安装的插件（带babel-plugin-前缀）。
     "transform-remove-console", //编译后移除console
     //自定义的plugin。component是作为参数传入。还有import，对应的需要安装babel-plugin-component和babel-plugin-import
     ["component", [{    
        "libraryName": "element-ui",           //按需引用element-ui插件
        "libraryDirectory": "src/components",    //指定从哪导入。
        //"styleLibraryName": "theme-default"   //按需引用element-ui主题 
     }]]
  ],
  "comments": false,// 在生成的文件中，不产生注释
    // 下面这段是在特定的环境中所执行的转码规则，当环境变量是下面的test就会覆盖上面的设置
  "env": {
    // test 是提前设置的环境变量，如果没有设置BABEL_ENV则使用NODE_ENV，如果都没有设置默认就是development
    "test": {
      "presets": ["env", "stage-2"],
      "plugins": [ "istanbul" ]    // instanbul是一个用来测试转码后代码的工具
    }
  }
}
```
**webpack中配置如下**：[bable官网](https://www.babeljs.cn/docs/babel-preset-env)。[.babelrc文件作用及属性，部分组件按需引入，需要配置。](https://www.cnblogs.com/wulinzi/p/8079509.html)
- `{ test:/\.js$/, use: 'babel-loader', exclude:/node_modules/ }`#exclude指定排除掉的文件夹。 如果不排除 node_modules， 则Babel 会把 node_modules 中所有的 第三方 JS 文件，都打包编译，这样，会非常消耗CPU，同时，打包速度非常慢；

#### 18、html2canvas使用：
用于将页面的html节点转化为图片，注意若其中包含图片，使用img标签而不要使用背景图。否则生成的图片不清晰。
```js
import html2canvas from "html2canvas";
const _el = document.getElementById("img");
 new html2canvas(_el, {
        scale: 3, //缩放数，大于1表示生成高清。
      }).then((canvas) => {
        // canvas为转换后的Canvas对象
        let oImg = new Image();
        oImg.src = canvas.toDataURL(); // 导出图片
        });
```