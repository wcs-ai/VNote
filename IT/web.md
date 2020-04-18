### 一、HTML
#### 1、svg：
```
<svg width="300" height="300"></svg>
<rect x="" y="" width="" height="" style="fill:red;stroke-width:2;stroke:blue;"/>
//rect标签绘制矩形，x,y为位置,fill,stroke等属性可写在style外。
<circle cx="" cy="" r=""/>绘制圆，cx,cy为位置。
<ellipse cx="" cy="" rx="" ry=""/>绘制椭圆，cx,cy为位置，rx,ry为宽高。
<line x1="0" y1="0" x2="20" y2="20"/>绘制线条，x1,y1,x2,y2为起始及结尾坐标。
<polygon points="10,10 20,20 150,320"/>绘制多边形，points中没两个值是一对坐标。
<polyline points=""/>绘制折线
<path d="M10 5L100 15C19 60,50 99"/>绘制任意路径、形状。d中属性如下：
```
M：移动至起始点，必须。L：直线结束点。H：从当前点画水平线。V:垂直线。
C:三阶贝塞尔曲线。Q：二阶贝塞尔曲线。
(将元素使用appendChild()方法动态添加到svg中并不会被显示出来,可以使用svg.
innerHTML方法将元素写入)。
http://www.mamicode.com/info-detail-1988813.html
#### 2、外部资源引入标签：
`<embed></embed>、<iframe></iframe>、<object></object>`
`<embed type="image/svg+xml" codebase="http:"></embed>`标签是H5新标签所有主流浏览器都支持，codebase属性中写资源路径,可以引入脚本;类似iframe标签用于引	入外部资源(`<iframe>`标签只在大部分浏览器可用),但规范的xhtml和html中不支持			
`<embed>`标签.`<object data="rect.svg" type="image/svg+xml" codebase="http">	`
`</object>`1标签是H4的新标签，浏览器支持性差，但不能引入脚本.(引入的文件
中的js对象和本页的js对象是不能共用的,且在引入的文件中获取的url也不是该页的)
#### 3、第三方资源的加载：
前端中有很多加载资源的标签例：iframe,video,audio,img,script,link等是用src属性或是用href属性，一些标签不能跨域加载资源多数标签允许跨域加载资源。除了link和script外其它标签几乎都有onload事件和onerror事件可在元素上添加这两个事件做加载成功和加载失败后的处理。js代码中的函数块语句需要达到相应的条件才能触发（body，head中添加的onload和<script></script>中的window.onload=“”除外)就算是onmouseout指定的函数也不行，因为它运行的前提就是有onmouseover被触发。
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
ctx.arc(x,y,r,stAngle,Math.PI*2)//绘制圆,控制第5个参数大小控制弧长。
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
```
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
```
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
```
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
### 二、CSS
#### 1、布局注意：
css中id的等级强于class强于标签名，只要带有id名的选择器（id选择器或是带有id名的兄弟选择器）语句块中定义的样式就是浏览器会显示的，他会覆盖类选择的器、标签选择器（前提：两个不同的选择器作用在一个元素上时；如果是两个相同类型选择器作用在同一个元素上以后一个选择器为主(为主指的是在相同的属性定义上)。
box-sizing:content-box;//定义的width不包含border宽度，即总宽度= padding值+border值+width值（margin值不算元素宽度）但如果是背景图片依然会占据	padding部分（不会占据border部分），文本内容不会占据padding部分；Box-sizing:border-box;//定义的width包含padding值和border值即：总宽度=width；背景图片占据padding部分。（伪类元素定义出来的是content-	box模型，即使通配符中已经定义了box-sizing:boder-box）。
box-sizing:border-box的前提下子元素相对于父元素定位是根据父元素的content的宽高来定位（border值，padding值不算）。
将一个元素定义为行内块时其会产生默认的外边距，即使在通配符中已经定义了margin为0px。
元素定位为relative时只能在样式中定义其宽度,其高度只等于它的子元素的高度加它的内边距加外边距之和(top，left等不算).
font-style:normal;去除<em></em>标签的斜体样式。
textarea禁止改变文本域大小：resize:none
自动换行：word-break：break-all或white—space：normal来实现自动换行。
引入外部文件中的资源地址不能用斜杠开头(一些浏览器不能识别)固定定位只相对于window窗口，无论该元素放到上面元素里。
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

【图片置中】
background:url(" ") no-repeat;
background-position:50% 0;
css所有选择器：http://www.w3school.com.cn/cssref/css_selectors.asp
(css选择器、js中的querySelect选择器、jquery封装的选择器中属性选择器
[dat~=src],[dat|=src]中要求这个属性中的值是以空格分割开的).
display：none将元素归为无(不占位置但其中内容任会解析)。
#### 5、尺寸单位：
em单位是根据当前元素字体大小而变化的,列入当前元素font-size:14px;
width:10em,此时width为140px(每1em为字体大小)，而rem是继承根部元素(html)的
字体大小的,例:html{font-size:16px;}.div{width:10rem;}//width为160px；vw视
窗宽度,1vm相对于视窗宽度的1%,vh:视窗高度;vmin,vmax:vw和vh中选择最小/最大那个。
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
```
el{
    box-reflect:below 1px linear-gradient();//box-reflect属性为元素添加倒影
    //效果，第一个值设置方向，第二个值为倒影与元素的距离，第三个值为线性渐变，将
    //渐变设为透明度逐渐增加的白色效果较好，做兼容处理时box-reflect前和渐变前
    //都加上前缀。
}

```
css3剪切：
```
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
```
el{
    /*默认的贝塞尔速度曲线是从(0,0)到(1,1)的一条匀速直线，括号中的四个数值是
    //贝塞尔曲线中的两个点的位置，通过这两个点拉扯曲线，速度安装曲线弯曲度改变。
    transition:all 1s cubic-bezier(0.7,0.1,0.9,1);
}

```
user-select为css3属性，需要做兼容。
perspective-orign:50% 50%;//改变视角位置坐标
#### 8、一个让全局提示的写法：
```
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
### 三、javascript
#### 1、拦截浏览器回退操作：
```
pushState()和popstate是H5的新属性。
history.pushState(null,null,document.URL);
window.addEventListener('popstate',function(){
history.pushState(null,null,document.URL);
});
```
#### 2、转码：
```
encodeURI('汉字');
decodeURI();
//url传参汉字时可以先encodeURI()对中文编码再用decodeURI()转码
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
WebSocket是一种在单个TCP连接上进行全双工通讯的协议，它允许服务端主动向客户
端推送数据，浏览器和服务器只用完成一次握手两者之间即可创建持久性的连接，并
进行双向数据传输。
需要先安装pywebsocket支持websocket服务
```
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
workers是让一个js文件在后台执行不影响页面执行速度的一种技术,对一些需要处理
大型的数据是一个不错的优化选择，且主流浏览器都支持(除了IE）
// 一个js文件,a.js
```
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
```
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
三元运算符用于赋值：
val = val>20 ? 20 : 10;//表示如果val大于20val值就为20，否则为10；
三元运算符中写多条语句：
a == 20 ? (a=15,alert(a)) : (a = 21,alert(a));

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
document.createElement("p");//创建一个节点
document.createTextNode("text");//创建文本节点
el.appendChild(c);//添加孩子节点：末尾添加
fa.insertBefore(el,fa.lastChild);//插入节点：fa中插入节点el,在最后一个节点前插入。
el.parentNode;//父节点,选中el的父节点。
el.previousSibling;//选取上一个节点
el.nextSibling;//选取下一个节点
a.contains(b)/a.compareDocumentPosition(b)//判断一个元素是否包含另一个元素
  el.removeChild(ak);删除元素节点//只能用父元素删除子元素的方式
  el.cloneNode();复制元素//复制的元素会复制其所有属性,但并不会复制其文本内
容和html结构。
el.childNodes;//返回元素的所有子元素(两种不同情况返回的长度)
```
<p><b>1</b><b>2</b><b>3</b></p>//p.childNodes.length>>3
<p>
<b>1</b>
<b>2</b>
</p>//p.childNodes.length>>4
```
el.childNodes[0].nodeName;//节点名,为间隙或文字则为#text为元素则为
大写的标签名,nodeValue;//节点中的文本内容(非html结构)
#### 8、网页中js调用摄像头：
```
<video id="but" onclick="get()">调用摄像头</video>
<canvas id="canvas"></canvas>
<div onclick="show()"></div>
<script>
var width = window.innerWidth;
var height = window.innerHeight;
// 点击调用摄像头
    function get(){
        var but = document.getElementById("but");
        // obj传到getUserMedia()方法中
        var obj = {
            // 设置视图大小，允许录制音频
            video:{width:width, height:height},
            audio:true
            }
        // 兼容性处理
        let photp = navigator.mediaDevices.getUserMedia(obj) ||
                    navigator.webkitGetUserMedia(obj) ||
                    navigator.mozGetUserMedia(obj) ||
                   navigator.msGetUserMedia(obj);
       // 会先获取权限(用户控制)，调用成功的话则运行then()方法
       photo.then(function(MediaStream){
           but.srcObject = MediaStream;//图像显示到but元素中
           but.play();// 显示
       });
       // 调用失败则运行catch()方法
       photo.catch(function(){alert("调用摄像头失败")});
    }
// 点击拍照
    function show(){
        var canvas = document.getElementById("canvas");
        var ctx.canvas.getContext("2d");
        // 上面获取到的but是RGB数组对象。
        ctx.drawImage(but,0,0,width,height);
    }
</script>
```
https://www.zcfy.cc/article/choosing-cameras-in-javascript-with-the-mediadevices-api
https://blog.csdn.net/jvid_sky/article/details/53213898
#### 9、js获取改变内嵌样式、外联样式：
原生js中使用ele.style.property的方法只能获取内嵌样式中的style属性或在js		语句中写入的属性,使用:
window.getComputedStyle('元素','伪类').getPropertyValue('属		性')的方法可以获取元素的css中所写的样式,但这两个方法都是只读属性，不能用	
来改变其中的css样式(getComputedStyle()方法中不能像选择器一样选中元素，而是要通过专门的元素选择器选好之后传进去)。
js写入内嵌样式的方式还可以是：ele.style["color"] = "red";
可以使用这两种方法来改变其元素的css样式(但是会显示在内嵌样式中)：
(1)ele.style.cssText=”width:150px;height:200px;”;//重写其css样式表
(2)ele.style.setProperty(‘样式名’,’样式值’);//setProperty()方法设置
属性是在style中的并不是一个直接的属性。
#### 10、选择本地图库中的图片显示并压缩：
input中的file属性提供了一个从本地图库选择图片文件的功能,以下代码将选中的图
片显示在页面上：
```
<img id="img"/>
<input type="file" onchange="get(this)" multiple="multiple"/>
<!--multiple允许一次选择多张图片-->
<canvas id="can" width="500" height="300"></canvas>
<form id="form"></form>
```
```
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
```
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
```
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
</script>

readyStatechange事件(试过google，不支持)
img.onreadystatechange = function(){
    if(img.readyState=="complete"||img.readyState=="loaded"){
        document.getElementById("img").innerHTML="ok";
    }
}

```
https://www.cnblogs.com/snandy/p/3704938.html
#### 15、js的兼容性问题：
事件的兼容性处理：
```
el.onclick = function(event){
    //ie中可直接用window.event/event读取事件，firfox中通过传参传入事件
    var eve = event||window.event;
}

```
元素选择：
document.idName/document.getElementById("");//IE
document.getElementById();//其它,统一使用此法
el.parentElement/el.parentNode;//IE,统一使用parentNode

元素中写入内容：
el.innerText = "";//多数支持
el.textContent="";//低版本的firefox使用，建议全部用innerHTML代替。
ajax兼容问题：
```
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
```
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
<i class="label1">使用原生ajax来上传文件</i>使用jquery封装的ajax和axios的ajax先用formdata封装文件再上传时发现浏览器的xhr/head项中没有显示FormData项数据，在请求头中修改Content-Type:'multipart/form-data'后发现head项出现FormData数据了，但是有报跨域问题，这可能跟axios源码中检测数据类型，做的特别处理有关。
```
<form id='a'><input type="file" name="file"/></form>
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
```
[各种Content-Type对应的数据，但是试过，似乎不太有效。](https://www.jianshu.com/p/10cdbb35ac87)
<i class="label1">使用ajax注入分页</i>使用document.write(data)的方法要求分页里只有元素结构（没有meta,html,body等在主页中重复的标签）,可是这样仍会把主页<head></head>标签中的外链样式覆盖为无,我们可以再写一个分页专门用于装效head标签及其里面的外联样式（link,script等）;可是外联的js语句只执行一次就	无效了!!（弃）;若注入分页的js
代码用引入的方式则`<script async='async' src=''></script>`或在注入的ajax代码中将async改为false或ajax代码后加一个延时器延时绑定事件。(一些坑爹的后台框架会劫持所有ajax请求导致报错所以使用需谨慎,本地打开带有使用ajax的文件会产生跨域问题);
<i class="label2">ajax中地址为空情况</i>ajax中如果url地址为空在提交时会变成提交到当前页url路径。jquery的ajax中不填写dataType值时jquery会自动判断返回值的类型(所填写的data中的格式不能是json格式)。
<i class="label2">ajax中添加加载动画</i>使用jquery的Ajax是在beforeSend:function(){}中添加动画，在complete:function(){}中取消加载动画。在原生js的ajax中也可以自行在onreadystatechange = function(){}前后添加两个函数也可实现。但beforeSend函数只在第一次请求时触发,所以显示加载动画最好是在调用ajax之前,complete中隐藏加载动画可以加一个延时取消这样交互效果更好。
<i class="label1">ajax接口的处理</i>做项目中在使用到ajax或其它方式对接数据时对接的接口需要用"http://"+获取的本地域名+接口来充当请求数据的接口，这样更换域名后也不会出错。(也可直接写域名后的接口名，在运行时会被自动添加上当前域名)。

ajax跨域问题：https://www.cnblogs.com/lxwphp/p/8080188.html
https://blog.csdn.net/WRian_Ban/article/details/70257261
https://blog.csdn.net/xr510002594/article/details/81409426
https://blog.csdn.net/mooncom/article/details/52402836
https://blog.csdn.net/codingnoob/article/details/80879208
#### 17、js数据类型操作：
javascript数据类型包括：数值、字符串、布尔、数组(列表)、对象(字典)，5种。
<i class="label1">数值</i>parseInt("fjdk889") //转为整型889,剔除字符串。parseFloat()//转为float型。
<i class="label1">字符串操作</i>x.toString()//转为字符串。x.replace(/target/,'')//替换。x.concat(“a”,”b”)//可与x连接多个字符串。
#### 18、js对象与json格式互转：
```
var obj = {name:"wcs",id:21}
obj = JSON.stringify(obj);// {"name":"wcs","id":21}
var json = {"name":"mx","id":23}
// eval()方法和JSON.parse()方法都可将json转为js对象，推荐用后一种
json1 = eval("("+ josn +")");//{name:"mx",id:23}
json2 = JSON.parse(json);
```
若是使用动态的方法将js对象转为json格式的话对象中的数值型会变成字符串，需要先用parseint()方法处理后再转换。
强大的eval()方法：
```
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
```
// 页面a：
var a = 55; // 页面a的对象
el.onclick=function(){window.open("b.html");}//打开一个新窗口
// 页面b:
console.log(window.opener.a);//window.opener会将前一个页面的所有对象封装为
//一个对象的形式，b页面可以使用，但对用户体验不好。    

```
#### 20、requestAnimationFrame()//动画制作专用
```
function play(){
console.log(a);
window.requestAnimationFrame(play);
}
window.requestAnimationFrame(play);//开始第一帧
cancelAnimationFrame()//方法取消动画。
```
#### 190、移动端手指事件:
需要使用事件绑定函数：addEventListener()或on()；
touchstart:手指触摸屏幕;addEventListener('touchstart',function(){})
touchmove:手指在屏幕上移动
touchend:手指离开屏幕
event.preventDefault():阻止默认行为；
event.stopPropagation():阻止冒泡；
event.touches[0].pageX,event.touches[0].pageY//手指坐标，touchend事件中不能用
event.changedTouches[0].pageX,event.changedTouches[0].pageY;//都可用
支持多指触摸事件？？？
(手机上涉及到手指移动事件再用移动端手指事件，其余事件就使用pc端的吧)
并不能完美的控制元素滑动的位置(做滑动元素时还是多使用overflow:scroll属性做滑动，滑动结
束后改变scroll位置(若要平滑效果用动画的方法设置))。
添加手指事件的元素最好都添加颜色（即便是透明）遇到过这种情况。
参考地址：https://blog.csdn.net/qq_40238154/article/details/78724917
    https://www.cnblogs.com/yangmengsheng/p/5973487.html
#### 198、jquery中的ready()方法：
下载好资源后浏览器先对html文件从上往下进行解析,当遇到css样式表时先解析形成CSSOM,然后DOM和cssom形成一颗渲染树进行渲染(先摆放元素位置大小再加样式)
如果遇到同步js文件(为设置async的script标签)会先解析js文件即:阻断对html的解析.所以推荐奖css样式文件放在头部,js文件放在html尾部。
将引入js文件的位置放在头部时若js文件中获取html中DOM元素就会失败,解决方法：
在<script>标签中加上异步属性<script src='' async="async"></script>；
js文件中使用DOMContentLoaded事件：
```
document.addEventListener('DOMContentLoaded',function(){
document.getElementById("ele").style.color="red";
});// ie6,7中使用onreadystatechange事件
```
但window.onload事件会在DOMContentLoaded事件之后加载。而jquery中的ready()方法等三种起手式中都封装了上面的事件，所以引用了jquery之后再在头部中引入其他包含操作DOM元素的js文件也不会报错。将js文件引入位置放在文档尾部</html>内，推荐这么使用。
https://www.cnblogs.com/caizhenbo/p/6679478.html
https://developer.mozilla.org/zh-CN/docs/Web/Events/DOMContentLoaded
#### 200、js es6语法大全
```
let a = 10;//块级作用域let定义变量,只在定义的块或附近的块有用，如for循环中
let a = () => 1;
alert(a);// 报错 a已被清除。
const a = 20;//const定义常量，第一次赋值后不能被改变
/*箭头函数，this*/
let foo = () => 1;//建立一个名为foo的函数返回值1，传参数时就等号后就写括号，
// var f = (1,2) =>{};多个参数时的写法，单个参数可不写括号，箭头指向执行语句
()=>{};// 将无名函数作为一个参数时的写法
v => {this.a = 20};// 将一个有名函数作为参数传入时的写法。箭头函数中的this
//不是指向他的上一级而是指向它本身
/*面向对象*/
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
/*子类中需要先调用super()方法才能用this添加实例对象因为子类中没有this对象只能
/*继承父类中的*/
// 解构
var [a,b,c] = [1,2,3]//a=1,b=2,c=3;
var {a,b} = {a:1,b:2}//a=1,b=2;
for(var i of obj){console.log(i);}//for of方法与for in方法不同，for of是
//迭代对象，它循环中的of表示对象中的每一项。
// 模板字符串
var name = 'your name is' + f_name + l_name;
var name = 'your name is ${f_name} ${l_name}';// 变量写在${}中
//模块的使用
import {a,b} from 'pages/home'
import a from 'pages/home/index'
export default{
    a
}
```
es6的兼容性问题：https://www.cnblogs.com/chris-oil/p/5931180.html
https://juejin.im/post/5ca2e1935188254416288eb2
#### 201、Object方法集：
```
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
```
Object.defineProperty(obj,'name',{
    configurable:true,//表示能否通过delete删除此属性,默认为true
    writable:true,//表示能否修改此属性值，默认true
    enumerable:false,//表示该属性能否被for in等方法枚举，默认true
    value:"wcs"//直接为该属性赋值
});
```
在第三个参数中写以上属性都不能与get,set一起使用。
```
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
### 四、库、框架、工具
#### 1、gitHub的使用：
 进入gitHub官网先注册一个账号,进入菜鸟教程点击git本地命令工具下载链接下载
git Barsh安装成功后打开(是一个命令行工具),操作如下：
输入ssh-keygen -t rsa -C "1815161966@qq.com"回车会提示要在/c/Users/Administrator/.ssh/id_rsa生成秘钥，之后一直回车到生成为止,此时在该路径下找到id_rsa.pub文件用记事本打开复制里面的所有内容,再在gitHub官网用户设置中找到SSH和GPG项将复制内容粘到键文本域中(title随意),回到命令行工具输入SSH -T git@github.com若成功会有提示成功信息。
// 把本地项目上传到github：
在github上创建一个仓库(点击加号选择第一个New repository),复制第一项中的url地址,然后打开Git Bush进入一个想放项目的文件目录中使用cd进入(cd G:/web),使用语句：git clone https://github.com/master,之后会在该目录下生产一个与你的仓库名同名的一个文件夹,将代码文件复制到该文件夹中,然后命令进入该文件夹(cd GanMa)再输入git add .(把文件添加进来)再输入git commit -m"xiaoswuwei"读
入完文件后输入git push -u origin master（传入到仓库中）.使用git clone +地址，也能下载别人仓库中的文件。http://www.runoob.com/w3cnote/git-guide.html
团队协作：https://blog.csdn.net/carfge/article/details/79691360
各种场景的撤销命令：
git merge --abort //合并过程中的撤销合并
git reset --hard HEAD^ //回退到前一个版本 ^^回退两个  ~100回退多个
https://baijiahao.baidu.com/s?id=1609673670814569258&wfr=spider&for=pc
git pull  //从远程更新代码到本地
git remote //查看远程信息
git remote -v //查看远程库信息
git push origin second //将本地分支推送到远程，远程也创建这个分支(远程未存在该分支的
情况，否则就是普通的提交信息)
git checkout master  //切换分支
git checkout -b main //创建并切换本地分支
git checkout -b ben origin/wcs //创建本地分支并关联到远程指定分支。
git merge WCS//合并WCS分支到当前分支，再git push origin master//更新，git status查看
合并情况若合并发生冲突的话会提示冲突的文件，找到该文件并处理标记了冲突的地方然后
git add filename 然后git commit -m 'merge'即可
git checkout -b origin/second //拉取second分支下的代码到本地
git branch -D second //删除本地分支second
git branch -a //查看所有分支
git push origin --delete yc //删除远程分支
.gitignore文件忽略设置(任何时候更改忽略文件都会有效)从主目录开始算路径
index.html //忽略文件
/dist/   //忽略整个dist文件夹
front/dist/  //忽略front文件夹下的整个dist文件夹
front/index.html  //忽略front文件夹下的Index.html文件
#### 2、mpvue:
教程地址：http://mpvue.com/mpvue/#_2
vue-cli安装：https://blog.csdn.net/u011320770/article/details/81281193
安装好vue-cli后用命令来初始一个项目,因为需要安装很多的配置文件和依赖，分为初始化创建一个小程序和初始化创建一个网站,两种命令不一样，如下：
小程序:vue init mpvue/mp-vue-quickstart wxObject    [安装期间会询问appid的一些信息...]web:vue init webpack web  [安装期间也会询问一些问题，但没有appid询问]
src文件中修改代码就能自动修改两个端代码？https://segmentfault.com/a/1190000015545555    https://www.v2ex.com/t/448121
[一套同时开发H5和小程序的demo]https://gitee.com/shqjustin/mpvuedemo 【里面有相关博客】
<i class="label1">运行与打包命令</i>npm run dev,npm run devH5	npm run build,npm run buildH5
注意项：【这里写的是在上面demo中的注意项】
[样式]使用的布局样式要使用less语言(style标签中写上less),一些标签不支持转译如ul,li,h5...index.vue等项目页面中在template标签中必须用一个标签包含所有内容(template内只能有一个一级子元素);只能使用改变类名的办法控制元素,v-bind:style=‘obj’失效,使用v-bind:style="{ color:gre }",样式参数从data中获取；不要使用标签选择器,一些小程序中使用的标签也无法转译。选择器使用>时后面不能跟#
(小程序端不能编译),img标签设置mode属性‘widthFiex’(自适应高度),不然小程序端不能显示。[字体大小:小程序上的rem为屏幕宽度/20这与网站端不一样]https://blog.csdn.net/qq_31383345/article/details/52817807，
[img设置自加载高度:https://developers.weixin.qq.com/miniprogram/dev/component/image.html]
[less中文文档:所有css代码最后被放到一个css文件中，所以在布局是谨慎使用同名的东西最好指定其父级]https://www.html.cn/doc/less/features/#features-overview-feature-operations-
<i class="label1">小程序单位</i>使用rem做单位在微信开发者工具上显示效果与web端差不多，但在真机上其大小会有一些差距，在一些需要精准定位的元素上能看出差不多4px的差距，官方并没有给出解释，这些地方可以使用按比例计算后的px作为单位效果更好。
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
```
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
```
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
【组件的使用】https://blog.csdn.net/qq_35661041/article/details/81476606    https://www.cnblogs.com/yun1108/p/9755785.html
<i class="label1">子组件触发父组件事件</i>
```
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
```
router.beforeEach((to,name,next)=>{
    window.document.title = to.meta.title;
    next();
});
```
<i class="label1">小程序端转json为js对象</i>
```
res_= res_.replace(/\ufeff/g,"");
if(typeof res_=='string'){
  res_ = JSON.parse(res_);
}
```
<i class="label1">小程序图片选择</i>
```
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
```
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
```
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
**linux上nodejs的安装：**官网上下载nodejs的linux压缩包，解压进入，将node_v...包拿出来放到相放的位置并重命名，然后建立软链接`ln -s /home/wcs/software/nodejs/bin/npm /usr/local/bin/ `(usr/local/bin下的命令是可直接访问到的，不然要加入环境变量才行)再`ln -s /root/hone/wcs/software/bin/node /usr/local/bin/`#然后node -v 安装成功。
**配置淘宝安装源：**npm本身指定的安装源是外国的，下载时多数会比较慢，`npm config set registry https://registry.npm.taobao.org`
#### 4、postman的使用：
(百度搜索下载postman安装)输入框左边选择请求方式，输入框中输入请求接口，下方Params项中输入要传的键值和value值，键值和value值的输入不需用单引号或双引号不然会出错,若报错可以在body项中选择form-data然后输入Params项中的键值和value值再点Send.
#### 5、vuejs框架常用：
设计原理猜测:做过许多项目后会发现所有项目几乎都包括向页面元素放值，获取值
、从后台获取数据在界面循环生成元素加数值；页面上几乎都会用到鼠标事件和一些
简单的交互效果，所以将这些分类：js中的变量数值统一放在一个集data中，js中
用到的函数统一放在方法集method中，即使是事件涉及的函数也映射到这个方法集中
。为了配合前端框架bootstrap等的使用vue框架中对元素通过id、类名等的选种操作
支持比较弱，因为前端框架中一个元素往往要加多个类名，这不便于选中元素。
**数据、事件、属性绑定：**
```
<p v-html="info">//info可以是html代码
<input v-model="dat"/>//input专用绑定数据语法
<a v-bind:href="url v-on:click="get()"></a>//绑定属性，事件
```
**循环：**
```
<li v-for="i in is">
<h5>{{ i }}</h5>
<div v-if="i == 0" v-html="a">这是i</div>
<div v-else-if="i == 1" v-html="b">这是else</div>
<div v-else v-html="c"></div>
</li>
```
加了v-for属性的元素会根据目标对象循环当前元素,包括其内部的结构，若目标对象长度为0或不是数组，字典那么当前元素也会被清除(可在for循环中加if,else语句条件循环是否要插入的元素)使用vue封装的ajax：
要下载vue-resource.min.js，方法集中使用：
```
this.$http.get("url",dat).then(function(res){console.log(res.body);},
function(){alert('失败')}));

```
$http方法是已经被封装在method对象中的所以可以用this直接调用，第一个参数传入接口地址，第二个参数传入要传送的数据，取到的值被当做参数传入then()中then()中第二个函数参数是请求失败时调用的函数。但使用vue封装的ajax感觉很不容易将获取到的值赋值出去，所以推荐使用jquery的ajax和原生ajax。vue中的ajax返回的数据中封装了很多东西，有数据、头部、catch-control等的加密信息，使用res.body代表获取到的数据。可使用JSON.stringify(res)查看结构。
**方法集中改变数据集中变量：**
```
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
v.alter()直接调用，或原始中<p v-on:click="alter()"></p>，v-on绑定的事件是动态
绑定的所以使用v-for循环出来也能使用。
**样式绑定：**
```
<div v-bind:class="{a:isa,b:isb}"></div><!--isa为true时将类名a绑定-->
<p v-bind:class="[a,b]"></p>// 绑定多个类名
<a v-bind:style="styObj"></a>//styObj是js中定义好的变量，内嵌样式
<b v-bind:style="{ width: w + 'px',color: col }">

```
**自定义组件：**
```
Vue.component("wcs",{
    template:'<h1>{{ info }}</h1>',
    props:['info']
});// 页面中直接<wcs></wcs>即

```
可使用。原生js中用document.createElement("wcs")实现。
事件绑定中传入event参数：
```
<p v-on:click="get($event)"></p>
function get(e){
    // 使用此法来获取当前元素
    e.target.style.color = "red";//若绑定事件的元素中有多个子元素请用
//currentTarget,因为可能点Z中的是子元素，触发事件的却是因为事件冒泡
}

```
**$refs的使用**
一个vue内置的一个元素选择器，<p ref="aa"></p> ref标记元素，this.$refs.aa选中元素，如果绑定的是一个组件还可以继续this.$refs.aa.get()调起组件内的方法。
[阻止事件冒泡]v-on:click.stop='get()'
注：数据集data中的属性值之间在初始赋值时不能相互依赖，可用全局变量达到初始
依赖赋值。vuejs中并没有像jquery中那种文档加载完成后再加载js代码的处理，所以
外联js文件写到页面底部才行。el.getAttribute("v-bind:src")类型的属性。
**使用vue-cli来初始化一个vue项目：**
`npm install vue-cli -g`#全局安装vue-cli工具，安装后可以使用vue命令初始化项目。
<i class="label1">安装vue-cli后找不到vue命令问题</i>安装vue-cli后会在所的nodejs/bin下看到vue。(npm config list#可以查看这个文件的位置)。为这个vue建立一个软链接将其放到/usr/local/bin下，`sudo ln -s /home/wcs/software/nodejs/bin/vue /usr/local/bin/vue`
<i class="label1">初始化</i>`vue init webpack test `#初始化一个名为test的项目，之后会询问一些设置上的问题，具体查看这个地址：[vue-cli初始化项目学习地址。](https://www.cnblogs.com/saint258/p/9621161.html)
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
#### 7、微信公众号开发注意项：
先用超级管理员账号登录微信公众号平台，开发>开发者工具>微信开发者工具>绑定开发者(将自己的微信号绑定为开发者账号)。
开发>接口权限>网页服务>网页授权>修改下把目标网站域名添加为公众号授权网页(先上传那个txt文件到服务器项目根目录)。
然后按照微信公众号开放文档步骤获取用户信息，注意：url地址处理使用
encodeURIComponent(url)函数处理,这个url中不能加端口号，所以只能是刚才配置的授权网页域名。
https://www.jianshu.com/p/b7e2100b56e4
#### 8、【集成网易云信IM】
下载demo(下载后先npm i 安装必要插件)
在login.js文件中，先将对应的appkey换成自己的。然后在获取到登录界面输入的账号，密码后添加一个网络请求，向自己的服务器获取用户在本应用下(对应的appkey应用下)的im用户id和云信服务器反给后台的云信token,然后调用cookie.setCookie()按格式放入到cookie中。
每次更改调试需要先npm run dev打包再node server启动本地服务。
要放到服务器使用的话直接将打包后的dist文件夹、regist.html,login.html,index.html文件放到服务器即可，主入口是index.html文件，在自己的项目中直接访问该路径+路由，然后带上uid,yxtoken两个参数(在指定im页面获取参数调用setCookie()登录，不然会报错)。
https://www.jianshu.com/p/2a601fe11bf0
https://www.jianshu.com/p/d56de7ea9736
