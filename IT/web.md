# 一、HTML

## 1、svg：

### a、svg 标签使用

mind: svg 标签及 svg 元素动态添加均不会生效，只可做静态使用

```html
<!--viewbox属性控制视图区域-->
<!--xmlns：xlink表示前缀为xlink的元素应该由理解该规范的UA使用xlink规范来解释.xmlns定义了默认命名空间,因此不需要前缀,-->
<svg width="300" height="300" xmlns="http://www.w3.org/2000/svg" version="1.1" viewbox="0 0 300 300">

<!--rx，ry控制圆角-->
<rect x="" y="" width="" rx="10" ry="20" height="" style="fill:red;stroke-width:2;stroke:blue;">
    <!--***animate:动画，放在元素中，则改动画会执行此动画
    -from:开始位置；
    -to:结束位置；
    -begin:开始时间；
    -dur：持续时间；
    -fill:remove表示结束动画时，回到起始位置；
    -repeatCount:为执行的次数；
    -path：有path的话则直接按path路线移动；
	  -attributeName：指定在哪个属性上变化；
	  -attributeType: 使用xml还是css样式变化；
    -->
    <animate id="one" attributeName="cx" attributeType="XML" from="30" to="470" begin="0s" dur="5s" fill="remove" repeatCount="1" />
    <!--animation: 可多个组合使用的动画-->
    <animateMotion path="M10,50 q60,50 100,0 q60,-50 100,0" begin="one.end" dur="10s" repeatCount="indefinite"></animateMotion>
    <!--animationTransform:transform属性类动画，additive为sum时可组合使用-->
    <animateTransform attributeName="transform" attributeType="XML" type="scale" from="1" to="3" begin="0s" dur="10s" repeatCount="indefinite" additive="sum"/>
    <animateTransform attributeName="transform" attributeType="XML" type="rotate" from="0 30 20" to="360 30 20" begin="0s" dur="10s" fill="freeze" repeatCount="indefinite" additive="sum"></animateTransform>
</rect>
//rect标签绘制矩形，x,y为位置,fill,stroke等属性可写在style外。
<circle cx="" cy="" r=""><title>hover提示作用标签</title><desc>描述作用，不显示，相当于文字注释</desc></circle>
<ellipse cx="" cy="" rx="" ry=""/>绘制椭圆，cx,cy为位置，rx,ry为宽高。
<line x1="0" y1="0" x2="20" y2="20"/>绘制线条，x1,y1,x2,y2为起始及结尾坐标。
<polygon points="10,10 20,20 150,320"/>绘制多边形，points中没两个值是一对坐标。
<!--set: 为元素设置属性值，一般配合动画使用-->
<polyline points=""><set attributeName="fill" to="green"></set></polyline>绘制折线

<!--****绘制任意路径、形状****
  - d: 路径绘制，属性如下：
    M：移动至起始点，必须。L：直线结束点。H：从当前点画水平线。
    V:垂直线。C:三阶贝塞尔曲线。Q：二阶贝塞尔曲线。Z: 连接到起始点
  - stroke-dasharray: 50 20; 边的一个线段长，线段之间的距离；
  - stroke-dashoffset: 50; 指定dash模式到开始点的距离；
【可让二者值相同，实现绘制线条的动画效果】
-->
<path d="M10 5L100 15C19 60,50 99 C 20 20, 40 20, 50 10" style="stroke-dashoffset:330;stroke-dasharray:330;stroke:#000;"/>
<image xlink:href="firefox.jpg" x="0" y="0" height="50px" width="50px"/>
<g></g><!--其它元素可以放到里面，做一组使用，无其它实意-->
<!--用于定义模板，一些效果类的东西可以放到里面，其它标签用xlink引用-->
<defs>
    <!--定义一个形状的裁剪;使用：clip-path="url(#cut)"【显示的是裁剪部分】-->
    <clipPath id="cut">
      <rect x="0" y="0" width="200" height="100" />
    </clipPath>
    <!--遮罩：可结合简便做淡入淡出动画-->
    <mask id="Mask">
      <rect x="0" y="0" width="200" height="200" fill="url(#Gradient)"  />
    </mask>
    <path id="a1" d="M0 50 C150 150 100 -50 300 50" stroke="#000" fill="none"/>
    <!--linearGradient定义一组线性渐变，(x1,y1)和(x2,y2)两点构成的方向即是渐变的方向-->
    <linearGradient id="gradient" x1="0" y1="0" x2="0" y2="1">
        <stop offset="0%" stop-color="green" />
        <stop offset="100%" stop-color="red" />
    </linearGradient>
    <!--
      定义一组圆形渐变
      -cx,cy: 定义渐变中心位置
      -fx,fy: 定义渐变焦点
      -使用示例：<circle cx="170" cy="170" r="30" fill="url(#eye_ra)"></circle>
    -->
    <radialGradient id="eye_ra" cx="50%" cy="50%" r="50%" fx="50%" fy="50%">
        <stop offset="0%" style="stop-color: rgb(249, 11, 11)" />
        <stop offset="90%" style="stop-color: rgb(117, 19, 19)" />
        <stop offset="100%" style="stop-color: rgb(58, 9, 9)" />
    </radialGradient>
</defs>
<!--text用于在svg中放置文字，xlink:href为引用模式-->
<text x="10" y="15">
    <textPath xlink:href="#a1">在平坦的路上曲折前行</textPath>
</text>
<!--一系列坐标点时，每个坐标对应的1个字符-->
<text x="0,20,40,60,70" y="0,20,40,60,70">This is some SVG</text>
<!--foreignObject可用于放置html元素，
且显示其渲染效果，可利用其将dom转为图片
（不过图片需用base64数据）
背景图也需要转为base64数据，且用单引号，使用；
-->
<foreignObject><div class="aa" xmlns="http://www.w3.org/1999/svg">contend:声称</div><style>.aa{color:red;background:url('data:image/svg+..');}</style></foreignObject>

<!--强大特效，滤镜部分-->
<filter id="filter"><!--定义一组滤镜-->
<!--<feTurbulence/>滤镜：采用perlin算法（产生类似自然纹理）
    -baseFrequency:噪声基本频率参数（【0-1】频率越高噪声越密集【越扭曲】）；
    -numOctaves:倍频数量（只能为整数【1-3】，数值越大，噪声看起来越自然【颜色点越分散】），
    -seed:伪随机数生成的起始值（改变噪声形状和位置）
    -stitchTiles:定义噪声在边框外的行为表现；【no-Stitch(svg元素边界处不会平滑处理) / stitch(元素边界处会平滑处理)】
    -type:【turbulence(端流，混乱) / fractalNoise(分形噪声)】
-->
<feTurbulence type="fractalNoise" baseFrequency="0.015" numOctaves="4" />
<!--<feDisplacementMap/>滤镜：可让图形按R,G,B颜色通道进行位置的偏移；多和<feTurbulence/>一起使用
    -scale:控制偏移程度；
    -in:指输入，sourceGraphic表示原图像
    -in2:第二个输入，turbulence，表示原图像断流处理过后的图像
    -xChannelSelector:指定in2从哪个颜色通道在x轴移动in中的像素；
    -yChannelSelector:指定in2从哪个颜色通道在y轴移动in中的像素；
-->
<feDisplacementMap in="SourceGraphic" in2="turbulence" xChannelSelector="R" yChannelSelector="B" scale="170" />
<!--光源滤镜，有3种光源可选；上面的滤镜和光源滤镜使用会失效；
    -in:输入的初始图像
    -lighting-color:灯光的颜色
    -surfaceScale:值越大，灯光越亮
    -diffuseConstant:光点的大小
-->
<feDiffuseLighting in="SourceGraphic" lighting-color="red" surfaceScale="1" diffuseConstant="2">
    <!--fePointLight：点光源，x,y,z控制光源位置（z由低到高，光会逐渐变亮）-->
    <fePointLight x="150" y="60" z="20"/>
    <!--feDistantLight：环境光；azimuth为平行光角度；elevation为平行光的海拔-->
    <feDistantLight azimuth="240" elevation="20"/>
    <!--feSpotLight：聚光灯效果；x,y,z控制光源位置；pointsAtX/Y/Z为聚光灯照向的位置;limitingConeAngle是灯光范围角度-->
    <feSpotLight x="100" y="30" z="99" limitingConeAngle="20" pointsAtX="390" pointsAtY="80" pointsAtZ="0"/>
</feDiffuseLighting>
<!--高斯模糊滤镜：-in:输入的基础图像；-stdDeviation:控制模糊程度；-->
<feGaussianBlur in="sourceGraphic" stdDeviation="4" />
<!--该滤镜执行两个输入图像的智能像素组合-->
<feComposite/>
<!--图片滤镜
- externalResourcesRequired：表示当前文档中是否需要外部资源。默认值为假
-->
<feImage x="" y="" width="" height="" externalResourcesRequired ="" preserveAspectRatio="" xlink:href="http://cc.jpg"/>
<!--用于组合两个图像，mode为指定模式-->
<feBlend in="" in2="BackgroundImage" mode="screen"/>
<feMerge>
<!--feFlood: 生成一层连续的颜色，填充元素的过滤器基本区域-->
<feFlood width="" height="" x="" y="" flood-color="#fff" flood-opacity="0.7">
<feMorphology operator="erode" radius="1"/>
<!--对原图像进行偏移，多用于创建阴影-->
<feOffset in="blur" dx="4" dy="4" result="offsetBlur"/>
<!--也是一个光源滤镜-->
<feSpecularLighting in="offsetBlur" surfaceScale="5" specularConstant=".75" specularExponent="20" lighting-color="#bbbbbb" result="specOut">
  <fePointLight x="-5000" y="-10000" z="20000"/>
</feSpecularLighting>
<!--颜色变换过滤器
***作为一个线性变换，在输入的图像的颜色上进行变换操作****
- type: matrix，还有：saturate(饱和度)、hueRotate(色相旋转)
- values: 4x5维的矩阵数据，（这里是趟平传参）各列值分别是：r,g,b,a,偏移量；
    第一行控制“红色通道”，第二行控制“绿色通道”，第三行控制“蓝色通道”，最后一行为“透明通道”
-->
<feColorMatrix type="matrix" values="110 10 20 1 0
                                     210 12 21 0 1
                                     210 12 21 0 1
                                     210 12 21 0 0"/>
</filter>
<!--使用滤镜,指定滤镜元素id，css中也可以使用
.css{filter:url(#filter);font-size:14px;}
-->
<circle id="shape" cx="" cy="" r="" filter="url(#filter)"/>
<!--symbol: 定义一组模板元素，一般与use配合使用-->
<symbol id="symbol" width="10" height="20" viewBox="0 0 10 20">
    <circle id="shape2" cx="" cy="" r="" filter="url(#filter)"/>
</symbol>
<!--use元素，用于复用其它图形，且可以使用其它svg标签中的图形-->
<use xlink:href="#shape" x="50" y="50" />
<use xlink:href="#symbol" x="200" y="50" />

</svg>
```

[基础部分学习地址](http://www.mamicode.com/info-detail-1988813.html)

### b、svg 内联

css 的 background-img 的 url 可以显示链接图片和 base64 图片，将 svg 转为 base64 的也能在其中显示出来，部分版本较高的浏览器可以直接用 svg 代码，如下：
**svg 文件引入**：.svg 文件可直接使用==img 的 src==，或 background-img 引入使用；`<img src="./img/图标.svg"/>或.el{background:url('./img/cc.svg');}`;(兼容性未知)

```html
<style>
  /*这种内联的svg渲染几乎无延迟*/
  .aa {
    background: url('data:image/svg+xml;utf8,<svg version="1.1" viewBox="0 0 200 200" xmlns="http://www.w3.org/2000/svg" version="1.1">...');
  }

  /*ie和一些浏览器中不能显示出来，但可以使用
-------js的encodeURIComponent()方法将其转码后使用,注意需要xmlns属性：
*/
  .bb {
    background: url("data:image/svg+xml,%3Csvg%...") no-repeat center;
  }
  svg {
    fill: currentColor;
  }
</style>
<script>
  // svg的fill设置为“currentColor”，其内部的元素“fill”的颜色可以跟随外层html元素的color变化；
  var svg =
    '<svg fill="currentColor" width="300" height="300" xmlns="http://www.w3.org/2000/svg" version="1.1">..</svg>';
  console.log(encodeURIComponent(svg));
</script>
```

注：利用 svg 的`viewBox`属性和其内部图形比例来控制它们；

### c、svg 将 dom 转图片

```js
function dom2svgImage(dom) {
  if (!(dom instanceof Object)) return;

  var cloneDom = dom.cloneNode(true);
  var SVG =
    '<svg xmlns="http://www.w3.org/2000/svg" version="1.1" width=">' +
    dom.offsetWidth +
    '" height="' +
    dom.offsetHeight +
    '">';
  var FOREG_PRE = '<foreignObject x="0" y="0" width="100%" height="100%">';
  var FOREG_END = "</foreignObject></svg>";
  // TODO:查询EL中的所有图片，转为base64表示;更完美的情况需要读取每个元素的样式，将他们都写到内嵌或style中
  //cloneDom.setAttribute('xmlns','http://www.w3.org/2000/xhtml');
  // 拼接为完整的svg；new XMLSerializer().serializeToString(cloneDom)将元素序列化；
  var res =
    SVG +
    FOREG_PRE +
    new XMLSerializer().serializeToString(cloneDom) +
    FOREG_END;
  // FIXME:注意处理一些特殊符号
  res = res.replace(/\n/g, "").replace(/\t/g, ""); //.replace(/#/g,'%23')
  // 转为img可使用形式
  var svgImg = "data:image/svg+xml," + encodeURIComponent(res);

  return svgImg;
}
var tt = dom2svgImage(document.getElementById("www"));
// TODO:将数据写入图片；可再将此图片用canvas转为base64，然后下载至本地；
document.getElementById("img").src = tt;
```

**注**：本地路径的图片是无法显示出来的，可以使用内联的图片数据，或者使用 http：开头的网络图；

### d、vue 项目中使用 svgIcon

1. 写一个公共组件放置引用 svg 图标：

```html
<template>
  <div
    v-if="isExternal"
    :style="styleExternalIcon"
    class="svg-external-icon svg-icon"
    v-on="$listeners"
  ></div>
  <svg v-else :class="svgClass" aria-hidden="true" v-on="$listeners">
    <use :xlink:href="iconName"></use>
  </svg>
</template>
```
### e、动态添加svg元素

SVG是基于XML格式定义图像的一种技术，因此创建节点的时候，需要指定命名空间（Namespace），也就是用createElementNS来代替createElement创建节点
```js
function makeSVG(tag, attrs) {
    const ns = 'http://www.w3.org/2000/svg';

    let el= document.createElementNS(ns, tag);
    if (tag==='svg'){
        el.setAttribute('xmlns:xlink', 'http://www.w3.org/1999/xlink');
    }
    for (let k in attrs) {
        if (k === 'xlink:href') {
            el.setAttributeNS('http://www.w3.org/1999/xlink', k, attrs[k]);
        } else {
            el.setAttribute(k, attrs[k]);
        }
    }
    return el;
}

window.addEventListener('load', function(){
    let svg = makeSVG('svg');
    let g = makeSVG('g');
    let rect = makeSVG('rect',{x:'0',y:'0',width:'20',height:'20',fill:'blue'});
    
    g.appendChild(rect);
    svg.appendChild(g);
    document.body.appendChild(svg);
});
```

2. js 文件中用 require.context()返回所有 svg 文件

```js
/**svg文件示例：code.svg
<?xml version="1.0" standalone="no"?>
<!DOCTYPE svg PUBLIC "-//W3C//DTD SVG 1.1//EN" "http://www.w3.org/Graphics/SVG/1.1/DTD/svg11.dtd">
<svg class="icon" xmlns="..."><defs><style type="text/css"></style></defs>
<path d="..."/>
</svg>
*/
import Vue from "vue";
import SvgIcon from "@cmp/private/SvgIcon"; // svg component
// register globally
Vue.component("svg-icon", SvgIcon);

const req = require.context("./svg", false, /\.svg$/); //返回一个webpack环境上下文（函数），包含文件id，keys等属性。
const requireAll = (requireContext) =>
  requireContext.keys().map(requireContext);
requireAll(req); //全部遍历出来。
```

3. 入口引入，并在 webpack 中使用`svg-sprite-loader`，然后配置，处理这些 svg 文件。

## 2、页面渲染过程：

- 先向服务端请求 html 网页。对 html 内容由上至下进行扫描，然后从头加载。
- 由上至下将内容构建 DOM 树和 CSSOM 树。
- 如果中途遇到 css 请求资源的加载会先请求 css 资源，然后加入到 cssom 树的构建中。
- 若中途遇到 js，会先阻塞 DOM 树，因为 js 可以操作 DOM。
- 两颗树构建完成之后会构建渲染树，由 cssom 树和 dom 树合并而成。
- [参考学习地址。](https://www.cnblogs.com/chenyoumei/p/9156849.html)

**页面的重绘与重排**（回流）：元素颜色的改变、css3 的一些变换等会引起页面的重绘，不过重绘速度非常快。而元素大小、display、position、float、overflow，js 的 resize 等会导致对页面的重新布局，即重排（也称回流）。无论是渲染树构建过程和渲染完毕后。回流比重绘需要的时间多得多，**所以应该尽量避免重排**。

## 3、第三方资源的加载：

很多加载资源的标签：iframe,video,audio,img,script,link 等是用 src 属性或是用 href 属性，一些标签不能跨域加载资源多数标签允许跨域加载资源。除了 link 和 script 外其它标签几乎都有 onload 事件和 onerror 事件可在元素上添加这两个事件做加载成功和加载失败后的处理。js 代码中的函数块语句需要达到相应的条件才能触发（body，head 中添加的 onload 和`<script></script>`中的 window.onload=“”除外)就算是 onmouseout 指定的函数也不行，因为它运行的前提就是有 onmouseover 被触发。
**link 标签**：

```html
<link href="http://a...pp.jpg" rel="prefetch" /><!--prefetch表示预加载-->
<link href="http://a...pp.css" rel="stylesheet" /><!--导入css-->
```

**外部资源引入标签**：
`<embed></embed>、<iframe></iframe>、<object></object>`
`<embed type="image/svg+xml" codebase="http:"></embed>`标签是 H5 新标签所有主流浏览器都支持，codebase 属性中写资源路径,可以引入脚本;类似 iframe 标签用于引入外资源(`<iframe>`标签只在大部分浏览器可用),但规范的 xhtml 和 html 中不支持`<embed>`标签.`<object data="rect.svg" type="image/svg+xml" codebase="http">`
`</object>`标签是 H4 的新标签，浏览器支持性差，但不能引入脚本.(引入的文件中的 js 对象和本页的 js 对象是不能共用的,且在引入的文件中获取的 url 也不是该页的)
**引入页面中刷新父页面更改浏览器 url**：
在`<iframe><embed><object>`标签中若是有用到跳转页面使用 window.location.href 或 window.open()或 a 标签中的跳转，页面跳转后还是只是显示在\<iframe>...这些标签之中
但使用 window.parent.frames.location.href = ""能让上一个页面跳转或直接`window.parent.location.href,window.top.location.href`让最外层的页面跳转，
a 标签中的跳转可用 target="parent"和 target="top"来实现。获取前一页 url：document.referrer;//包括传参也会获取到
**iframe 属性：**[参考地址](https://www.cnblogs.com/hzb462606/p/11394683.html)

```html
<iframe frameborder="0" sandbox=""></iframe>
<!--sandbox:
allow-same-origin：允许 iframe 内容被视为与包含文档有相同的来源；
allow-top-navigation：允许 iframe 内容从包含文档导航（加载）内容；
allow-forms：允许表单提交；
allow-scripts：允许脚本执行；
-->
```

## 4、canvas:

### a、基础图形绘制

```js
//`<canvas width="500" height="500"></canvas>`
var ctx = canvas.getContext("2d"); //获取2d对象

ctx.fillStyle = "blue"; //填充颜色需要放在绘制形状前
ctx.fillRect(x, y, width, height); //矩形填充颜色...
ctx.clearRect(x, y, width, height); //矩形清除图像像素
ctx.strokeRect(x, y, width, height); //绘制一个矩形框
ctx.fillText("str", x, y); //填充文字时不能填充其它且不能绘制形状。
ctx.font = "20px Arial"; //定义字体大小及类型。
ctx.textAlign = "center"; //left,start,right,end

ctx.beginPath(); //绘制路径，不规则图圆时先调用
ctx.lineWidth = 3; //线框
ctx.filter = "blur(15px)"; //模糊滤镜。
ctx.lineCap = "butt"; //线头样式,round:圆形头、square:方形头。
ctx.setLineDash([2, 5, 20, 30]); //设置为虚线，断点距头位置。
ctx.lineDashOffset = 10; //设置虚线起始偏离起始点距离。
```

### b、效果绘制

```js
//-----HTMLCanvasElement//表示页面内所有canvas元素，其余元素也有此类似对象。
HTMLCanvasElement.toDataURL()//方法将画布转化为base64图片格式。
HTMLCanvasElement.toBlob()//方法将画布转化为Blob对象。

a = ctx.createLinearGradient(0,0,300,0);//创建一个线性渐变，参数为区域
a.addColorStop(0,"red");//渐变a中添加位置,颜色
b=ctx.createRadialGradient(x0,y0,r0,x1,y1,r1)//中心渐变，两个圆中间的区域
patt=ctx.createPattern(ct1,null)//创建一个填充块，参数1是另一个canvas对象
//可将canvas对象ct1填充到canvas对象ctx中。
ctx.shadowBlur=20//阴影模糊程度
ctx.shadowColor="red"//阴影颜色
ctx.shadowOffsetX=2,ctx.shadowOffsetY=3//阴影偏移
ctx.strokeStyle="orange"//设置边框颜色
//坐标若超出canva画布大小则全部都不能绘制出来
ctx.quadraticCurveTo(10,10,20,20)//二次贝塞尔曲线，中转点，结束点
ctx.bezierCurveTo()//三次贝塞尔曲线
`ctx.arc(x,y,r,stAngle,Math.PI*2)`//绘制圆,控制第5个参数大小控制弧长。
ctx.ellipse(x,y,rx,ry,Math.PI/4)//绘制椭圆
//画圆，椭圆前定义lineWidth值填充strokeStyle值可画出圆环效果。
ctx.clip()//裁剪，使用之前先绘制一个路径区域再调用,裁剪掉区域外的东西
ctx.stroke()//绘制所描绘的路径
ctx.translate(10,10)//画布圆心位置移动,ctx.scale(0.1,0.1)//缩放,
ctx.rotate(Math.PI*30/180)//旋转,(在绘制时若多个变换一起使用需要先使用
translate()//变换否则出现的位置与设计的不一致)
ctx.globalAlpha=0.2;//设置画布全局透明度
ctx.save()//保存当前画布状态到栈空间，restore()方法依次取出。需要配合使用
save()方法放绘制的开头，restore(）方法放绘制的结尾。
```

ctx.globalCompositeOperation=

"source-over"//图形重叠处理，source-in:重叠部分绘制，source-out:重叠位置不绘制；

source-atop:重叠处类似遮罩的绘制、lighter:颜色叠加效果、copy:只显示新内容；

xor:互相重叠部分为透明、multiply:顶层像素与底层像素相乘，一般得到黑暗图形、screen:重叠处像素反转、overlay:multiply 与 screen 叠加效果、darken:变暗
lighten:叠加部分变量、color-dodge:底层像素值除顶层像素值、color-burn:颜色加深。底部图层的色值除以顶部图层色值，得到的结果再反相；

hard-light:重叠处强光、soft-light:柔光......

### c、图片绘制

**mind**：注意获取图片数据时会出现跨域问题，可以使用 vue 运行的本地环境中，使用`require()`获取本地图片（因为其获取到的直接是 base64 数据）

```js
img=new Image()//继承Image类，img.src="mv.jpg"//获取图片文件像素数据。
img.width、img.height、img.data//直接获取该图片的宽高，像素数据。
ctx.drawImage(img,dx,dy,width,height)//绘制图片,img可以是图片、svg、canvas
//图形对象(不写width和height时自己会计算宽高);该方法写在img.onload=function(){}内。
imgdata=ctx.createImageData(300,100)//创建一个全0像素矩阵,可操控每个点值
//使用imgdata.data[0]=230;这种形式改变。
dat=ctx.getImageData(x,y,width,height);//dat.data获取像素矩阵，
//getImageData()方法能获取canvas上任意图形的像素数据。
img.src =canvas.toDataURL(type,scl);//将整个canvas上的像素数据转换为
//base64格式,能直接显示到img中,type有图片格式,有:image/png(默认),
//image/jpeg,image/webp;scl为缩放值(更改图片质量0~1)
ctx.putImageData(imgdata,x,y)//重绘imgdata
/**********若img是网络图，可能会有跨域问题，使用img.crossOrigin='anonymous'，且服务端配置响应请求头可解决********/
/**********若img中的是base64，或xml,svg数据则不会有跨域问题************/
/**********也可使用ajax请求来获取图片，可得到图片数据************/
```

**获取图片色值**：利用 getImageData()得到的是 rgba 数据。

```js
function getColor(x, y) {
  var canvas = document.createElement("canvas");
  var ctx = canvas.getContext("2d");
  var img = new Image();

  img.src = require("@/assets/images/sj13.jpg");
  img.onload = function () {
    ctx.drawImage(img, 0, 0, img.width, img.height);
    var mgd = ctx.getImageData(0, 0, img.width, img.height);
    var dt = mgd.data;
    /*getImageData()得到的数据是一维数组，没相邻的4个值是一个点的rgba值，点是从左道右，从上到下排列的*/
    //像素开始位置：(W*y + x)*4
    var position = (img.width * Number(y) + Number(x)) * 4;

    console.info(dt[position], dt[position + 1], dt[position + 2]);
  };
}
```

**转灰度与反向**

```js
var img = new Image();
img.crossOrigin = 'anonymous';
img.src = './assets/rhino.jpg';

var canvas = document.getElementById('canvas');
var ctx = canvas.getContext('2d');

img.onload = function() {
    ctx.drawImage(img, 0, 0);
};
// 原图
var original = function() {
    ctx.drawImage(img, 0, 0);
};
// 反向色处理函数
var invert = function() {
    ctx.drawImage(img, 0, 0);
    const imageData = ctx.getImageData(0, 0, canvas.width, canvas.height);
    const data = imageData.data;
    // 每个通道取反向色值即可
    for (var i = 0; i < data.length; i += 4) {
        data[i]     = 255 - data[i];     // red
        data[i + 1] = 255 - data[i + 1]; // green
        data[i + 2] = 255 - data[i + 2]; // blue
    }
    ctx.putImageData(imageData, 0, 0);
};
// 置灰处理
var grayscale = function() {
    ctx.drawImage(img, 0, 0);
    const imageData = ctx.getImageData(0, 0, canvas.width, canvas.height);
    const data = imageData.data;
    // 每个像素点取均值
    for (var i = 0; i < data.length; i += 4) {
        var avg = (data[i] + data[i + 1] + data[i + 2]) / 3;
        data[i]     = avg; // red
        data[i + 1] = avg; // green
        data[i + 2] = avg; // blue
    }
    ctx.putImageData(imageData, 0, 0);
};

const inputs = document.querySelectorAll('[name=color]');
for (const input of inputs) {
    input.addEventListener("change", function(evt) {
        switch (evt.target.value) {
            case "inverted":
                return invert();
            case "grayscale":
                return grayscale();
            default:
                return original();
        }
    });
}
```

### d、保存和恢复
- save 和 restore 方法是用来保存和恢复 canvas 状态的，都没有参数。Canvas 的状态就是当前画面应用的所有样式和变形的一个快照。
- 你可以调用任意多次 save方法。每一次调用 restore 方法，上一个保存的状态就从栈中弹出，所有设定都恢复。
(利用 globalCompositeOperation 中的 copy 属性可以实现图形的位移、旋转)
(如果要用一个 2d 对象绘制多个图形且让其能产生动画效果那么需要在每个绘制图形前都加一个 globalCompositeOperation,属性值不为 copy 即可)

```js
var cn = document.getElementById("canvas");
function play() {
  var cv = cn.getContext("2d");
  // 以下两个图形用一个2d对象绘制。
  cv.globalCompositeOperation = "copy";
  cv.beginPath();
  cv.moveTo(10, 20);
  cv.lineTo(150, 230);
  cv.stroke();
  // 绘制另一个图形中间添加globalCompositeOperation属性
  cv.globalCompositeOperation = "source-over";
  //cv.save();若只想用transform中的方法产生动画在这里加上save()末尾用
  //restore()即可产生想要的结果。
  cv.beginPath();
  cv.moveTo(50, 200);
  cv.lineTo(310, 430);
  cv.stroke();
  cv.restore();
  // 使用这种模式，以上值处改为动态值即可产生动画
  requestAnimationFrame(play);
}
```

用 for 循环绘制多个图形：

```js
var can = document.getElementById("can");
var ttx = can.getContext("2d");
for (var i = 0; i < 3; i++) {
  ttx.globalCompositeOperation = "source-over";
  ttx.fillStyle = "blue";
  ttx.fillRect(0, i * 150, 300, 150);
  ttx.fill();
}
```

只刷新一个画笔的图形：

```js
var can = document.getElementById("can");
var ctx1 = can.getContext("2d");
var ctx2 = can.getContext("2d");
// 一个画布上有两个画笔
ctx1.fillStyle = "blue";
ctx1.fillRect(0, 0, 50, 100);
ctx1.fill();
ctx2.fillStyle = "red";
ctx2.fillRect(200, 30, 150, 90);
ctx2.fill();
window.onkeydown = function () {
  //只想改变一个画笔的图形时加上save()和restore()方法。就不影响其它图形了
  ctx2.save();
  ctx2.globalCompositeOperation = "source";
  ctx2.fillStyle = "red";
  ctx2.fillRect(200, 30, 200, 90);
  ctx2.fill();
  ctx2.restore();
};
```

第一个条语句用 globalCompositeOperation 可用 for 循环配合动态变量，绘制多个图形，放在动画代码中依然可用。
ctx.isPointInPath(x,y);ctx.isPointInStroke(x,y);//检测坐标点 x,y 是否在画笔对象 ctx 所绘制的图形中和边框上，canvas 上绘制的图形与 html 元素在生成的方式、操作上不一样所以 canvas 绘制的图形不能用 addEventLisener()来添加鼠标事件，所以可以借用以上这两个方法来添加鼠标事件效果。(不过这两个方法只支持使用 begInPath()方法绘制出来的图形对象。)

### e、动画


## 5、概念

**位图与矢量图**：位图又叫做点阵图，是一个个很小的颜色小方块组合在一起的图片。一个小方块代表 1px（像素）。矢量图是由一个个点链接在一起组成的，是根据几何特性来绘制的图像，和位图的分辨率是没有关系的。因此图片放大后也不会失真，不会出现位图的马赛克的样子，也就是说可以无限放大图片。

> 图片处理专项：(png 转为 jpg 后一般能缩小一半，但 png 色彩更丰富，且透明背景属性，所以项目中一般使用的是 png)
> jpg：全名是 JPEG，是数码相机的常用格式，特点呢就是色彩还原性好，天生适合风景照，可以在照片不明显失真的情况，大幅度降低体积。
> png：png 是最适合网络的图片，色彩丰富，png 不适用于颜色很少，或亮度差异十分明显的较简单的图片。

**各设备屏幕尺寸**：手机屏宽范围：300 – 768 px; 平板屏宽范围: 769 – 1199px;笔记本屏宽范围:1200 – 1400px; 台式，一体机屏宽范围:1401 – 1920px;广场电视机:1921 – 99999px。
**缓存**：缓存分为 CDN 缓存、数据库缓存、代理服务器缓存和浏览器缓存，浏览器的缓存问题主要指的是 http 缓存即协议层，H5 新增的 storage 缓存 和数据库缓存是应用层缓存。（协议层缓存可以分为强制缓存和对比缓存)。
强制缓存：缓存失效时才会去服务器获取最新资源的方式，就是强制缓存,协议层中可以使用字段 expires 和 cache-control。（暂未知）
对比缓存：先从缓存中获取对应的数据标识，然后向服务器发送请求,确认数据是否更新,如果更新则返回新数据和新缓存;反之返回 304 状态码（缓存可继续使用）浏览器行为引起的缓存变化：
(1)刷新网页：如果缓存没有失效浏览器会直接使用缓存；
(2)手动刷新（F5）：浏览器会认为缓存失效；
(3)强制刷新（ctrl+F5）：浏览器会直接忽略缓存；
**CDN**：Content Delivery Network，即内容分发网络。CDN 是构建在现有网络基础之上的智能虚拟网络，依靠部署在各地的边缘服务器，通过中心平台的负载均衡、内容分发、调度等功能模块，使用户就近获取所需内容，降低网络拥塞，提高用户访问响应速度和命中率。CDN 的关键技术主要有内容存储和分发技术。<b c=v>中小企业使用 CDN 一般是使用其它服务商提供的 CDN 服务，类似在域名解析处更改 DNS 地址即可。</b>
**OSS**：OSS 是一个分布式的对象存储服务，提供的是一个 Key-Value 对形式的对象存储服务。用户可以根据 Object 的名称（Key）唯一的获取该 Object 的内容。

- bucket：存储空间。同一个存储空间的内部是扁平的，没有文件系统的目录等概念，所有的对象都直接隶属于其对应的存储空间。存储空间的名称在 OSS 范围内必须是全局唯一的，一旦创建之后无法修改名称。
- 对象/文件：对象是 OSS 存储数据的基本单元，也被称为 OSS 的文件。对象由元信息（Object Meta），用户数据（Data）和文件名（Key）组成。对象由存储空间内部唯一的 Key 来标识。对象元信息是一个键值对，表示了对象的一些属性，比如最后修改时间、大小等信息，同时用户也可以在元信息中存储一些自定义的信息。
- 访问域名：Endpoint 表示 OSS 对外服务的访问域名。OSS 以 HTTP RESTful API 的形式对外提供服务，当访问不同的 Region 的时候，需要不同的域名。
- AccessKey：AccessKey，简称 AK，指的是访问身份验证中用到的 AccessKeyId 和 AccessKeySecret。OSS 通过使用 AccessKeyId 和 AccessKeySecret 对称加密的方法来验证某个请求的发送者身份。AccessKeyId 用于标识用户，AccessKeySecret 是用户用于加密签名字符串和 OSS 用来验证签名字符串的密钥。
- [学习地址。](http://www.360doc.com/content/18/0823/22/49604565_780716594.shtml)

## 6、web 中的安全措施：

1. **sql 注入**：通过输入框中输入一些 sql 的插入、删除等语句，在传到后台时被运行，然后操作数据库。防御：做一些正则匹配，替换输入中的特殊字符等，后台做一些站位等措施。
2. **XSS**： (Cross-Site Scripting)，跨站脚本攻击,因为缩写和 CSS 重叠，所以只能叫 XSS。跨站脚本攻击是指通过存在安全漏洞的 Web 网站注册用户的浏览器内运行非法的 HTML 标签或 JavaScript 进行的一种攻击。

- 可能造成以下影响：利用虚假输入表单骗取用户个人信息。利用脚本窃取用户的 Cookie 值，被害者在不知情的情况下，帮助攻击者发送恶意请求。显示伪造的文章或图片。
- 非持久型 XSS：（反射型 XSS ），有通过 url 传参的网页，攻击者可以直接通过 URL (类似：https://xxx.com/xxx?default=<script>alert(document.cookie)</script>) 注入可执行的脚本代码，如果目标网页获取该参数放于页面的话就会执行该脚本内容。不过一些浏览器如 Chrome 其内置了一些 XSS 过滤器，可以防止大部分反射型 XSS 攻击。

3. 持久型 XSS：（存储型 XSS）持久型 XSS 漏洞，一般存在于 Form 表单提交等交互功能，如文章留言，提交文本信息等，黑客利用的 XSS 漏洞，将脚本内容经正常功能提交进入数据库持久保存，当访问该文章时，前端页面获得后端从数据库中读出的内容放到页面上，就会将其渲染执行。

```js
//可以先对代码转码
console.info(
  btoa(`document.getElementById('tt').innerHTML="进来的人放弃一切希望!"`)
);
// 然后将转码的代码放到提交内容中。
<img src="static/a.jpg" onerror="atob(ZH...)" />; //这样放到页面中后就能执行onerror里的js代码，并绕过一部分检查。
```

- **防御**：Web 页面渲染的所有内容或者渲染的数据都必须来自于服务端。尽量不要从 URL，document.referrer，document.forms 等这种 DOM API 中获取数据直接渲染。尽量不要使用 eval, new Function()，document.write()，document.writeln()，window.setInterval()，innerHTML，document.createElement() 等可执行字符串的方法。<b c=gy>前后端都对输入做检查，检查是否有`<script>`等和一些特殊字符。对于混合开发类的 web 应用对放置页面的数据进行编码。</b>
- **禁止用户 js 代码中操作 DOM**：

```js
//将用户js代码放到匿名函数中任然无法禁止调用window下的document中。
(function (window, document) {
  "use strict";
  console.log(this, window, document); // {}, null, null
  const win = (function () {
    return this;
  })();
  console.log(win); // undefined
  setTimeout(function () {
    console.log(this); // Window
  });
}.call({}, null, null));
```

**使用 worker**：利用 worker 中不能操作 DOM 的特性，将用户代码放于 worker 中执行。
**使用 Shadow DOM**：[参考学习地址](https://zhuanlan.zhihu.com/p/355785418)

```js
(function () {
  const root = document.body.attachShadow({ mode: "closed" });

  let list;

  function init() {
    root.innerHTML = `
      <h1>Todo List</h1>
      <ul></ul>
    `;
    list = root.querySelector("ul");
  }

  function addTask(desc) {
    const task = document.createElement("li");
    task.textContent = desc;
    list.appendChild(task);
    return list.children.length - 1;
  }

  function removeTask(index) {
    const task = list.children[index];
    if (task) task.remove();
  }

  window.init = init;
  window.addTask = addTask;
  window.removeTask = removeTask;
})();

init();
addTask("task1");
```

4. CSRF：CSRF(Cross Site Request Forgery)，即跨站请求伪造，是一种常见的 Web 攻击，它利用用户已登录的身份，在用户毫不知情的情况下，以用户的名义完成非法操作。
   完成 CSRF 攻击必须要有三个条件：用户已经登录了站点 A，并在本地记录了 cookie。在用户没有登出站点 A 的情况下（也就是 cookie 生效的情况下），访问了恶意攻击者提供的引诱危险站点 B (B 站点要求访问站点 A)。站点 A 没有做任何 CSRF 防御。
   防御：防范 CSRF 攻击可以遵循以下几种规则：Get 请求不对数据进行修改。不让第三方网站访问到用户 Cookie。阻止第三方网站请求接口。请求时附带验证信息，比如验证码或者 Token
5. 点击劫持：是一种视觉欺骗的攻击手段。攻击者将需要攻击的网站通过 iframe 嵌套的方式嵌入自己的网页中，并将 iframe 设置为透明，在页面中透出一个按钮诱导用户点击。
   X-FRAME-OPTIONS 是一个 HTTP 响应头，在现代浏览器有一个很好的支持。这个 HTTP 响应头 就是为了防御用 iframe 嵌套的点击劫持攻击。
   该响应头有三个值可选，分别是：DENY，表示页面不允许通过 iframe 的方式展示。SAMEORIGIN，表示页面可以在相同域名下通过 iframe 的方式展示。ALLOW-FROM，表示页面可以在指定来源的 iframe 中展示。
   [web 端安全问题及应对方法。](https://www.cnblogs.com/pretty-sunshine/p/11442326.html)

## 7、HTML 规范&标签

`<!DOCTYPE>` 声明不是 HTML 标签；它是指示 web 浏览器关于页面使用哪个 HTML 版本进行编写的指令。在 HTML 4.01 中，<!DOCTYPE> 声明引用 DTD，因为 - HTML 4.01 基于 SGML。DTD 规定了标记语言的规则，这样浏览器才能正确地呈现内容。

- HTML5 不基于 SGML，所以不需要引用 DTD。[doctype 类型参考学习地址。](https://blog.csdn.net/Whisper_a/article/details/38706901)
- html5 中加了一些新的规范，如下示例：[H5 的一些新标签的使用学习地址。](https://www.cnblogs.com/nuanai/p/8856814.html)
- 带有 id 的元素其 id 名，在 js 中可直接使用（等同于选择了元素）
- 元素拥有 name 属性，且是`a,form,frame,img,iframe,..`等标签中的一个，则 js 中其 name 名可直接使用

```html
<! DOCTYPE html>
//声明使用H5规范来解析文档。
<html>
  // html5中标签名可以用大写，但推荐使用小写。不要省略html,head,body标签。
  <head>
    <link rel="stylesheet" type="text/css" href="./ff.css" />
    <!--带“defer”属性的script可以异步加载，页面渲染完成后执行，且能按顺序异步加载-->
    <script src="cc.js" defer></script>
    <!--带async的script也是异步加载，不过其加载完后会立即执行，然后继续渲染，且不能保证按顺序加载-->
    <script src="vv.js" async></script>
    <!--ES6 模块的写法，内部有export；与defer效果等同-->
    <script type="module" src="./foo.js"></script>
  </head>
  <body>
    // 如果父元素中的子元素个数很少时可以不用缩进。每个标签都必须关闭。
    <img src="" alt="HTML5" /> //alt能在图片加载失败时代替图片显示。 //
    一行代码尽量少于80个字符。少一些不必要的空行和缩进。
  </body>
</html>
```

**规范文档地址**：[HTML5 规范文档](https://html.spec.whatwg.org/)

**好用标签**：

### 1、meta 标签

```html
<meta name="keywords" content="标签,属性,seo优化" />
<meta
  http-equiv="Content-Type"
  content="text/html;charset=utf-8"
/><!--指定编码-->
<!--all：文件将被检索，且页面上的链接能够被查询。none时页面上的文件、连接将不能被查询。-->
<meta name="robots" content="All|None|Index|Noindex|Follow|Nofollow" />
<meta
  name="viewport"
  content="width=device-width, initial-scale=1.0"
/><!--viewport 是用户网页的可视区域-->
<meta
  http-equiv="X-UA-Compatible"
  content="chrome=1"
/><!--用以声明当前页面用chrome内核来渲染。-->
<meta
  name="renderer"
  content="webkit"
/><!--强制浏览器使用webkit内核渲染，当然前提是有该内核-->
<meta http-equiv="Cache-Control" content="cache" /><!--no-cache是不缓存该页面-->
<meta
  name="apple-mobile-web-app-capable"
  content="yes"
/><!--设置Web应用是否以全屏模式运行,content的默认值是no-->
```

注释常用语：`//TODO`(待实现的功能)、`//FIXME`(需要修正的功能)、`//XXX`(需要改进的功能)

### 2、**hr 标签**：

```html
<hr class="hr" data-content="分隔线" />
<!--文字会显示在正中-->
<style>
  .hr {
    border: 0;
    padding: 3px;
    /*/斜纹分隔线*/
    background: repeating-linear-gradient(
      135deg,
      #a2a9b6 0px,
      #a2a9b6 1px,
      transparent 1px,
      transparent 6px
    );
  }
  /*波浪线效果*/
  .hr::before {
    content: "\2000\2000";
    /* IE浏览器实线代替 */
    text-decoration: overline;
    /* 现代浏览器 */
    text-decoration: overline wavy;
  }
  .hr::after {
    /*attr()函数可让样式作用与元素的某个属性上，IE8 需要声明 !DOCTYPE 才可以支持 attr() 函数。*/
    content: attr(data-content); /*这里对文字内容进行装饰*/
    position: absolute;
    padding: 4px 1ch;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    color: transparent;
    border: 1px solid #d0d0d5;
  }
</style>
```

### 3、**marquee 标签**：

◎direction 表示滚动的方向，值可以是 left，right，up，down，默认为 left
◎behavior 表示滚动的方式，值可以是 scroll（连续滚动）slide（滑动一次）alternate（往返滚动）
◎loop 表示循环的次数，值是正整数，默认为无限循环
◎scrollamount 表示运动速度，值是正整数，默认为 6
◎scrolldelay 表示停顿时间，值是正整数，默认为 0，单位似乎是毫秒
◎align 表示元素的垂直对齐方式，值可以是 top，middle，bottom，默认为 middle
◎bgcolor 表示运动区域的背景色，值是 16 进制的 RGB 颜色，默认为白色
◎height、width 表示运动区域的高度和宽度，值是正整数（单位是像素）或百分数，默认 width=100% height 为标签内元素的高度
◎hspace、vspace 表示元素到区域边界的水平距离和垂直距离，值是正整数，单位是像素。
◎onmouseover=this.stop() onmouseout=this.start()表示当鼠标以上区域的时候滚动停止，当鼠标移开的时候又继续滚动。

### 4、**input 标签**：

```html
<input
  type="text"
  maxlength="5"
  pattern="[a-z]{5}"
/><!--maxlength限制最大输入长度，pattern可写正则匹配-->
<input
  type="text"
  readonly="readonly"
  value="不可编辑"
  autofocus="autofocus"
/><!--readonly让内容为只读状态。-->
<input type="number" min="5" max="10" /><!--限制输入范围-->
<!--表单和一些特殊类型的输入，可以用autocomplete属性-->
<form method="get" autocomplete="on">
  <input type="email" name="email" autocomplete="off" />
</form>
<!--list可以指定datalist的id，效果相当于select标签，不过鼠标触碰时才显示倒三角。-->
<input type="url" list="url_list" name="link" />
<datalist id="url_list">
  <option label="W3School" value="http://www.w3school.com.cn" />
  <option label="Google" value="http://www.google.com" />
  <option label="Microsoft" value="http://www.microsoft.com" />
</datalist>
<input type="file" multiple /><!--multiple可选多个-->
<input
  type="url"
  required="required"
/><!--required在没有输入，但触发submit时会自行提示-->
```

```html
<input type="radio" id="a" /> <label for="a">点我触发前面id为a的单选框</label>
<input type="checkbox" id="b" />
<label for="b">点我触发前面id为b的复选框</label> {
appearence:button;//设置单选框或复选框为正常状态。为none时无法使用 }
```

改变复选框状态：
`<input type="checkbox" checked='checked' value='1' id="ele"/>`
写上 checked 表示默认为选中这与 value 值无关，动态改变复选框或单选框状态需要用 js 控制：

```js
ele = document.getElementById("ele");
ele.checked = false; //false表示没选中，true改为选中。
ele.checked; //获取复选框状态返回true/false(布尔值，非字符串)。
```

**input 所有 type 类型**：
tel、number、email、text、radio、checkbox、image、date、color、button、submit、hidden、month、password、range、reset、search、time、url、week、file、month、datetime-local

### 5、**table 的使用**：

其直接属性控制的样式与 css 样式不同一。

```html
<table
  border="1"
  cellspacing="0"
  cellspadding="0"
  rules="rows"
  bordercolor="#e3e3e3"
>
  <!--
    - border: 为线宽;
    - cellspacing: 为格间距
    - rules：规定内侧边框的哪个部分是可见的。 【包括width、align等很多属性H5不再支持】
    - frame：规定外侧边框的哪个部分是可见的；    //border为0时这两个属性不生效。
    将table元素中的表格间距取消：border-collapse:collapse;
-->
  <thead>
    <tr>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <!--width可直接调整该列宽-->
    <tr>
      <td rowspan="2" colspan="3" width="150"></td>
    </tr>
  </tbody>
</table>
```

- [table 属性大全](https://www.w3school.com.cn/tags/tag_table.asp)

### 6、**script 标签**：

**阻塞行为**：<i c=gn>遇到脚本时，浏览器会先**下载**（非内嵌情况）脚本，然后执行。**执行结束后才会继续渲染下方元素**。</i>
**defer 属性**：带有 defer 属性的脚本表示内部没有 DOM 操作，可与其它资源`并行下载`，页面加载完成后（onload）才会执行这个脚本
推荐的无阻塞模式：使用一个下载文件的 js 脚本（下载其它 js 文件，动态生成 script 标签插入）并内嵌到页面底部。

```html
<script type="text/javascript">
  function loadScript(file) {}
</script>
<script type="text/javascript" src="acc.js"></script>
<script type="text/javascript" src="acb.js" defer></script>
```

### 7、img\a

```html
<!--
-alt：加载失败时显示的提示
-crossOrigin: 开启跨域；相应的服务端也需要配Access-Control,Allow-Credentials属性
    'anonymous': 使用此值时请求的header中会带上Origin属性；
    'use-credentials': 会带上cookie和一些其它认证信息；
-->
<img alt="加载失败" src="" crossorigin="" />
<!--只要设置了 ping 属性，用户点击此链接元素的时候，浏览器就会自动发送一个 POST 请求给 ping 属性值地址-->
<a href="" ping="https://www.xxx.cn/notify.php">发送</a>
```

### 8、MathML

HTML5 可以在文档中使用 MathML 元素，对应的标签是 `<math>...</math>`
MathML 是数学标记语言，是一种基于 XML（标准通用标记语言的子集）的标准，用来在互联网上书写数学符号和公式的置标语言。

```html
<math xmlns="http://www.w3.org/1998/Math/MathML">
  <mrow>
    <msup><mi>a</mi><mn>2</mn></msup>
    <mo>+</mo>
    <msup><mi>b</mi><mn>2</mn></msup>
    <mo>=</mo>
    <msup><mi>c</mi><mn>2</mn></msup>
  </mrow>
  <!--矩阵写法-->
  <mfenced open="[" close="]">
    <mtable>
      <mtr>
        <mtd><mi>x</mi></mtd>
        <mtd><mi>y</mi></mtd>
      </mtr>
      <mtr>
        <mtd><mi>z</mi></mtd>
        <mtd><mi>w</mi></mtd>
      </mtr>
    </mtable>
  </mfenced>
</math>
```

## 11、拖拽：

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

## 12、问题及解决：

1. 单个页面多场景问题：逻辑复杂的地方解耦开，分页处理。两个页面公共组件多考虑细分，逻辑部分用 mixins 抽离较合理。
2. 大页海报绘制问题：使用 canvas 绘制，计算数据使用 workers 计算，提高性能。
3. 登录页安全策略：使用 md5+非对称加密，使用安全键盘（前端绘制）。加密后的内容如果使用 url 传参的方式上送，会被浏览器转义部分内容，可以用 encodeURIcomponent()编码再传，java 用 URLDecode
4. **vuex 问题**：页面刷新会导致 vuex 数据丢失，解决的办法是存储时顺便存到缓存，在 vuex 文件中值的默认值，就使用从缓存恢复或请求的方法，这样其它页面不用做恢复操作。

```js
//===其它页面存储
window.sessionStorage.setItem("data",JSON.stringify(data));
//===vuex配置
var a = window.sessionStorage.getItem("data");
var state = {
    userInfo: JSON.parse(a);//解析使用
}
```

5. **props 问题**：props 中的值是单向的，子组件改变 props 中的值时会触发 error，可以将 props 中的值赋值到 data 中去（若是接口请求的数据在子组件 created 阶段），然后修改 data 中的该值。

```html
// 父组件
<child :cas="cases" />
<!--父组件获取值较慢，子组件created()中得到的是赋值前的状态。-->
<script>
  rpc(url, {}).then((res) => {
    this.cases = res.data;
    this.$refs.child.caval = this.cases; // 可以主动更新子组件中的值。
  });
</script>
// 子组件
<input v-model="caval" />
<script>
  export default {
    watch: {
      cas(nv) {
        if (this.cas.length === this.caval.length) {
          this.vaval = nv; //nv是深拷贝来的,注意条件判断，不然可能值接收不全或死循环。
        }
      },
    },
    created() {
      // 每次组件用完不销毁的话，只触发一次
      this.vaval = Object.create(this.cas);
    },
  };
</script>
```

6. vue 自定义组件最大复用问题：ui 样式一致，但内部逻辑变化差距过大的情况不再适合作为同一个组件，但 ui 样式可以抽离出来，其它部分不共用。

```html
/*=======将公共样式放在一个总类中。 .common-css{...} */
<template></template>
<script>
  export default {mixins:[mixin...]}//将一些公用的js方法以mixin注入，达到最大复用。
</script>
```

# 二、CSS

:::alert-info
简介：css(Cascading Style Sheets)层叠样式表，1996-12-17css1 诞生，2003 年 1 月 svg 被定为 w3c 规范，但当时的网页只是图文内容，css 更受偏爱。
:::

## 1、基础：

- **流**：俗称文档流，指的是 css 中的基本的定位和布局机制，css 中的布局规则。所以从上而下从左至右的描述只是 css 的一个默认流而已。
- **自适应布局**：对凡是具有自适应布局的一类统称，流体布局是自适应布局的一部分，但**流体布局**狭窄的多，<b class="violet">如 div+css 就是流布局，而 table 布局则不属于流布局，因为 css 真正是从 css2.1 开始的，IE8 开始支持它，在这之前 table 就已经存在，所以 ie8 前的浏览器多数使用 table 布局。</b>
- **元素的 4 个盒子**（盒模型）：content-box、border-box、padding-box(`padding`的百分比值是根据**元素宽来计算**的)、margin-box;
  元素的两个元素：每个标签有两个元素组成，内部元素控制宽，高、尺寸等；因此有“行内快”属性（`display:inline-block;`）
  Box-sizing:`border-box`;可以将宽度作用到哪一个盒子，无法作用到 margin-box；
- **未定义行为**：相同的 css 代码在不同浏览器可能效果不一样，甚至不显示，这并非 bug。因为各浏览器厂商去实现 css 时有一些自己的理解和定义，导致一些特殊情况未在其规则内导致的差异，繁杂多变的情况总有遗漏。<b class="gray">如伪类::activity 元素上同时绑定事件，事件中使用`event.preventDefault()`#这样能使拖动之类的效果更流畅，但火狐上不会显示 active 定义的行为。</b>

- FOUC(无样式内容闪烁)：Flash Of Unstyled Content ，`<style type="text/css" media="all">@import "../fouc.css";</style> `而引用 CSS 文件的@import 就是造成这个问题的罪魁祸首。IE 会先加载整个 HTML 文档的 DOM，然后再去导入外部的 CSS 文件，使用`<link/>`标签代替即可。<b c=gy>link 属于 HTML 标签，而@import 是 CSS 提供的、页面被加载的时，link 会同时被加载，而@import 引用的 CSS 会等到页面被加载完再加载。</b>
- **BFC**：（块级格式化上下文），是一个独立的渲染区域，让处于 BFC 内部的元素与外部的元素相互隔离，使内外元素的定位不会相互影响。
  > **BFC 的特性**：bfc 就是页面上的一个独立容器，容器里面的子元素不会影响外面元素。
  > **形成 BFC 的条件**
- `<html>`根元素；
  （1）float 的值不为 none；
  （2）overflow 的值为 auto、scroll 或 hidden；
  （3）display 的值为 table-cell、table-caption 和 inline-block 中的任何一个；
  （4）position 的值不为 relative 和 static。

- **css 选择器**：`div+p`#两个紧挨者的元素，`[attribute]`#选择带有 arrtibute 属性的元素。[attribute=value]选择等于指定值的。[attribute~=value]属性值中包含该值的。[attribute|=value]属性值中以该 value 开头的。`p:first-child`#选择 p 的父元素的第一个子元素(属于 p 元素)。p:last-child#选最后一个子元素。`p:nth-child(n)`#选择第 n 个子元素(属于 p 元素)。p:nth-last-child(2)#从最后子元素开始计数。[css 选择器全部](http://www.w3school.com.cn/cssref/css_selectors.asp)
  > **选择器优先级**：带!important>内嵌样式>id>类名==属性选择器>标签选择器>通配符(\*)>继承(继承父元素的属性)>浏览器默认属性。子选择器用 id 选择时比 id 选择器优先级高。
  > **选择器的解析**：解析选择器时是从右往左的（如使用`#div>.cc`时是先取.cc 再取#div 的顺序去构建树【更容易把公共样式放在一个节点】）少用一些子选择器。
- **鼠标样式**：cursor:pointer;//手指,提示可点击。hand//IE5 使用的手指样式、wait;//等待、help;//帮助、no-drop;//无法释放、text;//文字，暗示为文字内容、move;//提示可移动对象、crosshair;//十字准心、n-resize;//向上改变大小箭头、s-resize;//向下改变大小箭头、e-resize;//向右改变大小箭头、w-resize;//向左改变大小箭头、ne-resize;//向右上改变大小箭头、nw-resize;//向左上改变大小箭头、se-resize;//向右下改变大小箭头、not-allowed;//禁止、progress;//处理中、default;//提示可移动对象、url();//引入外部文件作为鼠标样式，文件格式必须为.cur 或.ani。
- **边框样式**：

```css
border:1px dotted red;
border-style:dotted:点线、dashed:虚线、double:双边框、groove:3d凹槽、ridge:菱形边框、insert:3d凹边、//outset:3d凸边。
border-width:think;/*think=1px,medium=3px,thick=4px*/
/*用border优雅的放大点击区域*/
border:10px solid transparent;
```

- 外边框：`outline:#00FF00 solid thick;`#样式，样式，宽度。

- textarea 标签：resize 属性的的各个取值:none：用户不能操纵机制调节元素的尺寸、both：用户可以调节元素的宽度和高度、horizontal：用户可以调节元素的宽度、vertical：让用户可调节元素的高度、
- **布局准则**：
  （1）无浮动：浮动容错性差；
  （2）无宽度：设置了宽度之后容器的“流动性”【width，padding 等尺寸上的自适应性】会丢失，元素宽发生改变后也会导致重绘；position:absolute;下的尺寸也具有流动性
  （3）无图片
- **流体布局下的宽度分离原则**：不用自己更多的计算，且更稳健;（也可以用`box-sizing:border-box;`把宽度作用到 border-box 上，但不大推荐如此）

```html
<div id="farther"><div id="son"></div></div>
<style>
  /*父元素控制宽，子元素控制其它盒子的尺寸，而不用都放在一个元素上写他们*/
  #farther {
    width: 100px;
  }
  #son {
    border: 2px solid black;
    padding: 20px;
  }
</style>
```

- **height:100%;**：父元素有具体高度时，所有定位，使用 height:100%；均可生效；
- **块级元素控制**：

```html
<div id="farther"><div id="son"></div></div>
<style>
  /*右对齐,不需要使用浮动*/
  .son {
    margin-left: auto;
  }
  /*左右居中*/
  .son {
    margin: 0 auto;
  }
  /*上下居中: 法一（但不能左右居中）*/
  .father {
    height: 200px;
    /*改变文档流方向*/
    writing-mode: vertical-lr;
  }
  .son {
    height: 100px;
    margin: auto;
  }
  /*上下，左右垂直居中*/
  .father {
    width: 300px;
    height: 150px;
    position: relative;
  }
  .son {
    position: absolute;
    width: 100px;
    height: 100px;
    margin: auto;
    top: 0;
    right: 0;
    bottom: 0;
    left: 0;
  }
  /*===============
浮动实现块级元素同行布局
（右侧或左侧不出现空白）
=================*/
  ul {
    margin-right: -20px;
  }
  ul > li {
    float: left;
    width: 100px;
    margin-right: 20px;
  }
</style>
```

- **滚动容器底部留白**：有滚动的使用一般底部使用一些留白，效果稍好；使用`margin-bottom:20px;`来实现（所有浏览器几乎可以）使用 padding 则会有兼容性问题；
- 平滑滚动：`scroll-behavior:smooth;`//发生滚动时更平滑(锚点跳转、改变 scrollTop 值)
- **滚动锚定**：滚动时或点击加载更多，新的内容导致滚动条位置变化，
  overflow-anchor:auto;状态会保持当前观看内容处于用户视线内，用户感觉不到滚动条位置变化。
  overflow-anchor:none;关闭时则会优先显示加载的内容。

- 滚动条样式：
```css
.scrollbar ::-webkit-scrollbar-thumb {
  /*滚动条里面小方块*/
  background: #c1c1c1;
  border-radius: 8px;
}
.scrollbar ::-webkit-scrollbar-track {
  /*滚动条里面轨道*/
  background: #f4f4f4;
  border-radius: 8px;
}
.scrollbar ::-webkit-scrollbar {
  /*滚动条整体样式*/
  width: 8px; /*高宽分别对应横竖滚动条的尺寸*/
  height: 8px;
}
```
- **input 选中后样式**：

```css
input:foucs {
  outline: none;
  border: 1px solid green;
}
/*修改placeholder字体样式*/
input::-webkit-input-placeholder {
  color: revert;
}
```

- **媒体查询器**：`@media only screen and (min-width: 300px) and (max-width: 768px) {}`

- **文本控制**：
  （1）调整字间距：letter-spacing:5px；
  （2）两端对齐：text-align：justify;和 text-align-last:justify;(一起使用)。最好将要对其子元素设置为 inline-block 元素。
  （3）**自动换行**：word-break：break-all 或 white—space：normal 来实现自动换行。
  （4）删除线：text-decoration:line-through;
  （5）**超出隐藏**：

```css
/*文字超出省略*/
el {
  overflow: hidden !important; /*!important的优先级大于内嵌样式*/
  text-overflow: ellipsis;
  white-space: nowrap; //3个属性一起设置可以让超出的文本变为省略号。
}

el {
  overflow: hidden;
  text-overflow: ellipsis;
  display: -webkit-box;
  -webkit-line-clamp: 2; //设置行数
  -webkit-box-orient: vertical;
}
/***********禁止点击**********/
 {
  pointer-events: none;
}
/*===============
    禁止选择文本
=================*/
 {
  -moz-user-select: none; /*火狐*/
  -webkit-user-select: none; /*webkit浏览器*/
  -ms-user-select: none; /*IE10*/
  -khtml-user-select: none; /*早期浏览器*/
  user-select: none;
}
/*===============
    禁止拖拽
=================*/
img {
  -webkit-user-drag: none;
}
/*背景图片设置*/
background: url(" ") no-repeat;
background-position: 50% 0; //图片居中
background-size: cover; //占满
/*===============
vertical-align使用【文字，图片居中】
vertical-align只作用于“内联”或table-cell的元素
<div class="box"><span class="children-word">我要居中</span><img class="children-img" src="../."/></div>
=================*/
.box {
  height: 30px;
}
/*根据情况，自行调整百分比值*/
.children-word {
  vertical-align: -25%;
}
.children-img {
  vertical-align: -40%;
}
```

- **引入外部文件夹中的字体**：
  [字体图标的使用]若是使用阿里图标库的话,头部 link 引入资源,元素中写上类名 iconfont,元素内容中写上对应的 unicode 编码。下载到本地使用的话引入下载的 iconfont.css 和 iconfont.js(那些 eot,svg,ttf...文件也要放到项目中)。[css 中自带的字体。](https://www.cnblogs.com/fozero/p/6087513.html)

```css
@font-face {
  font-family: sAir; // 自定义的字体名字
  src: url(../font/okj.otf); //一般是otf文件
}
div {
  font-family: "sAir";
} //使用字体
```

- marker 伪元素：

```css
ul::marker {
  /*marker用于定义ul，li中项目符号的颜色、大小甚至内容。普通元素也可以用：display:list-item;然后使用。*/
  content: "▶";
  color: blue;
  font-size: 14px;
}
```

- static 默认定位下元素**宽可以占满剩余空间**。

```html
<div class="main">
  <div class="left"></div>
  <div class="right"></div>
</div>
<style>
  .main {
    height: 100%;
  }
  .main > .left {
    height: 100%;
    left: 0;
    top: 0;
    width: 210px;
    background-color: red;
    position: fixed;
  }
  .main > .right {
    height: 100%;
    background: blue;
    margin-left: 210px; /*设置该属性，使用默认定位*/
  }
</style>
```

- **关键字**：几乎可用于所有属性，浏览器上

```css
div {
  color: initial; /*initial表示使用浏览器默认属性值*/
  line-height: inherit; /*inherit表示该属性值继承它的父元素的（非继承属性也可使用）*/
  all: revert; /*all表示所有属性，revert表示该属性值重置为浏览器默认*/
  font-size: unset; /*如果该属性是默认继承属性，该值等同于 inherit。如果该属性是非继承属性，该值等同于 initial*/
}
```

- **var 函数**：用于使用自定义的 css 变量。IE9.1 开始支持。

```css
/*:root中定义自己的遍历。*/
:root {
  /*必须要--开头*/
  --wcs-bg: red;
  --wcs-size: 80px;
}
/*var()中调用对应的变量值*/
.div {
  background-color: var(--wcs-bg);
}
```

- **展开/折叠动画**：展开折叠时一般要知道具体高才能设置 height 来完成过渡动画。这里使用 max-height 变化来绕开。

```css
p {
  max-height: 0;
}
p::hover {
  /*设置一个安全高度，设得太大，在收起时会有明显速度不统一的问题*/
  max-height: 100px;
}
```

## 1.1：无 js 的选项卡实现

```html
<div class="box">
  <div class="list"><input id="one" />1</div>
  <div class="list"><input id="two" />2</div>
  <div class="list"><input id="three" />3</div>
  <div class="list"><input id="four" />4</div>
</div>
<div class="link">
  <label class="click" for="one">1</label>
  <label class="click" for="two">2</label>
  <label class="click" for="three">3</label>
  <label class="click" for="four">4</label>
</div>
<style>
  .box {
    height: 10em;
    border: 1px solid #ddd;
    overflow: hidden;
  }
  .list {
    height: 100%;
    background: #ddd;
    position: relative;
  }
  .list > input {
    position: absolute;
    top: 0;
    height: 100%;
    width: 1px;
    border: 0;
    padding: 0;
    margin: 0;
    clip: rect(0 0 0 0);
  }
</style>
```

## 2、尺寸单位：

- **em**：是根据当前元素字体大小而变化的,列入当前元素 font-size:14px;width:10em,此时 width 为 140px(每 1em 为字体大小)。
- **rem**：是继承根部元素(html)的字体大小的,例:html{font-size:16px;}.div{width:10rem;}//width 为 160px。用以下代码修改根元素大小。

```js
function transfer(win, doc) {
  var W = win.innerWidth;
  var UIW = 750;
  var RATIO = 100; // 1rem = 100px

  if (W < 1000) {
    doc.documentElement.style.fontSize = W / (UIW / RATIO) + "px";
  }
}
window.onResize = transfer;
transfer();
```

- **vw**：视窗宽度，1vw 相对于视窗宽度的 1%。
- **vh**：视窗高度，1vh 相对于视窗高度的 1%。
- vmin 和 vmax：vw 和 vh 中选择最小/最大那个。

## 3、css3：

- css3 倒影：

```css
el {
  box-reflect: below 1px linear-gradient();
  /*box-reflect属性为元素添加倒影
    //效果，第一个值设置方向，第二个值为倒影与元素的距离，第三个值为线性渐变，将
    //渐变设为透明度逐渐增加的白色效果较好，做兼容处理时box-reflect前和渐变前
    //都加上前缀。
    */
}
```

- css3 剪切：

```css
el {
  clip-path: polygon(50% 0, 10px 100px, 150px 100px); //多边形剪切，点位置
  clip-path: circle(50% at 50% 50%); //圆形剪切,半径，圆心坐标
  clip-path: ellipse(30% 20% at 50% 50%); // 椭圆剪切，宽，高，圆心位置
  clip-path: react(); //矩形剪切，写入位置，宽高。
}

/*css3实现毛玻璃效果(高斯模糊)：*/
el {
  -webkit-filter: blur(10px);
  -moz-filter: blur(10px);
  -ms-filter: blur(10px);
  filter: blur(10px);
}
```

- css3 贝塞尔速度曲线：

```css
el {
  /*默认的贝塞尔速度曲线是从(0,0)到(1,1)的一条匀速直线，括号中的四个数值是.
    perspective-orign:50% 50%;//改变视角位置坐标
  //贝塞尔曲线中的两个点的位置，通过这两个点拉扯曲线，速度安装曲线弯曲度改变。*/
  transition: all 1s cubic-bezier(0.7, 0.1, 0.9, 1);
}
/***过渡transition:对svg,<path/>的d属性也可生效****/
path{
  /*<path d="M0 0Q40 20,100 80"/>*/
  transition: d 1s;
}
```

- 阴影：

```css
div {
  /*x轴偏移度，y轴偏移度，阴影模糊度，阴影范围*/
  box-shadow: 1px 2px 10px 5px black;
  /*常用写法*/
  box-shadow: 1px 2px 15px black;
  /*实现内边框原角*/
  box-shadow: 0 0 0 5px black;
  border-radius: 10px; /*可以作用在阴影上，结合实现边框效果*/
}
```
- 变换&过渡&动画：
```css
div{
  transition: height 2s;
  transform:translate(10px,20px);
  transform: rotate(30deg);
  transform: skew(30deg,20deg);
  -ms-transform:scale(2,3);
}
```
- **matrix()使用**：`transform:matrix(a,b,c,d,e,f);`,matrix()以上几个的综合，a,b,c,d,e,f都是数值；作用在元素的==每1个像素点上==
变换过程如下(用于2d变换)：结果第1行为变换后的**水平坐标**x，第2行值为变换后的**垂直坐标**y值
$$\left[\begin{matrix}a&c&e\\b&d&f\\0&0&1\end{matrix}\right]*\left[\begin{matrix}
  x \\ y \\ 1\end{matrix}\right]=\left[\begin{matrix}
    ax+cy+1 \\ bx+dy+f \\ 0+0+1\end{matrix}\right]
$$
==移动情况==：水平移动的话，只需修改e，f即可
```css
div{
  transform:matrix(1,0,0,1,x,y);
}
```
==缩放情况==：修改第a，d值即是缩放；
```css
div{
  transform:matrix(sx,0,0,sy,0,0);
}
```
- 动画：
```css
/******动画填充模式*****
none	默认值。动画在动画执行之前和之后不会应用任何样式到目标元素。
forwards	在动画结束后（由 animation-iteration-count 决定），动画将应用该属性值。
backwards	动画将应用在 animation-delay 定义期间启动动画的第一次迭代的关键帧中定义的属性值。这些都是 from 关键帧中的值（当 animation-direction 为 "normal" 或 "alternate" 时）或 to 关键帧中的值（当 animation-direction 为 "reverse" 或 "alternate-reverse" 时）。
both	动画遵循 forwards 和 backwards 的规则。也就是说，动画会在两个方向上扩展动画属性。

*/
div{
  animation: fadeShow 0.3s forwards;
}
```

- **图片遮罩**：mask-image 优化 png 图片加载。如果是不需要透明属性的 png 图片我们可以直接转为 jpg，但如果有透明要求转为 jpg 后就会透明部分变成白色。
所以使用 css 的 mask-image 属性有一张纯色 png 图(轮廓与原 png 一样，纯色填充后是以前的 1/100 大小)遮在 jpg 图上(png 转化后的)，这样使用 jpg 图片就能代替 png 了。

```css
img {
  // 不用担心兼容性问题。
  -webkit-mask-image: url(card-mask.png);
  mask-image: url(card-mask.png);
}
```

- **渐变**：

```css
i {
  /*第一个值为方向，可为：to right,to left,to top,to bottom,10deg*/
  /*默认为to top，使用角度时为顺时针旋转*/
  background: linear-gradient(
    70deg,
    #9b3675 15%,
    #1597bb 40%,
    #6155a6 90%,
    #364547 100%
  );
  /*shape: circle, ellipse
      size: farthest-cor,closest-side,closest-corner,fathest-side
      position: center,top,bottom
    */
  background: radial-gradient(shape size at position, color);
  background: radial-gradient(
    closest-side at 50% 60%,
    rgba(100, 90, 80, 0.2),
    transparent 60%
  );
  /********repeating-linear-gradient********/
  /*可利用此模板来绘制条纹背景*/
  background:repeating-linear-gradient(50deg,red 0px,red 10px,blue 10px blue 20px);
}
```

## 4、未知大小元素居中：

- 使用 table 布局：

```css
.parent1 {
  display: table; /*加将元素变为table元素性质*/
  height: 300px;
  width: 300px;
  background-color: #fd0c70;
}
.parent1 .child {
  display: table-cell; /*display: table-row=>相当于“tr”标签；display: table-cell=>相当于“td”标签*/
  vertical-align: middle;
  text-align: center;
  color: #fff;
  font-size: 16px;
}
```

- inline-block 使用 vertical-align:middle;属性。

```css
#tip {
  position: absolute;
  z-index: 100;
  top: 40%;
  left: 50%;
  width: 300px;
  margin-left: -150px;
  text-align: center;
  padding-top: 1px;
  > p {
    display: inline-block;
    position: relative;
    vertical-align: middle;
    padding: 8px 20px;
    color: white;
    background: rgba(0, 1, 2, 0.6);
    border-radius: 8px;
    font-size: 14px;
    text-align: center;
  }
}
```

- 借助 css3 属性

```css
.parent3 .child {
  position: absolute;
  top: 50%;
  left: 50%;
  color: #fff;
  transform: translate(-50%, -50%);
}
```

- 使用弹性布局的：justify-content:center;align-items:center;

## 5、弹性布局：

```less
.box {
  display: flex;
  display: -webkit-flex;
  flex-direction: row; //排列方向
  flex-wrap: wrap; //转行类型
  justify-content: space-between; //同一方向一根轴线时对其方式，space-evently:为所有间距等分
  // 多行时的对齐控制
  align-content: stretch; //同一方向多行元素时的对齐方式，属性值与justify-content一样。
  // 单行时的控制
  align-items: center; //元素垂直居中,控制的是另一个轴。stretch为占满高度。
}
.child {
  align-self: flex-end; // 其子元素对应align-item方向上的位置控制.
  order: 1; //定义子项目的所在顺序
  flex-basis: 500px; //定义了在分配多余空间之前，项目占据的主轴空间。若内部有内容则flex-basis不再生效。
  flex-grow: 2; //定义元素的放大比例
  flex-shrink: 0.5; //定义元素的缩小比例
  //flex:1;能让子元素自适应宽或高。
  flex: 0 1 auto; //flex-grow, flex-shrink 和 flex-basis的简写，默认值为0 1 auto。后两个属性可选。
}
```

[flex 布局学习地址。](https://www.runoob.com/w3cnote/flex-grammar.html)
**一排固定几个元素**：使用 justify-content:space-between 且给子元素宽度时，这时宽度不起用，需要加上：flex-direction: row;flex-wrap: wrap;这样每行就能像想象的个数显示。

## 6、栅栏布局：

:::alert-info
**简介**：栅栏布局也是 css3 的内容，是一种将元素分割为模块组合形式的布局方式。兼容性也还不错，ie9 中需要对父元素做清除浮动操作才能正常显示。
:::

```html
<div class="grid">
  <div><p>1</p></div>
  <div><p>2</p></div>
  <div><p>3</p></div>
</div>
<style lang="less">
  .grid {
    display: grid; /*/该box使用grid布局。*/
    grid-template-columns: 150px 1fr 2fr; /*设置每列的宽，fr表示当前列是前一列的倍数。也能用auto*/
    grid-template-rows: [r1] 100px [r2] 100px [r3] auto [r4]; /*[r1]是为该位置的网格线起名*/
    grid-gap: 20px 10px; /*行间距、列间距*/

    justify-items: start; /*各单元格内水平方向位置，end/center/stretch*/
    align-items: center; /*垂直方向，place-items:center end;是两个属性的合并*/

    justify-content: start; /*整个内容区域在容器里面的水平位置，center/end/stretch/space-around/space-between/space-evenly*/
    align-content: center; /*垂直方向，place-content是两者合并*/

    div:nth-child(5) {
      /*定义该子元素所占行、列数,span表示跨越*/
      grid-column: span 2;
      grid-row: span 2;
    }
    div:nth-child(1) {
      /*定义该项目各网格线位置，达到控制该元素位置及大小的目的。*/
      grid-column-start: 1; /*左网格线位置,也可以使用上面定义的网格线名代替数字*/
      grid-column-end: 3; /*右网格线位置*/
      grid-row-start: 2; /*上网格线位置*/
      grid-row-end: 4; /*下网格线位置*/
    }
  }
</style>
```

- [学习地址。](http://www.ruanyifeng.com/blog/2019/03/grid-layout-tutorial.html)

## 7、预编译的 css：

- **sass 与 scss**：scss 是 sass 的升级版。

```scss
//mixin可以定义一个你想重复使用的代码块，并可传参。
@mixin corner-icon($name, $top-or-bottom, $left-or-right) {
  background-image: url("/icons/#{$name}.svg");
  position: absolute;
  #{$top-or-bottom}: 0;
  #{$left-or-right}: 0;
}
@use 'foundation/code'; //导入指定目录下的scss文件，而且下方可以使用里面定义的变量。
@import "foundation/code", "foundation/lists"; //也用于导入文件。
.cir {
  $fs: 30px; //定义变量和使用
  width: $fs / 2;
  margin: {
    bottom: 10px; //有-的属性可以这样写成对象形式。
    top: 2px;
  }
  border-radius: if(
    $rounded-corners,
    5px,
    null
  ); //if函数，参数分别是条件，true对应的值，false对应的值。
  &:hover {
    font-size: 36px;
  } //伪类写法
  @include corner-icon("mail", top, left); //用include调用该代码块。
}
// 定义函数
@function px2vw($p) {
  @return ($p/1920) * 100vw;
}
.ff {
  width: px2vw(150);
}
/*-----使用deep来改变第三方组件库中的样式*/
/deep/.el-input {
  .el-input_count {
    height: 50px;
  }
}
/*==========
    最新语法使用::v-deep代替/deep/
============*/
::v-deep .el-input {
}

// 定义变量
$menuBg: #9966ff;
$subMenuBg: #9933ff;
$subMenuHover: #9900ff;
// 使用export将它们导出，js可使用。import variable from "var.scss";//variable.menuBg
:export {
  menuBg: $menuBg;
  subMenuBg: $subMenuBg;
}
```

- [sass 中文档](https://www.sasscss.com/documentation/syntax/parsing)
- **less**：

```less
@import "typo.css";//导入文件。
@width: 10px;
@imgurl: 'http://xxx/s';
@logoImg: "@{imgurl}/cc.png";

.bordered {
  border-top: dotted 1px black;
  border-bottom: solid 2px black;
}
#menu a {
  color: #111;
  .bordered();//less中的混合。
  &:after {
    content: " ";
    display: block;**
  }
}
// 函数使用
#colors() {
  primary: blue;
  secondary: green;
}
.button {
  color: #colors[primary];
  border: 1px solid #colors[secondary];
}
```

- [less 文档。](https://less.bootcss.com/#概览)

## 8. css 架构：

- 命令规则：一般使用 BEM 命名方式：`模块_描述--详细描述`，一套组件内的命令：`c-`。表状态：`is-或has-`。示例如下：

```html
<!--最外层是模块名-->
<div class="comment-area">
  <!--
    里层元素，名称前都加此模块名;
    子名称：用_连接;
    带功能描述的：可使用--连接
  -->
  <p class="comment-area_title">title</p>
  <button class="comment-area_title--modify">修改标题</button>
</div>
```

- 基本样式：网站想设置的全局默认样式（大小、边距、颜色等），包括更改组件库样式。将它们在主入口文件处导入。
- 对象：只关注布局的 css，将它们与基本样式分开放置。
- 全局变量：常用到的颜色、尺寸放在一个定义变量的文件中，其它文件使用。
- mixin：使用多的复杂样式也可以定义为 minx，然后 include 注入使用。
- [参考学习地址](https://zhuanlan.zhihu.com/p/32952130)
  9、元素的两个盒子：
  元素都有两个盒子，外面的盒子是 inline 级别，里面的盒子是 block 级别，<b c=gn>display 作用于外层，width，height 作用于内盒，所以</b>inline-block 能与文字一行又能设置尺寸。

```css
.inline-table {
  display: inline-table; //内联盒子
  width: 128px;
  margin-left: 10px;
  border: 1px solid #cad5eb;
}
```

# 四、库&工具

## 1、gitHub 的使用：

**安装**：

1. 进入 gitHub 官网先注册一个账号,进入菜鸟教程点击 git 本地命令工具下载链接下载。git Barsh 安装成功后打开(是一个命令行工具)；
2. **生成 SSH 公钥**：输入`ssh-keygen -t rsa -C "1815161966@qq.com"`回车会提示要在/c/Users/Administrator/.ssh/id_rsa 生成秘钥，之后一直回车到生成为止,此时在该路径下找到`id_rsa.pub`(公钥)文件用记事本打开复制里面的所有内容;
3. 再在 gitHub 官网用户设置中找到 SSH 和 GPG 项将复制内容粘到键文本域中(title 随意),回到命令行工具输入`SSH -T git@github.com`若成功会有提示成功信息。
4. 把本地项目上传到 github 在 github 上创建一个仓库(点击加号选择第一个 New repository),复制第一项中的 url 地址,然后打开 Git Bush 进入一个想放项目的文件目录中使用 cd 进入(cd G:/web)
5. 使用语句：git clone https://github.com/master,之后会在该目录下生产一个与你的仓库名同名的一个文件夹,将代码文件复制到该文件夹中;
6. 然后命令进入该文件夹(cd GanMa)再输入 git add .(把文件添加进来)再输入 git commit -m"xiaoswuwei"读入完文件后输入 git push -u origin master（传入到仓库中）.使用 git clone +地址，也能下载别人仓库中的文件。http://www.runoob.com/w3cnote/git-guide.html

**基本操作**：

- 权限：项目创建时 master 默认受保护，分支锁定：锁定后分支也是受保护状态。受保护状态的分支所有者有全部权限，其余开发人员只可拉取，不能再直接推送，只能使用发起合并请求的方式来推送。
- **合并过程中的撤销**：git merge --abort
- **回退到前一个版本** ：git reset --hard HEAD^ //^^回退两个 ~100 回退多个
- 拉取代码：git pull
- 查看远程信息：git remote -v
- 提交：git add filename，git commit -m '备注'，git push origin second //将本地分支推送到远程，
- **新建本地分支**：git checkout -b main origin/main //main 是本地分支，第二个是指从哪条源拉取代码，不写的话默认是 master。
- **新建远程分支**：网站上手动新建可直接指定源与哪个分支，命令式需要新建一个本地分支，然后：`git push origin new_dev:new_dev`#推到远程。
- 分支跟踪：git branch --set-upstream-to=origin/wcs //从 master 拉取代码，当前分支跟踪（提交时提交到该分支）远程分支 wcs。
- 查看所有分支：git branch -a //，-r 查看远程分支。
- 切换分支：git checkout master
- **查看文件状态**：git status
- **查看具体改动**：git diff (红色是改动前，绿色是改动后)
- **查看 commit 记录**：commit 历史：`git log`#会显示 commitID、人员、时间。最新的一个 commit：`git show`。查看指定人员 id 的提交记录：`git show 32cbad...`。查看指定文件修改情况：`git show 3241abk... src/avn.vue`。
- **丢弃 commit**：[参考地址](https://blog.csdn.net/zzyy1234/article/details/92429203)。
- 删除本地分支：git branch -D second
- **本地与远程分支关联情况**：git branch -vv
- **本地分支合并**：git merge WCS //合并 WCS 分支到当前分支，再 git push origin master//更新
- **远程分支合并**：一般在网站上申请合并到哪个分支，相关人员去审核，然后拉取到本地打包等操作。
- **合并发生冲突**：会提示冲突的文件，找到该文件并处理标记了冲突的地方然后 add，commit 即可。
- 查看所有分支：git branch -a
- 删除远程分支：git push origin --delete yc
- **合并冲突解决**：协商解决冲突的页面，然后 git add /src/...将冲突的页面加入，git commit -m 'merge'提交即可。

**修改仓库地址**：如仓库被迁移到另一个服务器。

1. .git/config 文件修改 url 即可。url 格式：`ssh://git@119..123/path1/project.git`
2. `git remote set-url origin xxxxxxx` #命令修改。

**全局配置用户名和密码**：如果没使用 sshKey 或使用了但不生效，那么每次 push 时都要求输密码和用户名，使用全局配置，一次性搞定。

```js
//注意这里的用户名和密码是对应所在的平台，如马云、github、gitee
git config --global user.name "wcs-ai"
git config --global user.password "34342"
```

**手动添加.gitignore 并使其生效**：git rm -r --cached . // 删除本地缓存，然后 add,commit。
**.ignore 文件格式**：

```js
# 此为注释 – 将被 Git 忽略
*.a # 忽略所有 .a 结尾的文件
!lib.a # 但 lib.a 除外
/TODO # 仅仅忽略项目根目录下的 TODO 文件，不包括 subdir/TODO
build/ # 忽略 build/ 目录下的所有文件
doc/*.txt # 会忽略 doc/notes.txt 但不包括 doc/server/arch.txt
```

**.gitignore 文件忽略设置**：(任何时候更改忽略文件都会有效)从主目录开始算路径。

```
index.html //忽略文件
/dist/   //忽略整个dist文件夹
front/dist/  //忽略front文件夹下的整个dist文件夹
front/index.html  //忽略front文件夹下的Index.html文件
```

**非克隆项目关联到 git 仓库**：本地没有修改、连接等设置，步骤如下：
`git init` #先将本地项目变为一个 git 仓库。
`git remote add origin https://xxxx.com`#关联远程仓库，
`git add .`>`git commit -m 'new'`>`git pull`#合并到本地。
此时会提示输入账号、密码，若输入错误，第二次可能不会再提示错误，而是直接报错(使用了第一次的缓存)。解决如下：
win10/控制面板/用户账户/凭据管理器/windows 凭据。最下方找到 git 的缓存，删除。
**内网中使用 git**：单独搭建一个 git 平台。封闭的内网环境内无法访问到外部网络，这需要自己在内网内指定一个 git 服务，做远程仓库用于存放代码。这也是众多代码托管平台，但多数是基于 git 或 svn 的原因。
**git 分支管理策略**：git 官网给出的一个管理分支的规则，几乎多数开发者都会使用。策略如下：

- 将 master 作为正式发布的分支，开一个 devl 作为开发使用的分支；
- 开发完成后合并到 master，然后使用 master 发布（`git merge --no-ff dev`,使用--no-ff 参数后，会执行正常合并，在 Master 分支上生成一个新节点）
- 因为其它需要，dev 上又可以延伸出其它 3 种功能的分支：预发布分支、缺陷分支、功能分支。<b c=r>这 3 个分支使用完后应该删除</b>
- 预发布分支：命名 release1.x，**源于 dev 分支**；开发完后合并：（dev 上）git merge --no-ff release1.x；开发完后，预发布在公司内测试。一般命名为 release-1.0 之类，。
- 缺陷分支：命名 fixbug，**源于 master 分支**；开发完后合并：（master 上）git merge --no-ff dev，然后 git merge --no-ff master；<b c=gn>先合并到 master，再并入 dev</b>
- 功能分支：命名 feature-x，**源于 dev 分支**；开发完后合并：（dev 上）git merge --no-ff release1.x；一个项目模块拿出来单独开发，开发完成后合并入 dev。
- [git 分支管理学习地址。](http://www.ruanyifeng.com/blog/2012/07/git.html)

| 功能         | 命名       | 创建                                  | 合并                              | 完成后 |
| :----------- | :--------- | :------------------------------------ | :-------------------------------- | ------ |
| 测试版分支   | release1.x | git checkout -b release1.0 origin/dev | dev：git merge --no-ff release1.0 | 删除   |
| 功能分支     | feature-x  | git checkout -b feature-x origin/dev  |                                   | 删除   |
| bug 分支     | fixbug     | git checkout -b fixbug origin/dev     |                                   | 删除   |
| 开发分支     | dev        | git checkout -b dev origin/master     |                                   | --     |
| 正式版本分支 | master     | --                                    |                                   | --     |

**项目资源搜索**：awesome 接想搜索的资源。[搜索技巧学习地址。](https://blog.csdn.net/csdnnews/article/details/86570635)
git-gui 的使用：在安装目录下的 cmd/下。不过是英文的，且没 sourceTree 那样全面。
[merge 时提示：refusing to merge unrelated histories 解决](https://blog.csdn.net/lindexi_gd/article/details/52554159)

## 3、nodejs：

:::alert-info
**简介**：js 只能运行在浏览器内，相比于其它 python，java 之类的编程语言可以运行在桌面环境，js 弱了很多，而 node 提供了 js 可在系统运行的环境，内部加了一些内置 api，提供文件 io 等功能。node.js 的最大优点是处理并行访问，如果一个 web 应用程序同时会有很多访问连接，就能体现使用 node.js 的优势。另一个好处是，使用 javascript 作为服务器端脚本语言，可以消除答一些与浏览器端 js 脚本的冲突。甚至发挥 javascript 动态编程的特性，在服务器与浏览器之间建立直接的动态程序。而 npm 是其自带的一个包管理工具。
:::
**windows 上安装**：官网下载 node 的 zip 包，解压后将路径添加到 path 路径即可。
**linux 上安装**：官网上下载 nodejs 的 linux 压缩包，解压进入，将 node_v...包拿出来放到相放的位置并重命名，然后建立软链接`ln -s /home/wcs/software/nodejs/bin/npm /usr/local/bin/ `(usr/local/bin 下的命令是可直接访问到的，不然要加入环境变量才行)再`ln -s /root/hone/wcs/software/bin/node /usr/local/bin/`#然后 node -v 安装成功。
**脚本语言**：又被称为扩建的语言，或者动态语言，是一种编程语言，用来控制软件应用程序，脚本通常以文本（如 ASCII)保存，只在被调用时进行解释或编译。

**包管理工具**：如果是 windows 系统的话，尽量使用管理员身份来运行 cmd，然后进行 npm 操作

1. cnpm：
   **配置淘宝安装源**：npm 本身指定的安装源是外国的，`npm install -g cnpm --registry=https://registry.npm.taobao.org`#安装淘宝镜像,使用时直接 cnpm install 即可.
   [参考学习地址.](https://www.cnblogs.com/onew/p/11330439.html)

- 错误集：
  - 打包 vue 项目报错：javascript heap out of memory。node 打包 vue 项目提示该 javascript 运行导致内存溢出，这是 node 封装的 v8 引擎运行的 javascript 其限制了 js 能使用的内存，解决如下：

```js
//在package.json文件加入：
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

- 删除 node_module 文件夹，重新 npm install 安装依赖，然后项目下：npm run fix-memory-limit
  //然后安装：`npm install -g increase-memory-limit`#接着进入项目目录执行：`increase-memory-limit`#结束后再试试运行项目。
- [参考学习地址(先尝试 3，4)](https://www.jianshu.com/p/410e826506be)。
- [npm 安装包失败的问题(设置一下安装源，npm 安装即可)。](https://blog.csdn.net/moxiong3212/article/details/79756553)

2. **npm**：
   临时设置安装源：`npm config set registry https://registry.npm.taobao.org `。
   npm 指令管理包的指令：

```cmd
npm install --save lodash  #--save表示生产环境的依赖，--save-dev表示开发环境的依赖。
npm cache clean -f       //清除缓存。
npm remove eslint        //移除包内的某个依赖。
npm install vue@3.0      //安装指定版本写法
```

**nvm**：[windows 版 nvm 下载地址，下载 nvm-setup.zip 包](https://github.com/coreybutler/nvm-windows/releases)。安装后 cmd 使用 nvm 命令
`nvm install 8.16.0`#安装其它 node 版本。`nvm use 8.16.0`#切换 node 版本。`nvm uninstall 8.16.0`#卸载指定版本。 - **运行 js 文件**：node name.js - **使用同级文件**：`const fl = require('./index')`。 - **使用同级目录下的文件**：`const fl = require('./config/multi')` - \*\*dirname：当前文件所在目录的绝对路径。

- \*\*filename：当前文件的绝对路径 - process.argv#以一个列表的形式返回命令行所有参数，如：`node a.js -m cc`->`['node','a.js','-m','cc']`

<i class="label1">编写自己的 npm 包</i>可以自己按照 npm 包的规则来写一个包，然后发布到 npm 平台使用。步骤如下：

- [先到 npm 官网注册一个人账号。](https://www.npmjs.com/signup)
- 进入一个人文件夹，使用 npm init，填写一些信息（会生成 package.json 文件），初始化一个 npm 包。其中**main 指定入口文件**如：`./moment.js`。
- 安装依赖：如果自己的这个 npm 包需要其它依赖，直接该目录下 npm i ... --save 即可。
- 登录：npm login 登录账号。
- 指定的入口 js 文件最后需要用：`module.exports = obj`//的形式导出一个模块。
- 发布：npm publish。撤销发布：npm unpublish

3. yarn：并行安装、离线模式、安装版本统一、多注册来源处理。
   - 安装：`npm install yarn -g`
   - yarn 安装：yarn install

### b、文件操作：

读写操作：

```js
var fs = require("fs");
// 读取指定目录下的所有一级目录或文件。
fs.readdir(MODULE_PATH, function (err, files) {
  if (err) {
    console.error(err);
  } else {
    pages = files;
  }
});
/*几乎所有的这类放发都有Sync，为同步读取*/
var pages = fs.readdirSync(MODULE_PATH);

const option = { flag: "w", encoding: "utf-8", mode: "0666" }; //flag指定使用的模式。
// 写
fs.writeFile("test.text", "内容", option, function (err) {
  if (err) {
    console.log("写入错误" + err);
  } else {
    console.log("写入成功" + err);
  }
});
// 一般使用writeFileSync()完成文件复制操作。
// 读，readFileSync为同步读取。
fs.readFile(
  "test.text",
  { flag: "r", encoding: "utf-8" },
  function (err, data) {
    if (!err) {
      console.log("文件数据" + data);
    }
  }
);
```

### c1、chalk 的使用：

一个给字体添加样式的包，支持模板使用：

```js
const chalk = require("chalk");
//字体颜色、粗体、背景色。
console.log(chalk.red.bold.bgWhite("内容"));
//模板写法
console.info(chalk`{blue.bold 内容}`);
```

### c2、输入，输出：

```js
//方法一
process.stdin.resume();
process.stdin.setEncoding("utf-8"); //设置字符集
process.stdout.write("请输入:"); //标准输出
process.stdin.on("data", function (data) {
  var str = data.slice(0, -2); //slice选取字符。不使用也可
  process.stdin.emit("end"); //输入结束，触发
  process.stdout.write("输入的:" + str);
});
process.stdin.on("end", function () {
  //    监听上面的end事件。
  process.stdin.pause();
});
//------- 方法二
const readline = require("readline");
const rl = readline.createInterface({
  input: process.stdin,
  output: process.stdout,
});
//获取输入
read.on("line", (line) => {
  inputArray.push(line);
  console.warn(">", inputArray);
  if (inputArray.length === 2) read.close();
});
rl.question("你认为 Node.js 中文网怎么样？", (answer) => {
  // 对答案进行处理
  console.log(`多谢你的反馈：${answer}`);
  rl.close();
});
rl.on("close", function () {
  process.exit(); //退出命令行。
});
```

## 4、第三方平台：

1. **postman 的使用**：
   (百度搜索下载 postman 安装)输入框左边选择请求方式，输入框中输入请求接口，下方 Params 项中输入要传的键值和 value 值，键值和 value 值的输入不需用单引号或双引号不然会出错,若报错可以在 body 项中选择 form-data 然后输入 Params 项中的键值和 value 值再点 Send。
2. **微信公众号**：
   先用超级管理员账号登录微信公众号平台，开发>开发者工具>微信开发者工具>绑定开发者(将自己的微信号绑定为开发者账号)。
   开发>接口权限>网页服务>网页授权>修改下把目标网站域名添加为公众号授权网页(先上传那个 txt 文件到服务器项目根目录)。
   **授权登录步骤**：
   > 跳转文档中指定的地址（地址中加上 appid 之类的参数）。分静默和非静默两种。
   > 对应页面用户手动点击授权登录后会将 code 放到 url 中返回，且会刷新刚才那个页面。
   > 获取到 code（为 openId）上传给后台，后台会与微信服务器换取信息，返回 token 给前端。
   > 用该 token 作为用户已登录的凭证，存于本地。注意跳转页面时判断 token 是否过期。

**微信支付**：

- 微信小程序内：向后台获取时间戳、签名串等，然后：

```js
wx.requestOrderPayment({
  timeStamp: "",
  nonceStr: "",
  package: "",
  signType: "MD5",
  paySign: "",
  success(res) {}, //拉起微信支付，支付成功后调用。
  fail(res) {},
});
```

- 公众号内：使用 H5 支付需要先在商户号开通 H5 支付，还需要填写支付域名。前端调用自己后台的下单接口成功后跳转到后台返回的支付页 url 即可。
- 普通 H5 页面：与公众号类型。
- **注意**：url 地址处理使用 encodeURIComponent(url)函数处理,这个 url 中不能加端口号，所以只能是刚才配置的授权网页域名。
- [配置、获取 openid、授权登录。](https://www.jianshu.com/p/b7e2100b56e4)

3. **集成网易云信 IM**：
   下载 demo(下载后先 npm i 安装必要插件)
   在 login.js 文件中，先将对应的 appkey 换成自己的。然后在获取到登录界面输入的账号，密码后添加一个网络请求，向自己的服务器获取用户在本应用下(对应的 appkey 应用下)的 im 用户 id 和云信服务器反给后台的云信 token,然后调用 cookie.setCookie()按格式放入到 cookie 中。
   每次更改调试需要先 npm run dev 打包再 node server 启动本地服务。
   要放到服务器使用的话直接将打包后的 dist 文件夹、regist.html,login.html,index.html 文件放到服务器即可，主入口是 index.html 文件，在自己的项目中直接访问该路径+路由，然后带上 uid,yxtoken 两个参数(在指定 im 页面获取参数调用 setCookie()登录，不然会报错)。

4. **微信小程序**：

- **获取 openId**：

```js
wx.login({
  success(res) {
    if (res.code) {
      // 这里调用自己后台接口，用code交换openId。
    } else {
      console.log("登录失败！" + res.errMsg);
    }
  },
});
```

- 调起微信小程序：小程序需要已正式上线发布。

  - 通过 url scheme 跳转进来（公众平台/工具，生成类似 weixin://dl/business?t=Ljf-...），ios，网页中可直接 location.href 打开。
  - android App 调用：android 无法通过 scheme 调起小程序，不过可以提供**小程序原始 id**（公众平台/设置，查看。非小程序 id）、线上版本号、页面路径，供其 app 打开。

- **文件 formData 上传**：小程序无有 formData 对象，使用以下方式与 formData 对象上传文件对象

```js
wx.chooseImage({
  count: 1, //默认9
  sizeType: ["original"], //可以指定是原图还是压缩图，默认二者都有
  sourceType: ["album"], //从相册选择
  success: function (res) {
    //console.log(JSON.stringify(res.tempFilePaths),config.baseUrl + "/system/user/profile/avatar");
    wx.uploadFile({
      url: "http://xxx.com/system/user/profile/avatar",
      filePath: res.tempFilePaths[0],
      header: {
        "content-type": "multipart/form-data", //'application/json',
        token: uni.getStorageSync("token"),
        Authorization: uni.getStorageSync("token"),
      },
      name: "avatarfile",
      formData: {
        id: 11, //TODO:放置额外的参数
      },
      success(rq) {
        let data = JSON.parse(rq.data); // TODO:返回的是JSON
        if (data.respCode === "00") {
          _s.userInfo.avatar = data.imgUrl;
          uni.showToast({
            title: "修改成功",
            icon: "none",
          });
        }
      },
    });
  },
});
```

5、动画开发：

- [anime.js 文档](https://www.animejs.cn/documentation/#direction)

## 6、资源收集：

**文章部分**：
[张鑫旭空间](https://www.zhangxinxu.com/)、[前端技术文档大全](https://developer.mozilla.org/zh-CN/docs/Web/API/MediaDevices/ondevicechange)
[HTML 转义字符表](http://tool.oschina.net/commons?type=2)、[HTML 标签大全](http://www.w3school.com.cn/tags/index.asp%20)、[axure 各破解版本下载地址。](https://www.axure.com.cn/78629/)、[plotly.js 起始教程地址，里面有下载地址(dist 文件夹下)。和源码文档。](https://www.kutu66.com//GitHub/article_132050)、[javascript 事件集](http://www.w3school.com.cn/html5/html5_ref_eventattributes.asp)、[支付宝 H5 开发文档](https://myjsapi.alipay.com/alipayjsapi/index.html#3__E5_BF_AB_E9_80_9F_E5_BC_80_E5_A7_8B)、[marquee 标签属性大全](https://blog.csdn.net/bright_101/article/details/52124278)、[validator 官网 git 地址，里面有使用示例。](https://github.com/yiminghe/async-validator#start-of-content)
[jest 使用](https://www.cnblogs.com/chenwenhao/p/12007184.html)、[谷歌浏览器插件开发文档](https://developer.chrome.com/extensions/getstarted.html)
**工具部分**：[很多实用前端工具。](https://www.zhihu.com/question/20241338?sort=created)

- [属性兼容性查看网站](https://caniuse.com/?search=flex)：红色为完全不支持的版本，棕色为部分支持的版本，绿色为几乎全部支持的版本。命令使用：npm install -g caniuse-cmd
- [配色网站](https://colorhunt.co/)：很多不错的颜色值组合。
- [诸多在线工具网站](https://tool.lu/)、[windows 部分批处理命令学习](https://blog.csdn.net/qq_17204441/article/details/89062591)

## 8、IDE 工具:

### a、vscode：

:::alert-info
支持各种语言的开发,但需要对应的插件来支持,所以会有一定缺陷。打开 vscode 点击第四个图标(方形)，安装 python 在点右边的安装。
:::

- **快捷键**: 参考地址:https://www.cnblogs.com/pleiades/p/8146658.html
  首先是 F1/Ctrl+Shit+P 万能键。Ctrl+P：文件切换。Ctrl+空格：自动提示。
  F12/Ctrl+左键：跳转到定义。Shift+F12：预览定义。Ctrl+G：跳转行号。Ctrl+/：注释切换
  Alt+↑↓：整行上下移动。Ctrl+↑↓：编辑器垂直滚动条上下移动，光标不动。Ctrl+Backspace/Delete：整词/连续空白删除。Ctrl+→←：光标整词移动
  Ctrl+F 查找/Ctrl+Shift+F 在文件中查找，这都属于通用的。F5：运行代码。Ctrl+F5：运行当前文件代码。Shift+Alt+F：触发默认格式化。
  选择下一个相同字符：ctrl+D
  选择全部相同字符：ctrl+shift+L

- **部分插件配置**：vscode 上一款不错的颜色主题：搜索 Code Blue 点击 install 右界面点击 Reload 使用
  vscode 下载项输入框搜索 Live Serve 点击下载安装后右界面点击 Reload to Active 后在 html 文件页面点击最下方(软件脚部)的 Go Live(也可能是@go live)会在浏览器打开页面此时浏览器地址栏就变成了 ip 地址而不是本地路径地址，(使用默认浏览器时有效)。
  **好用的插件**：Dracula(颜色样式插件)、city Lights icon package(icon 插件)、vue、Anaconda。
  **插件使用**：左侧栏最后一个功能搜索下载，下载好后右边界面上方有设置使用按钮。
- Markdown 插件：Markdown Preview 插件，支持全屏预览，目录和一些附加功能（ctrl+shift+v 预览）；还有一些其它 md 插件，自己搜索探索；（源码页，上方状态栏可点目录）
- **Powern Model 插件**：在选择颜色主题栏最下方选择安装其它主题，下载 Power Model 插件然后在左下角点击设置打开 user settings 文件或按 F1 输入 user settings，界面右半部分大括号中加上"powermode.enabled":true,就能使用该插件了,"powermode.enableShake":false//桌面是否震动
  ，"powermode.presets":"particles"/"fireworks"/"magic"/"flames"/样式。
  (配置的文件是 json 文件一定要用双引号)然后点击 Reload to Active 载入即可使用。
- **vscode-icons**：颜色主题安装列表中安装 vscode-icoons，点击 Reload to Active 然后按 F1 输入 icon 在弹出的列表中点击激活 vscode icons 即可使用该插件。[同时选中多个相同的字符]ctrl+shift+L 选中该页中所有相同的字符。ctrl+D 选择下一个相同的字符
- markdown+math：支持 markdown 中书写数学公式，右上角预览按钮查看效果。上班偷学数学使用。

**格式化**：

- **python 代码格式化**：先安装 yapf 库，pip install yapf 然后在 cscode 设置搜索框中搜 python.formatting.provider 右边下拉框中选择 yapf。设置好后选中要整理的代码块，右键点 format selection 整理，但对缩进无效。空格只有半字符长问题：设置>搜索框输入 font，FontFamily 项输入'monospace'
- **prettier 格式化**：主要 web 代码时使用，部分配置如下（setting.js）：其它详细的可以搜索 prettier 设置。[prettier 相关设置。](https://blog.csdn.net/hbiao68/article/details/107176795/)
- **editor 格式化配置**（setting.js）：

```js
{
  //editor是vscode自带的格式化配置方法，有这些配置时vs就会使用。
  //!项目根目录下的.editorconfig文件就是editor的配置，vs会优先使用这个配置。
  "editor.suggestSelection": "first",
  "editor.fontSize": 16,
  "editor.tabSize": 2,//table为几个字符长。
  "editor.detectIndentation": false,
  "editor.formatOnSave": true,//保存时自动格式化。！！就算使用了其它格式化插件，也请开启此项。
  //"eslint.autoFixOnSave": true,
  "editor.codeActionsOnSave": {
    "source.fixAll.eslint": true
  },
  "editor.fontLigatures": false,
}
```

- **.editorconfig 格式**：安装 EditorConfig 插件后可用

```
[{*.js,*.vue}]    #用来匹配文件，匹配到的遵守下面规则。
indent_style = tab  #设置缩进风格(tab是硬缩进，space为软缩进)
indent_size = 4   #用一个整数定义的列数来设置缩进的宽度，如果indent_style为tab，则此属性默认为tab_width
tab_width = 4    #用一个整数来设置tab缩进的列数。默认是indent_size
end_of_line = lf   #设置换行符，值为lf、cr和crlf
charset = utf-8     #设置编码，值为latin1、utf-8、utf-8-bom、utf-16be和utf-16le，不建议使用utf-8-bom
trim_trailing_whitespace = true #设为true表示会去除换行行首的任意空白字符。
insert_final_newline = true   #设为true表示使文件以一个空白行结尾
root = true    　　　#表示是最顶层的配置文件，发现设为true时，才会停止查找.editorconfig文

#其它匹配符号：
*        匹配除/之外的任意字符串
**        匹配任意字符串
?        匹配任意单个字符
[name]      匹配name中的任意一个单一字符
[!name]     匹配不存在name中的任意一个单一字符
{s1,s2,s3}    匹配给定的字符串中的任意一个(用逗号分隔)
{num1..num2}  　匹配num1到num2之间的任意一个整数, 这里的num1和num2可以为正整数也可以为负整数
```

- **使用 prettier 格式化**：可在根目录下建立 prettier.config.js 用于配置，其它类型参考：[prettier 官网](https://prettier.io/docs/en/configuration.html)。[prettier 配置大全](https://segmentfault.com/a/1190000012909159)。

```js
//prettier.config.js or .prettierrc.js
module.exports = {
  trailingComma: "none", //对象最尾无逗号。
  tabWidth: 4,
  semi: true,
  singleQuote: false,
  useTabs: false,
};
```

**ignore**：忽略一些不想格式化的代码。可在项目根目录下建一个.prettierign 文件忽略不格式的文件，写法与其它 git 等的忽略一样。

```vue
<!-- prettier-ignore -->
#html部分的忽略写法，会忽略下面这个html的格式化
<pop v-model="(fm['ac'] = vb || ac[0])" />

{/* prettier-ignore */} #jsx中的忽略写法 // prettier-ignore #js部分的忽略写法
var c=89;
```

- **vetur 格式化**：支持 vue 文件语法高亮，使用 eslint-plugin-vue@beta 检测，可配置对 vue 页面代码的格式化（多数情况下会关闭 vetur 的检测和 js 部分的格式化）。[vetur 官网](https://vuejs.github.io/vetur/guide/highlighting.html#custom-block)

```js
{
    "vetur.format.defaultFormatter.html": "prettier",//可设置哪部分代码使用指定插件格式化。
    "vetur.validation.template": false,//关闭vetur的检测。这样不和eslint的检测冲突。
    "vetur.format.defaultFormatterOptions": {
		"js-beautify-html": {
			//"wrap_attributes": "force-aligned" //属性强制折行对齐
			"wrap_attributes": "auto"
		},
		"prettier": {
			"semi": true,// 结尾使用分号。    ！！！这里的优先级更高。
			"singleQuote": false    //关闭单引号代替双引号。
		},
		"vscode-typescript": {
			"semi": false,
			"singleQuote": false
		}
	},
	// 格式化stylus, 需安装Manta's Stylus Supremacy插件
    "stylusSupremacy.insertColons": false, // 是否插入冒号
    "stylusSupremacy.insertSemicolons": false, // 是否插入分好
}
```

**我的 vscode/setting.json**：

```json
{
  "workbench.iconTheme": "city-lights-icons-vsc",
  "vsintellicode.modify.editor.suggestSelection": "automaticallyOverrodeDefaultValue",
  "workbench.colorTheme": "Shades of Purple",
  "gitHistory.alwaysPromptRepositoryPicker": true,
  "iceworks.materialSources": [],
  "editor.suggestSelection": "first",
  "editor.formatOnSave": true, //保存时触发格式化
  "eslint.run": "onSave",
  "editor.codeActionsOnSave": {
    "source.fixAll.eslint": true
  },
  "editor.tabSize": 2,
  "git.ignoreWindowsGit27Warning": true,
  "vetur.validation.template": false, //关闭vetur的检测。
  "vetur.format.defaultFormatter.js": "none", //关闭vetur对js的格式化。
  "vetur.format.defaultFormatter.html": "prettier",
  "[json]": {
    "editor.defaultFormatter": "esbenp.prettier-vscode"
  },
  "files.exclude": {
    "**/.classpath": true,
    "**/.project": true,
    "**/.settings": true,
    "**/.factorypath": true
  }
}
```

配置 2：

```json
{
    // 整个窗口缩放比例
    "window.zoomLevel": 1,
    // lint 配置
    "eslint.validate": [
        "javascript",
        "javascriptreact",
        {
            "language": "vue",
            "autoFix": true
        }
    ],
    // save 后自动 fixed 代码
    "eslint.autoFixOnSave": true,
    "tslint.autoFixOnSave": true,
    // prettier 配置
    "prettier.singleQuote": true,
    "prettier.stylelintIntegration": true,
    "prettier.eslintIntegration": true,
    "prettier.tslintIntegration": true,
    "prettier.jsxSingleQuote": true,
    "prettier.useTabs": true,
    // vetur 配置
    "vetur.format.options.useTabs": true,
    "vetur.format.defaultFormatter.html": "js-beautify-html",
    // 编辑器配置（默认tab、字体修改）
    "editor.formatOnSave": true,
    "editor.tabSize": 2,
    "editor.fontFamily": "Fira Code",
    "editor.fontLigatures": true,
    // git 配置
    "git.enableSmartCommit": true,
    "git.autofetch": true
    // go 配置
    "go.gopath": "/Users/xx/xx",
    "go.autocompleteUnimportedPackages": true,
    "go.gocodeAutoBuild": true,
}
```

修改 python 环境：设置中搜索 python.python path 将框内的路径修改为自己想要的(worker pace 和 user 项都修改)，如果不成功则参考 35 中的注意事项。
控制台打印中文乱码问题：点击左侧工具栏第四个按钮，左上角点击生成 launch.json 文件，选择 python 环境，然后在生成的文件中以下位置填入：

```
  "version": "0.2.0",
  "configurations": [
    {
      "name": "Python: 当前文件",
      "type": "python",
      "request": "launch",
      "program": "${file}",
      "console": "integratedTerminal",
      "env":{/*添加这个env配置*/
        "PYTHONIOENCODING":"GBK"
      }
    }
```

Anaconda 环境设置：插件安装栏搜索 anaconda 安装运行即可。
写 python 代码没有提示和补全：先确保安装了 kite Autocomplete(一个 python 和 javascript 的自动补全插件)插件(顺便安装 kiteConnect 插件)，若安装重启 vscode 后还未生效，右下角会有 kite query install ...的提示，点击 install 按钮跳到 git 地址，下方有各系统下载地址，按照教程安装，使用即可，安装后重启 vscode 即可生效。[git 地址。](https://github.com/kiteco/vscode-plugin#installation)

### b、sublim 编辑器：

sublim 使用起来在提示方面和运行速度方面都很不错，要使用 Anaconda 中的环境需要安装一些插件:
CTRL+SHIFT+p 打开输入框输入 install Package Control 回车安装再：install Package 都安装好后就可以在搜索框中搜索 Anaconda 回车安装了(左下角)
[ctrl+Tab]鼠标放在一个调用的函数括号中按 ctrl+Tab 能还呼出该函数的所有参数。
去除白框：anaconda 插件，用户设置中添加："anaconda_linting": false
sublim3 配置 python 环境：https://blog.csdn.net/Ti__iT/article/details/78830040
https://www.jianshu.com/p/0ad5625e9717
[选中多个相同字符]ctrl + d,一直按，从当前向下查找相同字符。
[改变运行环境]anaconda 插件，默认设置下修改 python_interpreter 后的值为想要设置的 python.exe
文件所在的目录，注意使用\\。然后工具栏>编译系统中选择 Anaconda Python Build
[新建一个编译系统]选择编译系统后，sublim 会按指定的编译系统解析文件中的代码。编译系统,新建: #修改下面 python.exe 所在的路径 path 即可。

```json
{
  "cmd": ["python.exe", "-u", "$file"],
  "path": "E:\\somtwar\\Anaconda\\plateform\\envs\\wcs",
  "file_regex": "^[ ]*File \"(...*?)\", line ([0-9]*)",
  "selector": "source.python"
}
```

### c、jetBring 公司产品：

**主题样式下载**：http://www.riaway.com/theme.php。
**更换主题后字体会变小问题**：在 setting>Editor>Color Scheme>color scheme Font 中设置字体大小。注意不是 consol Font
**主题的使用**：setting/color scheme/右侧齿轮按钮点击选：Import setting 导入自己下载的 jar 包，应用即可。

- **pycharm 插件**：[插件资源 1](https://www.cnblogs.com/jfdwd/p/11137798.html)、[插件资源 2](https://www.2bboy.com/archives/153.html)
- **快捷键**：[常用快捷键。](https://www.cnblogs.com/sui776265233/p/10200809.html)
  Ctrl + F(当前文件查找 )。Ctrl + R(当前文件替换)。Ctrl + Shift + F(全局查找)。
  Ctrl + Shift + R(全局替换)。
  隐藏左边的文件栏：shift+esc 。 打开左侧项目目录：ALT+1
  Shift + F10#运行。Shift + F9#调试。Alt + Shift + F10 运行模式配置。Alt + Shift + F9 调试模式配置
  同时选择相同字符串的下一个：Alt+j。
  选中当前文件所有相同字符串：Ctrl+Alt+shift+j。

- [linux 上安装 pycharm。](https://blog.csdn.net/xiaoxiaofengsun/article/details/82257391)
  **使用 Anaconda 环境**：setting>project:name>Project interpreter 下拉框中选择运行的环境，添加新的运行环境：下拉框点 show all 后点击+号>选第二个单选文件夹中选择 Anaconda 安装目录>envs>wcs>python.exe(envs 是自己在 anaconda 创建的所有环境,wcs 是自己创建的一个环境,每个环境下都有一个 python.exe)不过似乎还会要下载点东西，网速不好就恼火咯，包括 sublim 中切换环境也是切换 python.exe 的位置。

### d、jupyter:

一个 web 式的 ide 工具，通过电脑上安装 jupyter notebook 工具，运行后会开通一个本地服务，按照其给出的链接进入 web 页面，在上面进行编辑代码。支持 50 多种语言。

- 安装：`pip install jupyter`。
- 使用：命令行`jupyter notebook`直接运行会出现一个链接，在 web 中打开。#windows 端应该是一个虚拟机形似的运行工具。
  进入 web 页面后会将当前用户下所有的目录显示出来，右侧的 view 选项中选择 python3 进入一个编辑页面。
- 问题：pip install -i https://pypi.mirrors.ustc.edu.cn/simple/ prompt-toolkit==1.0.15 # prompt-toolkit 的版本过高致使与 Jupyter-notebook 的版本不兼容
  e、visual studio：
  下载安装：到官网下载社区版，社区版可免费使用。选中安装位置、下载位置、工具位置。
  新建项目：左上角新建项目。源文件下新建 c++文件。

## 9、真机调试：(使用谷歌浏览器)

**方法一**：同一局域网内，用手机直接访问 node 开启的 web 服务地址(ip 地址使用电脑 ipv4 地址，而不是 localhost)。
**方法二**：使用 google 浏览器。
pc 端和手机端都下载 google 浏览器，手机上打开开发者选项并允许使用 usb 调试(可按链接中教程一样使用安装驱动也可以 pc 端下载手机助手),手机和 pc 用数据线连接,然后打开手机端 chrome 浏览器(确认连接,连接成功后手机助手会显示手机页面),在 pc 端 google 浏览器地址栏中输入 chrome://inspect 进入如下
![google_phone](_v_images/20200419110535134_1308380564.jpg)
若下面没有显示手机型号可以多等待一会试试，输入框中输入要打开的网页,如果是打开自己做的项目地址要写成 pc 地址加文件名(例:浏览器中带服务打开网页为
127.0.0.1:5500/self.html,需要输入 192.168.1.12:5500/self.html)这里的 192.168.1.12 是你 pc 的 ipv4 地址。(注:虽然在手机浏览器上能看到效果但其实在 pc 端浏览器上运行的效果,并不是在手机端浏览器环境下运行出来的)。[参考地址 1。](https://www.cnblogs.com/meakchen/p/5665887.html)[参考地址 2。](https://www.cnblogs.com/imwtr/archive/2016/09/18/5881039.html)
**问题**：如果方法一无法打开页面，那么可以尝试设置防火墙，设置里有控制各服务允许通过防火墙的设置，找到 node,javascript 相关字样的，勾选允许即可。
[解决该问题参考地址。](https://www.cnblogs.com/AwenJS/p/12840924.html)

google 浏览器控制台使用：

- netWork/wifi 形状左侧，可选择 slow3G，模拟弱网环境；
- 右上角设置/右下角 Disable javascript，可禁用 js；

## 11、uni-app 的使用：

**介绍**：uni-app 是一个使用 Vue.js 开发所有前端应用的框架，开发者编写一套代码，可发布到 iOS、Android、H5、以及各种小程序（微信/支付宝/百度/头条/QQ/钉钉/淘宝）、快应用等多个平台。结合 Hbuilder x 使用，文件新建一个项目选择 uni-app 项目(网站、app、小程序都选这个)。[uni-app 官网。](https://uniapp.dcloud.io/)[插件市场](https://ext.dcloud.net.cn/search?q=uni-ui)。
**项目目录结构**：pages 文件夹存放业务页面，pages/index/index.vue 页面是 app 打开时的引导页面。创建其它页面时新建一个文件夹然后在文件夹内建页面，可以多个页面放一个文件夹。
static 文件夹存放静态资源文件。main.js 文件是 vue 实例化入口。APP.vue 页面写全局样式，生命周期函数。manifest.json 文件配置应用名、appid、图标等。package.json 配置路由，选项卡、插件、导航条等。
**插件、组件的使用**：在插件市场中可以搜索想要的插件，点击 hbuildx 导入能直接调用 hbuilderx 安装插件，安装好后会放在目录下的 components 中，当作组件调用即可，示例：

```html
<pop type="text"></pop> //不用:来表示绑定。
<script>
  import pop from "@/components/load.vue"; //导入。
  //-------使用注释#ifndef和#endif包围的代码只在，编译或打包到该端时使用。
  // #ifndef H5
  const vv = 10;
  // #endif
  export default {
    data() {
      return { text: "hh" };
    },
  };
</script>
```

一些常用插件地址：[弹出框(顶、中、底弹出)。](https://ext.dcloud.net.cn/plugin?id=329)[头部导航插件。](https://ext.dcloud.net.cn/plugin?id=52)[时间、日期、城市联动选择器。](https://ext.dcloud.net.cn/plugin?id=273)[cool 组件库文档地址，功能还算比较全面。](http://uni.cooljs.vip)
cool 组件库的大体使用：从[git 地址](https://github.com/cool-team-official/cool-uni)下载到本地，把里面的 src/cool 文件夹复制到项目根目录中，然后 pages.json 文件加入以下配置：

```js
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

然后在 APP.vue 页面的 style 引入它的 css 文件，如下：

```
<style lang="scss">
@import "cool/ui/static/css/index.scss";
</style>
// 其它单页面中导入组件：然后可以按照文档中的教程使用了。
import clButton from "@/cool/ui/components/button/button"
```

**app 唤醒页和引导页**：app 中打开都有一个广告页面，第一次使用 app 都有一个引导页面，在 uni-app 开发 app 时需要新建一个页面来放置它们=》在 index 文件夹下新建一个 Introduct.vue 页面，然后在 package.json 文件设置如下：

```js
{
    "pages":[{
        "path":"pages/index/introduct",
        "style":{
            "app-plus":{"titleNView":false} //静用掉自带的顶部，这样才能全屏显示。（index页面首页也可以设置这个）
        }
    }]
}
```

建议将唤醒页和引导页放在同一个页面。在生命周期函数中写一个定时器，3 秒后跳到首页。

```
onReady(){
	setTimeout(()=>{
		this.$router.replace('../index/index')
	},3000);
},
```

**页面生命周期函数**：

```js
onLoad(){}//	监听页面加载，其参数为上个页面传递的数据，参数类型为Object（用于页面传参
onShow()//	//监听页面显示
onReady(){}//	监听页面初次渲染完成
onHide(){}	//监听页面隐藏
onUnload(){}	//监听页面卸载
onPullDownRefresh(){}//	监听用户下拉动作 ，一般用于下拉刷新
onReachBottom(){}//	页面上拉触底事件的处理函数
onPageScroll(){}//	监听页面滚动 ，参数为 Object
onTabItemTap(){}//	当前是 tab 页时，点击 tab 时触发。
onShareAppMessage(){}//用户点击右上角分享
/*============
{   子组件中，周期函数使用vue语法。
    mounted(){}
}
==============*/
```

**尺寸单位**：uni-app 中使用 upx 为自适应单位，与小程序一样，750upx 占满屏宽，设计稿不是 750 大小的需要与 750 算一个比例，然后在量一个元素大小时乘以该比例转化为 upx 大小即可。

- H5 端的 rpx 被转为 px，但随机型变化也会变化（所以不用使用 rem 做适应）！暂时不知道怎么实现的。
- **转换 upx**：只要在 manifest.json 里配置下面"transformPx" : true。
- H5 端 rem 使用：[rem 使用的特别解决方案](https://www.jianshu.com/p/62e399f4aa2e)
- [uni-app 中的跨域解决。](https://blog.csdn.net/paopao79085/article/details/91948809)、[全局可用的 api](https://uniapp.dcloud.io/api/README)

**app 调用微信小程序**：[参考地址](https://ask.dcloud.net.cn/question/67412)

```js
function gowx() {
  if (plus.os.name == "Android") {
    // 需先在manifest.json中配置微信分享。
    plus.share.getServices(
      function (res) {
        var sweixin = null;
        for (var i = 0; i < res.length; i++) {
          var t = res[i];
          if (t.id == "weixin") {
            sweixin = t;
          }
        }
        if (sweixin) {
          sweixin.launchMiniProgram({
            id: "小程序原始id", //非小程序id
            type: 1.1, // 版本号
            path: "pages/index/index",
          });
        }
      },
      function (res) {
        console.log(JSON.stringify(res));
      }
    );
  } else {
    plus.runtime.launchApplication(
      {
        action: "weixin://dl/business?t=Kjl-...",
      },
      function (e) {
        console.log("Open system default browser failed: " + e.message);
      }
    );
  }
}
```

路由及传参：
getApp().globalData.idenInfo = res;

- 问题集合：
  （1）H5 端，页面刷新有时会有无法回退、页面不加载等问题。
  （2）打开小程序报：errno: -4083：维新开发工具/设置/安全/打开服务端口

## 12、富文本编辑器：

web 中使用的富文本编辑器比较多，这里是两个自己尝试过的：
wangeditor：比较轻便，所以功能没有其它几样多，因为简便所以比较容易引入，几乎不会报异常错误。[wangeditor 使用参考地址。](https://www.jianshu.com/p/52852d39f869)
vue 项目中安装：`npm i wangeditor -S`#使用配置如下：

```html
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
        editorContent: "",
      };
    },
    mounted() {
      this.editor = new E(this.$refs.editorElem);
      // 编辑器的事件，每次改变会获取其html内容
      this.editor.customConfig.onchange = (html) => {
        this.editorContent = html;
        this.catchData(this.editorContent); // 把这个html通过catchData的方法传入父组件
      };
      this.editor.customConfig.menus = [
        // 菜单配置
        "head", // 标题
        "bold", // 粗体
        "fontSize", // 字号
        "fontName", // 字体
        "italic", // 斜体
        "underline", // 下划线
        "strikeThrough", // 删除线
        "foreColor", // 文字颜色
        "backColor", // 背景颜色
        "link", // 插入链接
        "list", // 列表
        "justify", // 对齐方式
        "quote", // 引用
        "emoticon", // 表情
        "image", // 插入图片
        "table", // 表格
        "code", // 插入代码
        "undo", // 撤销
        "redo", // 重复
      ];
      this.editor.create(); // 创建富文本实例
    },
  };
</script>
```

**tinymce**：国外的，默认是英文，中文版的需要下载语言包。[参考学习地址。](https://www.cnblogs.com/wisewrong/p/8985471.html)[语言包下载地址。](https://www.tiny.cloud/get-tiny/language-packages/)
引入后报..dont support (text/html) ..css 的错误：在`<style></style>`中用@import url("");引入 css 样式。
出现找不到中文语言包的问题：！暂未解决。
[百度 umeditor 下载地址(选择 jsp)。](http://ueditor.baidu.com/website/download.html)[使用参考学习地址。](https://blog.csdn.net/fanhu6816/article/details/81223909)

## 13、axios：

内部依然封装的 ajax 使用。npm install axios

```js
import axios from "axios";
const URL = require("./index");
// 响应时间
axios.defaults.timeout = 5000;
// 请求头设置
axios.defaults.headers.post["Content-Type"] =
  "application/x-www-form-urlencoded;charset=UTF-8";
/*--不同的环境可以设置不同的地址。
--如果服务端配置了接口的映射的话，也可以不写生产环境的url，但本地代理配置请保持与服务端一致。
----列devserve:{'/api':{target:"http://127.45.28.29:8080"}}，一个接口：/api/login。该项目打包后放置在：http://av.cc.com
----访问这个接口时变为：http://av.cc.com/api/login，av.cc.com服务端配置的代理可以匹配到/api将其反向代理到真正的接口地址。
*/
if (process.env.NODE_ENV === "production") {
  axios.defaults.baseURL = "https://nb.com";
} else {
  axios.defaults.baseURL = URL.dev.requestUrl;
}

// 请求拦截器
axios.interceptors.request.use(
  (config) => {
    // 这里添加加载动画
    if (config.method === "post") {
      config.data = JSON.stringify(config.data);
    }
    // 可以通过axios.post(url,data,params)#params传递参数。
    if (config.params["switchType"]) {
      config.headers["Content-Type"] = "application/json";
    }
    return config;
  },
  (err) => {
    // 加载动画关闭
    console.info("请求错误");
    return Promise.reject(err);
  }
);

// 响应拦截器
axios.interceptors.response.use(
  (res) => {
    // 关闭动画，一些公共的错误，可以在这里处理。
    if (res.errorCode !== "0") {
      console.info("返回失败", res);
    }
    return Promise.resolve(res.data);
  },
  (err) => {
    // 关闭动画
    console.info("返回错误");
    return Promise.reject(err);
  }
);
export default axios;
// ...main.js将其绑定到原型上：vue.protetype.$rpc = axios;
```

**返回的内容**：`{config:{},data:{},headers:{},request:{},status:200,statusText:'ok'}`

- config 中包括设置 axios 时的 url、请求方式、headers、baseUrl 等。
- data 是服务端返回的数据内容。
- headres 是请求中使用的头部内容。
- request：包含 custom、onerror、onabort 等。

**调用**：

```js
// 这两个方法不支持then回调，一般封装到promise中。
axios.post(url, data, { params: { a: 1, b: 2 } });
axios.gt(url, { params: { a: 1, b: 4 } });
//===params中的键值对会被拼接到url后。
axios.request({
  url: "",
  method: "POST",
  data: {},
  session: true, // 自定义值，请求拦截器、响应拦截器，中都能拿到。
  params: { token: 1234 },
});
```

[axios 配置，学习地址。](https://www.cnblogs.com/mica/p/10795242.html)

## 14、NUXTJS：

:::alert-info
**ssr 实现原理**：ssr 有两个入口文件，client.js 和 server.js 。webpack 通过两个入口文件分别打包成给服务端用的 server bundle 和给客户端用的 client bundle。当服务端接受到来自客户端的请求后，会创建一个渲染器 bundleRender, 这个 bundleRenderer 会读取上面生成的 server bundle 文件，并且执行它的代码，然后发送一个生成好的 html 到浏览器，等客户端加载了 client bundle 之后，会和服务端生成的 DOM 进行 Hydration (判断这个 DOM 和自己即将生成的 DOM 是否相同，如果相同就是将客户端的 vue 实例挂载到这个 DOM 上，否则会提示警告)。一般只做首屏渲染。
:::
模板：在项目跟目录新建一个 app.html 模板，可被用于最后生成的 html 文件。默认模板如下：

```html
<!DOCTYPE html>
<html {{ HTML_ATTRS }}>
  <head {{ HEAD_ATTRS }}>
    {{ HEAD }}
  </head>
  <body {{ BODY_ATTRS }}>
    {{ APP }}
  </body>
</html>
```

**layouts**：该目录下的页面相当于普通 vue 项目中的 APP.vue 最外层 vue 页面，所以需要在页面中放置一个<Nuxt/>加载其它页面的标签。当然在 layouts 中放置 error 页面之类的可不用
components：该目录下的为组件，各页面中不用导入，注册，直接按照组件文件名称使用即可。
**plugins**：对应的是 vue 中使用的 plugin，无论是自定义的还是第三方的都可以放置在 plugins 目录下，然后 nuxt.config 中配置使用。例如：plugins 下建立一个 axios 全局配置的 js 文件，其它文件直接引用即可。

```js
//-----plugins/element-ui.js内容如下：
import Vue from "vue";
import Element from "element-ui";
Vue.use(Element);

//-----nuxt.js内容如下：
module.exports = {
  plugins: [
    {
      src: "@/plugins/element-ui", //src指定文件地址。
      ssr: true, //若为false时则只会在客户端被打包引入，为true则会直接在服务端渲染。
    },
  ],
};
```

**路由**：nuxt 会自动根据 pages 下的结构转为路由，示例如下：！路由的跳转方法不变。

- pages/index.vue =>变为`{name:"index",path:"/"}`。
- pages/user/index.vue =>变为`{name:"user",path:"/user"}`#index 文件名不计。
- pages/user/cord.vue =>变为`{name:"user-cord",path:"/user/cord"}`。
- pages/user/\_id.vue =>变为`{name:"user-id",path:"user/:id"}`#下划线会变为动态路由标志。且文件名变为参数名。
  loading：有一个默认的顶部进度条加载动画，在 nuxt.config.js 中设置 loading:false 可以将其关闭，当然也可以是一个字典定义进度条的一些外观。也可以自己定制一个加载动画页面，然后`loading:'~/components/loading.vue'`使用。

```js
export default {
  mounted() {
    //使用$nextTick()函数<用于延迟执行一段代码>，确保loading被调用。
    this.$nextTick(() => {
      this.$nuxt.$loading.start();
    });

    setTimeout(() => {
      this.$nuxt.$loading.finish();
    }, 1000);
  },
};
```

**middleware**：该目录用于存放中间件，中间件允许您定义一个自定义函数运行在一个页面或一组页面渲染之前。

```js
//middleware/state.js内容：
export default function ({ req, redirect, route }) {
  if (req.adfgasd) {
    if (req.url === "/") {
      return redirect("/homepage"); //重定向路径。
    }
  }
}

//nuxt.config.js内容：
module.exports = {
  //...,路由变化时使用中间件。
  router: {
    middleware: "stats", //stats对应文件名。
  },
};
```

store：该目录下存放 vuex 文件，像平常一样建立，使用即可。
**额外的键**：nuxt 提供的一些 vue 框架之外的键，如下：

```js
export default {
  //asyncData在组件化之前调用，可在这里做数据请求，return或callback返回的值会与data中的合并。
  asyncData({ params, req, res, error }, callback) {
    //params可获取上个页面传来的参数。
    if (params.name) {
      callback(null, { message: "success" });
    } // 或者return {message:"success"}也是一样的。
    else {
      // 显示错误页面（layouts目录下的error.vue页面）。
      error({ statusCode: 404, message: "Post not found" }); //或者callback({ statusCode: 404, message: 'Post not found' })
    }
  },
  //用于在渲染页面之前获取数据填充应用的状态树,不会设置组件的数据。
  async fetch({ store, params }) {
    //store为vuex中的对象。
    await store.dispatch("GET_STARS");
  },
  //	配置当前页面的 Meta 标签等。
  head() {
    return {
      title: this.title,
      meta: [{ hid: "description" }],
    };
  },
};
```

[参考学习地址。](https://segmentfault.com/a/1190000021050814?utm_source=tag-newest)、[NUXTJS 中文网。](https://www.nuxtjs.cn/guide/configuration)、[nuxt 部署](https://www.jianshu.com/p/bbe874c32f90)

## 16、提交代码时检查：

- 简介：husky 是 git 的一个钩子，可以在 git 的 hook 中执行一些命令。使用的是 eslint 检查。prettier 可配置 vscode 格式化方式。lint-staged 对 git 暂存的文件进行 lint 检查。提交时对暂存的代码用 eslint 规则检查，出现 error 的话会禁止提交。
- 安装：cnpm install --save-dev prettier husky lint-staged eslint
- [学习地址](https://blog.csdn.net/Jsoning/article/details/103577402)。[prettierpeiz 官网](https://prettier.io/docs/en/options.html)。

package.json 配置如下：可在 scripts 中添加：`"lint": "eslint --ext .js,.vue src"`#这样来单独运行检查文件。

```json
{
  "husky": {
    "hooks": {
      "pre-commit": "lint-staged"
    }
  },
  "lint-staged": {
    "src/**": [
      "prettier --config prettier.config.js --write",
      "eslint --fix",
      "git add"
    ]
  }
}
```

**eslint 配置**：常用如下

```js
module.exports = {
  rules: {
    indent: [1, "tab"], //缩进，等价于[1,2]#2表示缩进字符个数。
    quotes: [1, "double"], //引号使用：2表示error，1表示warning。单引号single
    semi: [1, "always"], //分号结尾，/nenver。
    "vue/html-indent": [
      "error",
      "tab", //vue页html元素的缩进，默认使用2个空格。
      {
        attribute: 1,
        baseIndent: 1,
        closeBracket: 0,
        alignAttributesVertically: true,
        ignores: [],
      },
    ],
  },
  //一些定义了全局的变量，这样这些变量不会被检测为未定义。
  globals: {
    app: true,
    AlipayJSBridge: true,
    process: true,
  },
};
```

- **问题集**：可以鼠标放在提示错误的地方，点击`Peek Problem`，然后点击规则`eslint(...)`，跳到该规则相应的配置介绍，去学习它的使用。
- 提示一些规则没有找到（顶部红色波浪线）：该版本没有对应的规则支持，尝试升级版本。
- [eslint 配置大全。](https://blog.csdn.net/p358278505/article/details/77429251)

## 18、html2canvas 使用：

用于将页面的 html 节点转化为图片，注意若其中包含图片，使用 img 标签而不要使用背景图。否则生成的图片不清晰。

```js
import html2canvas from "html2canvas";
const _el = document.getElementById("img");
new html2canvas(_el, {
  scale: 3, //缩放数，大于1表示生成高清。
  backgroundColor: "#fff",
  allowTaint: true, //允许跨域
  useCORS: true,
  height: 100,
  width: 200,
  scrollY: 0,
  scrollX: 0,
}).then((canvas) => {
  // canvas为转换后的Canvas对象
  let oImg = new Image();
  oImg.src = canvas.toDataURL(); // 导出图片
});
```

## 19、nginx：

:::alert-info
**简介**：是一个高性能的 HTTP 和反向代理 web 服务器，同时也提供了 IMAP/POP3/SMTP 服务。Nginx 是一款轻量级的 Web 服务器/反向代理服务器及电子邮件（IMAP/POP3）代理服务器，在 BSD-like 协议下发行。其特点是占有内存少，并发能力强，事实上 nginx 的并发能力在同类型的网页服务器中表现较好。
:::

- 安装：解压后进入目录，sudo ./configure 运行配置生成 Makefile 文件，当前目录下再 make,make install 编译安装，在/usr/local 下会出现 nginx 目录。
- 配置如下：似乎新版 nginx 默认支持

```js
#工作模式及连接数上限
events {
    worker_connections 1024;    #单个后台worker process进程的最大并发链接数
}

#设定http服务器，利用它的反向代理功能提供负载均衡支持
http {
    # 可配置多个server
    server {
        listen 443;     # 监听本机所有ip上的 443 端口
        listen 80;      # 可设置监听多个端口
        server_name  aa.xx.com; # 域名地址

        #反向代理的路径（和upstream绑定），location 后面设置映射的路径
        location / {
            proxy_pass http://zp_server1;
        }
        # -----root作用：使用了root时，实际路径是：访问路径/root路径。如：http://localhost/bank,->http://localhost/bank/html->访问D:/.../bank/html下文件。
        location /bank/page/ {
            root html;//实际寻找路径：http://localhost/bank/page/html
            #alias D:\WEB\dist; #别名使用的路径,不与root使用。
            try_files $uri $uri/ /bank;
        },
        #文件服务写法：
        #-----alias作用：url路径与本地寻文件路径不影响。
        location /download {
            autoindex on;# 显示目录
            autoindex_exact_size on;# 显示文件大小
            autoindex_localtime on;# 显示文件时间
            alias D:\\download;//访问路径变化：http://localhost/download->访问D:\Download
        }
        # 配置多个webapp时location后面的路径与前端配置的history的base路径一致。
        location /bank2/page/ {
            try_files $uri $uri/ /bank2;
        }

        error_page  500 502 503 504  /502.html;
        location = /50x.html {
            root   html;
        }
    }
}
```

- [windows 端下载地址](http://nginx.org/en/download.html)
- [参考地址 1](https://www.cnblogs.com/goloving/p/13501265.html)、[配置学习地址](https://www.cnblogs.com/jingmoxukong/p/5945200.html)

# 五、android 和 ios：

**h5 在两端的兼容性问题**：

1. **时间兼容性**：将时间转换为时间戳时，ios 端得到 NaN 问题。解决：安卓用 Date.parse(new Date('2018-03-30 12:00:00'))，iosDate.parse(new Date('2018/03/30 12:00:00'))。
2. **input 框聚焦**：有时候，ios 有时候会出现 outline 或者阴影，安卓则是显示正常的。解决：`input:focus{outline:none} input:{-webkit-appearance: none;}`
3. input 输入框的 placeholder：也就是输入框的提示性文字。会出现不在输入框的中间位置，导致位置偏上。解决：`line-height：normal`
4. 安卓手机可以点击图片：解决：用 img{ pointer-events: none; }来禁止。
5. 键盘挡住下方输入框问题：解决：用`document.querySelector('#inputId').scrollIntoView();`选中对应元素滚动到可视范围。

- [参考地址 1](https://zhuanlan.zhihu.com/p/83969781)。[参考地址 2](https://zhuanlan.zhihu.com/p/47584892)。

**java/ios与js的交互原理**：Android的webview是基于webkit内核的,**webview中集成了js与java互调的接口函数**,通过addJavas criptInterface方法,==可以将Java的类注册进webkit==,给网页上的js进行调用,而且还可以通过loadUrl方法是给webkit传递一个URL,供浏览器来进行解析,实现Java和js交互
# 六、typescript：

1. **基础类型**：在变量名后声明其类型。<b c=r>声明的变量类型是用小写的，不然某些情况编译不通过。</b>

```ts
let x: [string, number];//声明一个可以有多种类型的元组变量。(元组各元素类型不必相同)
let decLiteral: number = 6;
let isDone: boolean = false;
let list: number[] = [1, 2, 3];//数组写法
let list: Array<number> = [1, 2, 3];
let notSure: any = 4;//any表示可以是任意类型。
//默认情况下null和undefined是所有类型的子类型。 就是说你可以把null和undefined赋值给number类型的变量。
let u: undefined = undefined;
let n: null = null;
//用枚举，可作为变量的类型。
enum Color {Red, Green, Blue}
let c: Color = Color.Green;
//>>>>>>>>>>>>!使用
let y:number
y = null! //用在值后可以让不符合的类型编译通过。
/*========================
    未知对象类型使用,不要使用object
==========================*/
var cc:Record<string:unknow>;
//-----------数值连接字符串：直接使用+或模板字符串连接会报错。
let res:string = decLiteral.toString().concat(str);
//interface用于创建一个类型要求例子，可以公共调用。
/*==================
        自定义类型
====================*/
interface LabelledValue {
  readonly label: string;//对象必须含有该键值。readonly表示该属性只读。
  color?: string;//带?号表示可选，在判断使用时会有一些友好的提示。
}
/*==================
        map方法
====================*/
let myMap = new Map();
myMap.set("key",value); //set(),clear(),delete(),size()等方法
```

2. **函数**：

```ts
//参数是函数时，参数函数也要定义类型
interface fn1 {
  (): void;
}
//有返回值的函数也是如此
function warnUser(): string {
  return "hello";
}
//void类型像是与any类型相反，它表示没有任何类型。
function warnUser(a: number | string): void {
  //参数也需要定义类型。
  alert(a);
}
//never类型是那些总是会抛出异常或根本就不会有返回值的函数表达式或箭头函数表达式的返回值类型
function error(message: string): never {
  throw new Error(message);
}

function printLabel(labelledObj: LabelledValue) {
  console.log(labelledObj.label);
}
//泛型变量：传给函数什么类型，函数就返回什么类型。
function identity<T>(arg: T): T {
  return arg;
}

function test(fn: fn1): void {
  fn();
}
```

3. **枚举**：

```ts
enum FileAccess {
  // constant members
  None,
  Read = 1 << 1,
  Write = 1 << 2,
  ReadWrite = Read | Write,
  // computed member
  G = "123".length,
}
//常数枚举写法
const enum Enum {
  A = 1,
  B = A * 2,
}
```

4. **类**：与 es6 的写法大致一致

```ts
class Animal {
  public a: string = "11"; //默认都是public
  private name: string; //private将变量设为私有
  //这是构造函数，这些参数能在继承时作为接收参数使用。使用的protected表示被保护，不能直接用new继承这个类。
  protected constructor(theName: string) {
    this.name = "hh";
  }
}

class dog extends Animal {
  //构造函数内调用super()这样，子类中也可以使用this指针。
  constructor(name: string) {
    super(name);
  }
  move(distanceInMeters = 45) {
    console.log("Galloping...");
    super.move(distanceInMeters);
  }
}
```

5. **装饰器**：是一个方法，可以注入到类或类的方法、属性参数上来扩展类、属性、方法、参数的功能。<b c=r>只用于类或其中</b>。[更多学习地址。](https://blog.csdn.net/weixin_33928467/article/details/87963596)

```ts
//>>>>>>>>>>>>>>>>>>普通装饰器，无法传参。
function logClass(params: any) {
  //params就是当前类
  console.log(params); //f HttpClient() {}
  params.prototype.apiUrl = "xxxx"; //相当于动态扩展的属性
  params.prototype.run = function () {
    console.log("run");
  };
}
@logClass
class HttpClient {
  //将该类作为上面的params参数
  constructor(name: string) {
    console.info(name);
  }
}
//>>>>>>>>>>>>>>可传参的装饰器，装饰器传的参数是params，而修饰的类时target参数
function logClass2(params: string) {
  return function (target: any) {
    //需要返回一个函数用于接收装饰的类。
    target.prototype.apiUrl = params; //相当于动态扩展的属性
  };
}
@logClass2("http://www.abc.com")
class HttpClient {
  constructor(name: string) {
    console.info(name);
  }
}
const cc = new HttpClient("wcs");
//>>>>>>>>>>>>>>>属性装饰器，用于类内部的变量装饰。
function logProperty(params: any) {
  //params是装饰器传入的参数，target是所在类，attr是修饰的对象。
  return function (target: any, attr: any) {
    console.log(target); //{getData:f,constructor:f}
    console.log(attr); //url
    target[attr] = params;
  };
}
class HttpClient {
  @logProperty("http://www.abc.com") //属性装饰器后面不能加分号，该值赋给url。
  public url: any | undefined;
  constructor() {
    console.log(134);
  }
  getData() {
    console.log(this.url);
  }
}
let cn = new HttpClient();
cn.getData(); //http://www.abc.com
//>>>>>>>>>>>>>>>>>类方法装饰器
function get(params: any) {
  return function (target: any, methodName: any, desc: any) {
    //params是装饰器传入的参数，target是所在原型，methodName是修饰的方法名，desc是修饰的方法的描述。
    target.apiUrl = params;
  };
}
class HttpClient {
  public url: any | undefined;
  constructor() {
    console.info("init");
  }
  @get("http://www.abc.com")
  getData() {
    console.log(this.url);
  }
}
let http = new HttpClient();
```

6. **ts 中使用 js 库**：

- 安装第三方 js 库，如 jquery：[安装 jquery](https://www.cnblogs.com/juliazhang/p/10103985.html)

```js
npm install jquery --save; //安装jquery
npm install @types/jquery --save-dev; //jquery的类型定义文件，node_modules/@types/jquery下。
// tsconfig.js的types中加入jquery，可全局使用。
"types": ["jquery"];
// 使用：
<script lang="ts">
import jquery from "jquery";
jquery("#id");
</script>
```

- **自定义 js 导入**：编写对应 js 文件的类型定义文件（.d.ts），使用处导入定义文件，html 文件导入对应 js 文件。

```js
//cool.d.ts 类型声明文件：
declare module Runoob {
  export class Calc {
     doSum(limit:number) : number;
  }
}
//home.vue页面引入：
<script lang="ts">
//js部分引入类型定义文件，【注意前面3个斜杆！】
/// <reference path="../assets/cool.d.ts" />
var obj = new Runoob.Calc();    //使用,【重运行服务后，报错提示可去除】
</script>
//index.html文件,引入使用
<script src="/assets/cool.js"></script>
```

7. **模块**：与 es6 的几乎一致

```ts
export cosnt ak: number = 3489;
export * from "./StringValidator";
//一个文件只能有一个default
declare let $:JQuery;
export default $;//另一个文件import $ from "JQuery";使用。
```

[typescript 中文档](https://www.tslang.cn/docs/handbook/decorators.html)。[菜鸟教程](https://www.runoob.com/typescript/ts-ambient.html)。[tsconfig.js](https://segmentfault.com/a/1190000021749847)

# 七、测试：

单元测试：对软件中的最小可测试单元进行检查和验证。
功能测试：对产品的各功能进行验证。
集成测试：在单元测试的基础上，将所有模块按照设计要求（如根据结构图）组装成为子系统或系统，进行集成测试。

**1、jest 做单元测试**：[jest 中文档](https://www.jestjs.cn/docs/getting-started)

- 安装：
  （1）全局安装：`npm install jest -g`
  （2）初始化一个配置：`jest --init` #项目下会生成一个 Jest.config.js 配置文件。
  （3）命令指定配置：自定义配置文件使用。需要注意与 babel 版本有关，一下是一个合适版本的组合。

```json
{
  "scripts": {
    "test": "jest --config test/config.js"
  },
  "devDependencies": {
    "babel-core": "^6.22.1",
    "babel-helper-vue-jsx-merge-props": "^2.0.3",
    "babel-jest": "^21.0.2",
    "babel-loader": "^7.1.1",
    "babel-preset-env": "^1.3.2",
    "babel-preset-stage-2": "^6.22.0",
    "babel-register": "^6.22.0",
    "jest": "^22.0.4",
    "jest-serializer-vue": "^0.3.0"
  }
}
```

（4）项目也安装：`npm install -D jest`。

- 配置文件：[配置文档地址](https://jestjs.io/docs/expect#expectvalue)

```js
module.exports = {
  clearMocks: true,
  // Indicates whether the coverage information should be collected while executing the test
  collectCoverage: true,
  coverageDirectory: "coverage",
  coverageProvider: "v8",
  testEnvironment: "node", //测试脚本所在环境，js-dom为六浏览器环境。
  testMatch: [
    "**/__tests__/**/*.js", //设置匹配测试用的脚本文件，默认放在：跟目录/__tests__/sj.js
    "**/?(*.)+(spec|test).[tj]s?(x)",
  ],
};
```

- **错误集**：
  > jest SecurityError: localStorage is not available..：配置文件中将环境改为 node 即可，`testEnvironment: "node"`。

**2、mock 数据做测试**：mock 也可用作直观的测试使用。

1. 使用 mockjs

- 安装：npm i mockjs -D。建立一个放置数据的目录，用 json 文件存放数据，新建一个 mock.js 文件。
- mock.js 文件配置请求的路径和对应的数据：

```js
const Mock = require("mockjs");
const _url = "https://nb.com"; //如果使用了axios，这里路径要与axios配置的baseUrl一致。
//请求路径、请求类型、数据。
Mock.mock(`${_url}/index/test`, "get", require("./moc.json"));
Mock.mock(`${_url}/index/use`, "post", require("./moc.json"));
```

- **导入**：main.js 将其导入即可。使用 mock 数据时**不要与代理路径一样，或干脆不用代理**。

```js
// 使用环境判断，开发时才导入
if (process.env.NODE_ENV !== "production") {
  require("@/mock");
}
```

2. 利用 ajax 可请求文件的方法。
3. 使用 node 在开一个本地服务用于返回 mock 数据，让代理目标地址更改为该服务地址。
   [使用本地 mock 数据。](https://blog.csdn.net/zhushikezhang/article/details/104447438)
   **mock 与测试环境切换**：可以在运行命令多添加一个参数，用于判断是否 mock 环境。
   `"dev:mock": "cross-env DEV_ENV=mock webpack-dev-server --inline --progress --config build/webpack.dev.conf.js mock"`
   config/index.js 文件中检测环境，修改 url，然后 axios 配置文件中使用该文件的 url，mock.js 文件中的地址写为固定即可。

```js
// process.argv获取传入的所有参数。
if (process.env.DEV_ENV === "mock") {
  // mock数据地址。
  url = "http://mock_test.com";
} else if (process.env.DEV_ENV === "sit") {
  // 测试环境
  url = "http://test_env.com";
} else {
  // 正式环境
  url = "http://127.0.0.1:3000";
}

module.exports = {
  dev: { url: url },
};
```

**3、e2e 测试**：把整个系统当作一个黑盒，测试人员模拟真实用户在浏览器中操作 UI，测试出的问题可能是前端也可能是后端导致的。
**cypress**：

- 安装：npm install cypress --save-dev，项目下自动生成 cypress 文件夹。
- 运行：script 添加运行命令："test:view": "cypress open"，npm run test:view 打开 cypress 测试界面。
- [cypress 英文档](https://docs.cypress.io/guides/overview/why-cypress)

# 八、华为鸿蒙：

1. 系统层次：[文档学习地址](https://developer.harmonyos.com/cn/docs/documentation/doc-guides/ability-service-lifecycle-0000000000044472)

- 内核层（进程/线程管理、内存管理、文件系统、网络外设管理等）。
- 服务层：
  （1）分布式任务调度：基于分布式软总线和分布式数据管理，可对设备应用进行远程调用、远程启用、远程连接等操作；
  （2）分布式数据管理：（属于框架层）对数据流动时对数据分类、分级保证使用数据正确。对数据生成、存储等各生命周期保护，保证数据安全。支持多设备下的数据存储、共享、访问；
  （3）分布式软总线：（任务总线和数据总线）多设备互联、自发现连接、为设备之间的无感发现和零等待传输创造了条件。
  （4）分布式设备虚拟化：可以实现不同设备的资源融合、设备管理、数据处理，多种设备共同形成一个超级虚拟终端。
  （4）基础软件服务子系统：事件通知服务子系统、电话服务子系统、多媒体子系统、DFX 子系统、MSDP&DV 子系统。
- 框架层：UI 框架，可 java/js 语言、用户程序框架，支持 c/c++/java/js、多种语言框架 api、ability 框架。
- 应用层：应用部署（根据硬件形态和需求可选择所需组件、根据硬件资源情况和功能需求，选择配置组件中的功能集、根据编译链关系自动生成组件依赖关系）。
- DVID： 分布式虚拟设备标识符。设备登录了 HarmonyOS 账号后，应用程序信息生成分布式虚拟设备 ID。
  > 场景一：应用程序一键式登录。场景二：应用程序管理多设备
- UUID：应用在其生命周期内可以用该标识唯一识别相同设备。应用使用情况统计分析。（当应用卸载后该标识销毁。再次重新安装后调用获取 UUID 接口时会重新生成不同的 ID）

2. 开发：安装华为 IDE 工具，下载 SDK，新建一个 app 项目：一个 app 只有一个 entry 类

- entry/src/main/resource
  代码部分：

```java
/*部分文件目录
Resource/
--base/
---layout/    //存放布局文件。java中用ResourceTable.Layout_前缀调用
---graphic/   //作为背景使用
---media/     //存放图片，java中用ResourceTable.Media_前缀调用
java/
--com/
----ttjy/
------stxd/
- - - --a.java            //这是一个java ability
- - - --b.java
--------slice/
- - - - - -PaySlice.java    //PaySlice.java是a.java的一个子ability，一般在这个页面绘制java ui界面
--------util/
- - - - - -c.java
*/

/*==========================
slice/PaySlice.java文件（java page）        文件所属模块：包名相同的文件，其文件所有公共类，在其它文件可直接使用。将其它项目文件拷贝过来时，记得更改这里
=========================*/
package com.ttjy.stxd.slice;

import com.ccb.paycard.ResourceTable;
import ohos.aafwk.ability.AbilitySlice;
import ohos.aafwk.content.Intent;
import ohos.aafwk.content.Operation;
// 日志部分
import ohos.hiviewdfx.HiLog;
import ohos.hiviewdfx.HiLogLabel;
// 布局部分
import ohos.agp.components.Image;
import ohos.agp.components.Component;
import com.ttjy.stxd.slice.Success;
import com.ttjy.stxd.MainAbility;

public class PaySlice extends AbilitySlice {
    private static final HiLogLabel LABEL = new HiLogLabel(HiLog.LOG_APP, 0x230, "MY_TAG");    //建立日志
    @Override
    public void onStart(Intent intent) {
        super.onStart(intent);
        super.setUIContent(ResourceTable.Layout_pay);                                          //设置使用的布局xml文件
        // 获取intent的参数值，还有getBoolParam,getIntParam()等方法
        String formOrder = intent.getStringParam("formOrder");
        findComponentById(ResourceTable.Id_header_back).setClickedListener(this::goBack);      //绑定点击事件
        // 在选中元素前加类型，得到对应的元素类，这样才能使用相应类下的函数。
        Image lonImg = (Image) findComponentById(ResourceTable.Id_radio_img);
        lonImg.setPixelMap(ResourceTable.Media_checked);                                       //设置图片
    }
    public void goBack(Component v){ terminate();}                                             //页面返回
    public toSuccess(){
        Intent itt = new Intent();itt.setParam("res","justice");
        present(new Success(),itt);                                                            //page内跳转方法
    }
    public void goHome(Component v){
        Intent intent = new Intent();
        Operation operation = new Intent.OperationBuilder().withDeviceId("")
        .withBundleName(getBundleName()).withAbilityName(MainAbility.class.getName()).build();
        intent.setOperation(operation);startAbility(intent);                                   //不同ability间的跳转。
    }
}
/*===========================
    b.java文件，service
=============================*/
package com.ttjy.stxd;

public class ComputeServiceAbility extends Ability {
    private MyRemote remote = new MyRemote();
    // FA在请求PA服务时会调用Ability.connectAbility连接PA，连接成功后，需要在onConnect返回一个remote对象，供FA向PA发送消息
    @Override
    protected IRemoteObject onConnect(Intent intent) {
        super.onConnect(intent);
        return remote.asObject();
    }
    // 远程链接类
    class MyRemote extends RemoteObject implements IRemoteBroker {
        private static final int PLUS = 1001;
        MyRemote() {super("MyService_MyRemote");}
        // 调用监听
        @Override
        public boolean onRemoteRequest(int code, MessageParcel data, MessageParcel reply, MessageOption option) {
            switch (code) {
                case PLUS: {
                    /*结果返回*/
                    Map<String, Object> result = new HashMap<String, Object>();
                    result.put("code", 0);
                    result.put("abilityResult", 20);
                    reply.writeString(ZSONObject.toZSONString(result));            //回复js结果。
                    break;
                }
            }
        }
    }
}
```

js 页面代码：

```js
export default {
  // js FA调用java PA
  async js2java() {
    // 向java PA传输的参数
    var actionData = {};
    actionData.firstNum = 1024;
    actionData.secondNum = 2048;
    // 必须先声明map，再向其中添加数据，不然无法调用
    var action = {};
    action.bundleName = "com.ttjy.stxd";
    action.abilityName = "com.ttjy.stxd.b";
    action.messageCode = ACTION_MESSAGE_CODE_PLUS;
    action.data = actionData;
    action.abilityType = ABILITY_TYPE_EXTERNAL;
    action.syncOption = ACTION_SYNC;

    // 调用PA能力
    var result = await FeatureAbility.callAbility(action);
    var ret = JSON.parse(result);

    this.money = ret.abilityResult;
  },
};
```

配置部分：

```js
{
  //app: "全局配置信息",（最外层大致有哪些要记）
  "app": { "bundleName": "com.example.phonedemo","vendor": "example","version": {}},
  "deviceConfig": {},//设备恢复、网络安全等
   //HAP包配置信息
  "module": {
    //自定义权限申请,（内部字段要记）
    "defPermissions":{
        "name":"come.myability.permision.MYPERMISION",//记住格式
        "grantMode":"system_grant",
        "avaliableScope":["signature"]
    },
    "package": "com.ttjy.stxd",//应用包名，唯一
    "name": ".MyApplication",
    "mainAbility": "com.ttjy.stxd.a",
    "deviceType": ["phone"],
    "abilities": [{
        // 入口页面，entity.system.home表示入口页面。
        "skills": [
          {
            "entities": [
              "entity.system.home"
            ],
            "actions": [
              "action.system.home"
            ]
          }
        ],
        "visible": true,
        "name": "com.ttjy.stxd.a",
        "icon": "$media:icon",
        "description": "$string:mainability_description",
        "label": "$string:entry_MainAbility",
        "type": "page",
        "launchType": "standard",
        "metaData": {
          "customizeData": [{
            "name": "hwc-theme",
            "value": "androidhwext:style/Theme.Emui.Light.NoTitleBar" //去掉页面顶部标题
          }]
        }
    },{
        "name": "com.ttjy.stxd.b",
        "icon": "$media:icon",
        "description": "$string:skippay_description",
        "type": "service"   //一个service ability
      },],
    //对权限进行逐个声明（部分非敏感权限）。敏感权限（通讯录、位置等）需要代码中动态申请
    "reqPermissions":{},
    //jsUI应用时，使用使用web来构建页面
    "js": [
      {
        "pages": ["pages/index/index"],
        "name": "default",
      }
    ]
  }
}
```

**NFC 功能**：

1. NFC 基础查询：在进行 NFC 功能开发之前，开发者应该先确认设备是否支持 NFC 功能、NFC 是否打开等基本信息。
2. 访问安全单元（Secure Element，简称为 SE）：SE 可用于保存重要信息，应用可以访问指定 SE，并发送数据到 SE 上。
3. 卡模拟：设备可以模拟卡片，替代卡片完成对应操作，如模拟门禁卡、公交卡等。
4. NFC 消息通知：通过这个模块，开发者可以获取 NFC 开关状态改变的消息以及 NFC 的场强消息。

**界面 ui**：界面元素由**组件**和**布局**构成。可用 xml 布局和 java 代码布局。【javascript ui 框架属于应用层】

- 组件：绘制在屏幕上的一个对象。Component（界面中所有组件的基类）。
  > 常用：（1）Text：、Image、Clock、TickTimer、ProgressBar。
- 布局：容纳其它组件和布局的容器。ComponentContainer（容器，容纳 Component 和其它 ComponentContainer）。
  > 常用：PositionLayout、DirectionalLayout（水平垂直布局）、StackLayout（层叠布局，用`moveChildToFront`可将子视图移到顶层）、DependentLayout（相对于其它元素定位）、TableLayout（表格布局）、AdaptiveBoxLayout 等。

```xml
<!--=========background_button.xml==========-->
<?xml version="1.0" encoding="utf-8"?>
<shape xmlns:ohos="http://schemas.huawei.com/res/ohos" ohos:shape="oval">
    <corners ohos:radius="10"/>
    <solid ohos:color="#007CFD"/>
</shape>
<!--===================
        另一个xml文件
=======================-->
<?xml version="1.0" encoding="utf-8"?>
<!--部分属性：
match_content：表示自适应内容大小
ohos:truncation_mode="ellipsis_at_middle"：表示文本超长时在文本框中间位置使用省略号截断。
$graphic:background_button：表示引用上面定义的xml文件中的样式。
ohos:scale_mode="zoom_center"：图像缩放类型。stretch、center（不缩放）、inside（原比列缩放）、clip_center等
ohos:alpha="0.5"：设置透明度。
Button,TextField都继承自Text组件。
-->
<DirectionalLayout
    xmlns:ohos="http://.."
    ohos:width="match_content"
    ohos:height="match_parent"
>
    <Text ohos:text="内容部分" ohos:text_alignment="center" ohos:truncation_mode="ellipsis_at_middle"/>
    <Button ohos:margin="20" ohos:background_element="$graphic:background_button"/>
    <Image
        ohos:id="$+id:imageComponent"
        ohos:height="200vp"
        ohos:width="200vp"
        ohos:alpha="0.5"
        ohos:scale_mode="zoom_center"
        />
<!--动画-->
    <animation-list xmlns:ohos="http://schemas.huawei.com/res/ohos" ohos:oneshot="false">
        <item ohos:element="$media:01" ohos:duration="100"/>
        <item ohos:element="$media:02" ohos:duration="100"/>
        <item ohos:element="$media:03" ohos:duration="100"/>
    </animation-list>
</DirectionalLayout>
```

- 动画：
  > 静态动画：核心是 transform 样式，主要可以实现以下三种变换类型，一次样式设置只能实现一种类型变换。translate、scale、rotate
  > 连续动画：静态动画只有开始状态和结束状态，没有中间状态，如果需要设置中间的过渡状态和转换效果，需要使用连续动画实现。连续动画的核心是 animation 样式，它定义了动画的开始状态、结束状态以及时间和速度的变化曲线。通过 animation 样式。

**Ability**：能力的抽象。功能、页面。

- **FA**：支持 page Ability，提供用户交互能力。`page Ability`，java 程序生命周期如下：

```java
package com.example.phonedemo;

import ohos.ace.ability.AceAbility;
import ohos.aafwk.content.Intent;
// page Ability生命周期
public class MainAbility extends AceAbility {
    @Override
    public void onStart(Intent intent) {}     // 首次创建page实列触发
    @Override
    public void onActive(Intent intent) {}    // 页面进入活跃状态时触发
    @Override
    public void onInactive() {}               // 页面失去焦点触发
    @Override
    public void onBackground() {}             // 页面不可见时触发
    @Override
    public void onForeground() {}             // 后台重新回到前台时
    @Override
    public void onStop() {super.onStop();}    // 销毁页面时触发
}
```

- AbilitySlice 间导航：
  > 同一 Page 内导航：
  > （1）当发起导航的 AbilitySlice 和导航目标的 AbilitySlice 处于**同一个 Page 时**，您可以通过`present()`方法实现导航。
  > （2）希望在用户从导航目标**AbilitySlice 返回**时，能够获得其返回结果，则应当使用`presentForResult()`实现导航。
  > （3）系统为每个 Page 维护了一个 AbilitySlice 实例的栈，每个进入前台的 AbilitySlice 实例均会**入栈**。当开发者在调用 present()或 presentForResult()时指定的 AbilitySlice 实例已经在栈中存在时，则栈中位于此实例之上的 AbilitySlice 均会**出栈**并终止其生命周期。

**PA**：`particle Ability`#支持 Service 模板（后台任务运行，service 中用`terminateAbility()`停止，其它用 stopAbility()停止）和 Data 模板（对外提供对数据的增、删、查、改，文件等）。

- service Ability ：后台运行程序。生命周期如下：terminateAbility()停止。
  > 启动类型的 service：`startAbility()`时创建、stopAbility()来停止。
  > 连接类型的 service：该 Service 在其他 Ability 调用`connectAbility()`时创建（可连接 startAbility 创建的）、disconnectAbility​()断开连接、onStop 停止。
- Data Ability：用于管理数据。

**Intent**：是对象之间传递信息的载体。例如，当一个 Ability 需要启动另一个 Ability 时，或者一个 AbilitySlice 需要导航到另一个 AbilitySlice 时，可以通过 Intent 指定启动的目标同时携带相关数据。

- 获取 intentAgent：`getIntentAgent`(Context context, IntentAgentInfo paramsInfo)
- 激发：triggerIntentAgent()触发通知。
- 取消：cancel(IntentAgent agent)取消一个 IntentAgent 实例。
- 常用场景：即时消息、广告 、导航

3. **管理**：
   **线程管理**：运行时，系统为应用启动一个主线程，所有 UI 操作都在主线程执行，所以也叫 UI 线程。

- 进程通信：通过`EventRunner`创建线程（可创建多个 EventHandler）。进程通信机制`EventHandler`（只能与一个 EventRunner 绑定。将`EventInner`和`Runnable`投递到其它线程进行处理）。EventHandler 创建的子类中通过重写 processEvent 来处理事件。
- EventRunner：有托管方式（系统自动调用 run(),stop()等方法控制）。手动方式（自己调用控制）。
- 任务分发器：TaskDispatch。
  > 分发器类型：GlobalTaskDispatch（全局并发任务分发器）、ParallelTaskDispatch（并发任务分发器）、SerialTaskDispatch（串型）、SpecTaskDispatch（专有）。
  > 任务派发方法：（1）SyncDispatch()：同步派发，使用不但可能死锁。（2）asyncDispatch()：异步派发。（3）delayDispatch()：异步延迟派发。（4）group()：成组派发。

**数据管理**：使用关系型数据库概念来增、删、查等操作数据。
（1）用`@Database`注解，继承 OrmDatabase 类，对应关系型数据库。
（2）用`@Entity`注解，继承 OrmObject，使用对应表。`Preference.flush()`#异步写入。`Preference.flushSync()`#同步写入。

- 关系型数据库，对象关系映射数据库都是基于 SQLite。轻量偏好数据库是 NoSQL 型数据库。

**网络管理**：数据连接管理、数据网络管理、流量统计、创建本地套接字。

- 需要权限：ohos.permission.GET_NETWORK_INFO（获取网络连接信息）、ohos.permission.SET_NETWORK_INFO（修改网络连接状态）、ohos.permission.INTERNET（允许网络连接）。
- 主要功能：数据连接管理：网卡绑定、数据链路参数查询、打开 url。数据网络管理、提供网络访问、socket 等 api。
- 连接方式：WLAN、蓝牙和 BLE、NFC（卡模拟）、电话服务。

```java
NetManager netManager = NetManager.getInstance(null);    //获取网络管理实列对象
NetHandle netHandle = netManager.getDefaultNet();        //获取默认数据网络
```

**日志管理**：5 种级别：DEBUGGER、INFO、WARN、INFO、ERROR、FATAL。

```java
static final HiLogLabel LABEL = new HiLogLabel(HiLog.LOG_APP,0X00201,"MY_TAG");
HiLog.warn("warn");//输出一条日志
```

调试：预览器、模拟器、真机。
**应用发布**：顺序如下：

1. 准备签名文件：生成密钥和证书请求文件、创建 AGC 项目、创建 HarmonyOS 应用、申请发布证书和 Profile 文件。
2. 编译构建 APP：配置签名信息、编译构建 App、
3. 上架应用市场

# 十一、webpack：

:::alert-info
**简介**：当项目变得很大之后再按照之前的资源引入方法会很难管理项目，不容易理清其依赖、加载顺序。webpack 能自动找到所有依赖，将它们按顺序都打到一个 js 包中，最后引入。用 Loader 转换文件、plugin 注入钩子。
**模块化规范**：commonJS：需要通过转换位 es5 才能在浏览器环境运行。AMD：异步方法加载依赖模块，用于解决浏览器环境模块化问题。现在使用 es6 也有模块化(但大部分浏览器还不支持)，也需要转换为 es5。
:::
**require 与 import 区别**：require 是赋值过程并且是运行时才执行，也就是异步加载。import 是解构过程并且是编译时执行，性能稍好。两者在 webpack 中都算是异步方案。

- require 属于 commonjs 规范的东西社区方案，提供了服务器/浏览器的模块加载方案。只能在**运行时确定模块的依赖关系**及输入/输出的变量，无法进行静态优化。
- import 是 es6 语法规范，可以解构，语言规格层面支持模块功能。支持编译时静态分析，便于 JS 引入宏和类型检验。动态绑定。

## a0、package.json

```js
{
  "name": "@jeecg/antd-online-mini",
  "version": "3.0.0-beta",
  // 导入该项目时，默认导入的文件，一般做依赖包时配置
  "main": "./dist/OnlineForm.umd.min.js",
  //可运行的命令项
  "scripts": {
    "serve": "vue-cli-service serve --open",
    "build": "vue-cli-service build",
  },
  "dependencies": {},
  "devDependencies": {},
}
```

## a1、原理：

Webpack 的构建流程可以分为以下三大阶段：在每个大阶段中又会发生很多事件，Webpack 会把这些事件广播出来供给 Plugin 使用。

- 初始化：启动构建，读取与合并配置参数，加载 Plugin，实例化 Compiler。
- 编译：从 Entry 发出，针对每个 Module 串行调用对应的 Loader 去翻译文件内容，再找到该 Module 依赖的 Module，递归地进行编译处理。
- 输出：对编译后的 Module 组合成 Chunk，把 Chunk 转换成文件，输出到文件系统。如果只执行一次构建，以上阶段将会按照顺序各执行一次。
- webpack 不会对多次引入的文件重复打包。

- [原理学习地址。](https://www.jianshu.com/p/44e6741e3b7e)[webpack 中文文档地址。](https://webpack.docschina.org/concepts/)

```js
//commonJS的导入导出。
const moduleA = require("./moduleA");
moduleA.exports = moduleA.someFun;

//AMD的模块定义，和导入使用。
define("module", ["dep"], function (dep) {
  return exports;
});
require(["module"], function (module) {});
```

**安装**：npm install webpack -g#全局安装。目录下使用：npm init#会在当前路径下生成一个 mypackage 文件夹，里面有 package.json 文件、webpack.config.js 文件和 src 文件夹。
**项目中使用别名**：可以在 build 目录下的配置文件中使用

```js
//例如/build/webpack.dev.conf.js配置如下
const merge = require("webpack-merge");
const baseWebpackConfig = require("./webpack.base.conf");
// merge将其它文件的配置合并过来。
const devWebpackConfig = merge(baseWebpackConfig, {
  resolve: {
    alias: { "@c": "src/common/tools" }, //别名对应路径。
  },
});
```

**配置**：[webpack 详细配置学习地址。](https://blog.csdn.net/c_kite/article/details/71279853)。[devserver 属性学习地址。](https://blog.csdn.net/franktaoge/article/details/80083317)

## a2、常用 loader：

- vue-loader：解析 vue 文件。
- css-loader：一般 vue-loader 解析过后结果 css-loader,处理过后会把样式都变成 module 形式，然后直接导出这个模块，模块中包含了 css 的源码跟模块的 id。
- style-loader：会引用 css-loader 生成的模块，然后在 Html 的 head 中加入 style 标签，当然也支持 link 引入等其它方式。
- vue-style-loader：在 style-loader 上的一层封装，不过还加了一些支持服务端的渲染。
- postcss-loader：把 CSS 解析成 JavaScript 可以操作的 AST，第二个就是调用插件来处理 AST 并得到结果，还能自动添加 css 前缀，如果要与 MiniCssExtractPlugin 的 loader 一起使用还要配置其它选项！。所以一般是放在 css-loader 之后，less-loader 等之前。
- less-loader,sass-loader,scss-loader：css 的预处理使用。scss 是 sass 的 3.0 版本引入的语法，去除了之前的一些严格规则，且规则与 css 一致。
- style-resource-loader：向样式文件中添加全局的样式属性。
- url-loader：用来为资源文件生成路径的。允许你有条件地将文件转换为内联的 base-64 URL。
- file-loader：可以指定要复制和放置资源文件的位置

```js
//这三个loader均可以类似如下配置。
module: {
  rules: [
    {
      test: /\.js$/, // 匹配指定的文件类型。
      //use: ['babel-loader?cacheDirectory'],//use指定对文件使用的插件，可以多项，配置规则。
      use: [
        {
          loader: "babel-loader", //指定使用的插件。
          options: {
            // 这里可以写.bablesrc中的格式配置。
            cacheDirectory: true,
          },
          // enforce:'post' 的含义是把该 Loader 的执行顺序放到最后。还可以是 pre，代表把 Loader 的执行顺序放到最前面
          enforce: "post",
        },
      ],
      // 只命中src目录里的js文件，加快 Webpack 搜索速度
      include: path.resolve(__dirname, "src"),
      exclude: /node_modules/, //指定不需要编译的目录。
    },
    {
      test: /\.less$/,
      use: [
        "vue-style-loader",
        { loader: "css-loader", options: { sourceMap: true } },
        { loader: "postcss-loader", options: { sourceMap: true } },
        { loader: "less-loader", options: { sourceMap: true } },
      ],
    },
    {
      test: /\.scss$/,
      use: [
        {
          loader: "style-resource-loader",
          options: { patterns: "全局样式文件路径" },
        },
      ],
    },
    {
      test: /\.(png|jpe?g|gif|svg)(\?.*)?$/,
      loader: "url-loader",
      options: {
        limit: 10000, //大小大于该值的交给file-loader处理。
        outputPath: "images", //打包后的输出路径
        name: utils.assetsPath("img/[name].[hash:7].[ext]"),
      },
    },
    {
      // 还能用file-loader来从js中抽离css用，
      test: /\.css$/,
      use: ["file-loader"],
    },
  ];
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
    background:url('~@/imgs/acc.jpg') 50% 0;/*背景图写法*/
    /deep/.ac{color:red;}
    /* 子组件的最外层编译后才会被加上scoped标志，而内部元素不会，若是使用了第三方组件库时，其样式
    会被全局的覆盖，此时可以用/deep/来改变。*/
}
/* >>>也和/deep/一样作用，不过只有普通css中可用*/
.k >>> .a{width:500px;}
</style>
```

## a21、自己编写 webpack-loader

loader文件：hello-loader.js （最后只使用此文件）

```js
// 每个文件都会调用一次该loader
module.exports = function loader(source) {
  // source文件的源码
  console.info(source);
  var cc = "hello loader！"
  // 返回处理后的结果
  return `export default ${ JSON.stringify(cc) }`;
};
```
入口文件：main.js

```js
// webpack根据导入的依赖，检测到此文件角给loader
import data from './test.hello';
function test() {
    // main.js中的代码也会被打包到最后的bundle.js
    let element = document.getElementById('app');
    console.log(data);
    element.innerText = data;
}
test();
```
webpack.config.js

```js
const path = require("path"); // node的方法

module.exports = {
  entry: "./src/main.js",
  //mode: "development",
  //target: "node",
  output: {
    // 导入文件配置，也是index.html 引入的
    filename: "bundle.js",
    path: path.resolve(__dirname, "output"),
  },
  module: {
    rules: [
      {
        test: /\.hello$/, // 需要加载的文件类型，正则匹配
        loader: path.resolve(__dirname, "./loader/hello-loader.js"), // 我们的loader文件
      },
    ],
  },
};
```

[参考地址 1](https://www.lmlphp.com/user/16516/article/item/464591/)
[参考地址 2](https://wenku.baidu.com/view/51088c0dccc789eb172ded630b1c59eef8c79a61.html)

## a3、常用的 Plugin：

<b c=b>plugin 在 loader 之后执行，目的在于解决 loader 无法实现的其他事。</b>。这些 plugin 除了 webpack 自带的，其它插件还是需要 npm 安装的。

- **DefinePlugin**：用于配置可用的全局变量。也可以额外 npm install -D dotenv 然后根目录下创建.env 文件编写，配置中使用 require('dotenv').config()，然后一样插件中配置。
- **HtmlWebpackPlugin**：根据原 html 文件配置，打包后生成一个 html 文件，里面可以配置一些生成明细相关。[详细参数](https://www.cnblogs.com/wonyun/p/6030090.html)。
- **CopyWebpackPlugin**：用于将指定文件放到编译或打包后的文件中去，然后 html 页面可以引入使用：`<script src="<%=htmlWebpackPlugin.options.prefix %>static/jquery.min.js"></script>`。然后单页内可直接使用$()方法。
- FriendlyErrorsPlugin：友好提示插件，允许 webpack 编译成功和失败后输出的信息。
- HotModuleReplacementPlugin：热更新使用插件。
- CommonsChunkPlugin：分离公共模块使用的插件，具体见 f。
- UglifyJsPlugin：用于压缩 js 代码。会拖慢编译速度，建议打包时使用。`npm install uglifyjs-webpack-plugin --save-dev`#需要安装
- ExtractTextPlugin：主要是为了抽离 css 样式,防止将样式打包在 js 中引起页面样式加载错乱的现象。

```js
const webpack = require('webpack')
const HtmlWebpackPlugin = require('html-webpack-plugin')
const CopyWebpackPlugin = require('copy-webpack-plugin')

// #####windows中使用set设置一个临时的环境变量
"dev": "set NODE_ENV=development &&  webpack-dev-server --open --hot"
// mac中使用：export
"dev": "export NODE_ENV=development &&  webpack-dev-server --open --hot",
// ————————为了统一两个系统，便于开发，使用一个第三方包:cross-env
"dev":"cross-env DEV_ENV=test webpack-dev-..."//注意cross-env要放在命令开头。
//但是运行程序中虽然能拿到变量名，但无法匹配到，进行如下设置：
//webpack.dev.conf.js的插件中.使用vue-cli-server还可以在最外层文件中添加环境变量。

module.exports = {
    ...
    plugins:[
        new webpack.DefinePlugin({
            'process.env':require('../config/dev.env'),//使用dev.env文件导出的环境变量。
            "process.env.DEV_ENV": JSON.stringify(process.env.DEV_ENV),//添加该项!!猜测其它地方如此使用也可。
        }),
        new HtmlWebpackPlugin({    //配置多页时需要使用多个该plugin。
            title:"测试app",//网页title，相应的html文件中使用<title><%= htmlWebpackPlugin.options.title %></title>才会有效
            filename: 'index.html',//输出后的名字
            template: '../src/index.html', //原html路径
            inject: true,//向template或者templateContent中注入所有静态资源
            chunks:'all' //指定导入的模块，多个写法》['vendor']
       }),
       new CopyWebpackPlugin([{    //一个数组的形式，所以可以写成多项。
        from: path.resolve(__dirname, '../static'),// from与to都可以是指定的文件或目录。
        to: 'static', //编译或打包后的项目下的目录。
        ignore: ['.*'] //可忽略匹配到的文件。
      }]),
      new UglifyJsPlugin({
        uglifyOptions: {
           compress: {
              warnings: false
           }
        },
        sourceMap: true,
        parallel: true
     }),
    ],
    modules:{
        rules:[{
            test: /\.css/,
            loader: ExtractTextPlugin.extract({
                use: ['css-loader'],
                fallback: 'vue-style-loader',
                publicPath: '../../'    //解决打包后背景图找不到问题。vue-cli脚手架的话在utils文件中添加。
            })
        }]
    }
}
//#-----dev.env文件如下内容
module.exports = {NODE_ENV:'"development"',NUM:'20'}//注意对应变量是字符串的话需要 '"字符串"',而'20'则该变量是数值。
```
## a3.1、实现1个plugin

```js
// plugin配置中引入使用文件即可
class CopyrightWebpackPlugin {
    constructor(options) {
        console.log('插件被使用了, 传入的参数为：'， options)
    }
    // 参数 compiler 是 webpack 的一个实例
    // compiler 存放着所有配置内容，包括所有打包的相关内容
    // compiler.hooks 定义了打包过程中的时刻值（钩子）
    // emit 时刻：将打包的资源输出到 输出目录(dist) 前,是一个异步的时刻值
    apply(compiler) {
        // compile 时刻是同步的时刻
        // 同步的时刻的参数中， 第二个方法参数只传一个 compilation 参数
        compiler.hooks.compile.tap('CopyrightWebpackPlugin', (compilation) => {
            console.log('compiler')
        })
        // compilation 存放着这一次打包的内容
        compiler.hooks.emit.tapAsync('CopyrightWebpackPlugin', (compilation, callback) => {
            // 打包生成的内容存放在compilation.assets
            // console.log(compilation.assets)
            // 打包输出前添加一个 copyright.txt 文件
            compilation.assets['copyright.txt'] = {
                source: function() {
                    return 'copyright output by plugin'
                }
                size: function() {
                    return 26
                }
            };
            // 使用 tapAsyns 时 最后一定要调用一下 callback
            callback()
        })
    }
}
​
module.exports = CopyrightWebpackPlugin;
```
## a5、resolve 与 output&魔术注释：

```js
/**三种hash的区别：（3种hash都是应对浏览器缓存而建立的）
hash：是跟整个项目的构建相关，只要项目里有文件更改，整个项目构建的hash值都会更改
chunkhash：只要我们不改动公共库的代码，就可以保证其哈希值不会受影响。
contenthash:
*/
{
    // 只能有一个output
    output:{
        filename:"[name].js",//为从入口处涉及到的bundle命名，name为占位，[fullhash]为使用hash。
        chunkFilename:"chunk[hash].js",//为按需加载类型的js命名。可以在路由处import给chunk命名。
        path:__dirname + '/dist',// 输出位置
        publicPath:"/" //各个资源路径前面添加的前缀。
    },
    // 项目中
    resolve:{
        extensions:['.js','.vue','.json'],
        alias:{'vue$':"vue/dist/vue.esm.js"}
    }
}

//-----路由配置
export default new Router({
    routes:[{
        path: '/textEdit',
        name: 'textEdit',
        //注释中为chunk命名。
        component: () =>
            import ( /*webpackChunkName:"wangeditor"*/  //可以多个路由命名为同一个名字，这样它们会被打包到同一个块。
                     /* webpackMode: "lazy" */
                     /* webpackPrefetch: true */ //这个是预先加载资源使用的注释。与 <link rel="prefetch"> 相同的特性
                     '../pages/textEdit.vue'),
        info: { login: true, title: "富文本编辑" }
    }]
});
```

- [其它注释学习参考地址。](https://webpack.js.org/api/module-methods/#magic-comments)

## a6、devtool：

为便于调试的设置。编译打包后的代码出错时难以找到编译前的位置调试，设置 devtool 可以让其找到编译前报错位置。

```js
{
  //有5个值：cheap,eval,module,inline,source-map。这些可以互相组合
  devtool: "cheap-module-eval-source-map";
}
```

- eval：不生成.js.map 文件，仅仅是在每一个模块后，增加 sourceURL 来关联模块处理前后对应的关系。
- source-map：打包后有 map 文件，相应的要在浏览器设置中开启：设置齿轮/preference/Sources/Eable javascript sources。
- inline：该属性不会生成独立的 .map 文件，而是将 .map 文件以 dataURL 的形式插入。
- cheap：该属性在打包后同样会为每一个文件模块生成 .map 文件
- module：该属性的配置也是生成一个没有列的信息的 sourceMaps 文件，同时 loader 的 sourcemap 也被简化成为只包含对应行的。
- 开发环境常用：cheap-module-eval-source-map。
- 生产环境常用：cheap-module-source-map。
- [详细学习地址。](https://www.cnblogs.com/jkr666666/p/11067189.html)

## a7、vconsole 插件：

移动端上网页调试颇为不便，使用 vconsole 模拟控制台功能进行调试。

- 安装：npm install vconsole
- main.js 中使用：

```js
import Vconsole from "vconsole";
// 开发环境中使用。
if (process.env.NODE_ENV === "development") {
  let vConsole = new Vconsole();
  Vue.use(vConsole);
}
```

## b、devServer：

**正向代理**：代理是处于客户端和服务器中间的一台计算机，正向代理是接受客户端的链接，然后向目标服务器请求资源，逐步返回给客户端。正向代理的服务器与目标服务器不在同一网段内，面向服务器。如 vpn。
**反向代理**：面向的是客户端，对外表现为一台服务器，目标服务器放在内网，而反向代理服务器作为网关，访问内网中的服务器需要经过代理服务器，<i class="green">所以目标服务器更安全且压力变小，代理服务器还负责分发内容，缓存前端资源，因此也能优化前端性能。</i>
vue 中使用代理来处理跨域，在 config 文件夹下的 Index.js 文件中配置，这个文件是配置运行、打包的一些具体属性的，exports 中对应的键值与 package.json 中的 scripts 里设置的运行命令对应，用 vue-cli 初始化的项目则默认是 dev 和 build。
**webpack-dev-server 参数**：--hot#热更新，修改代码后，只会替换原来块的代码，而不会整个刷新页面。--open#启动后打开浏览器。--config#指定使用的配置文件。
**注**：proxy 下面是按顺序来匹配的，一个项目配置了多个映射的话，如果上面的映射项匹配到接口路径满足，那么下面的映射配置就不在生效，然而代理信息 devServer 也不会打印出来，所以注意自己的接口路径是否会被前面的映射匹配到。

```js
// 一般在webpack.base.config.js文件。注意是使用0.0.0.0而不是Localhost，不然无法ipv4访问。
const HOST = process.env.HOST || '0.0.0.0';

const devWebpackConfig = merge(baseWebpackConfig, {
  devServer: {
      host:HOST,  // 设置可访问的地址。process.env.HOST表示本机ip可访问。
      port:3320, //访问网页的端口号。
      hot:true,//模块热替换功能,默认是又变动后刷新整个页面
      open:true,//服务启动后打开浏览器。
      onListening:function(server){},//提供监听触发请求时的一个自定义操作。
      historyApiFallback:true,//历史请求信息
      // 浏览器访问的是，本机ip:端口+路径。终端会显示代理访问记录
      proxy:{
          "/api": {
            bypass: function (req, res, proxyOptions) {},
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

- [devserver 配置部分](https://www.cnblogs.com/wb336035888/p/10448873.html)

## c、vue 多页面应用配置：

`/build/webpack.base.config.js`文件添加多个主 js 文件入口，形如：

```js
module.exports = {
  entry: {
    app: "./src/pages/home/min.js",
    one: "./src/pages/game/min.js",
  },
};
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
  plugins: [
    // 其它页面复制，相应的更换index，app即可。
    new HtmlWebpackPlugin({
      filename: config.build.index,
      template: "index.html",
      inject: true,
      minify: {
        removeComments: true,
        collapseWhitespace: true,
        removeAttributeQuotes: true,
      },
      chunksSortMode: "dependency",
      //(在这里和你上面chunks里面的名称对应),不然会同时导入两个页的js，然后报错。
      chunks: ["manifest", "vendor", "app"],
    }),
  ],
});
```

`/config/index.js`文件添加：

```js
module.exports = {
  build: {
    //build时导出的文件。
    index: path.resolve(__dirname, "../dist/index.html"),
    one: path.resolve(__dirname, "../dist/one.html"),
    two: path.resolve(__dirname, "../dist/two.html"),
  },
};
```

根据上面相应的位置创建 js、vue、html 文件。<b c=r>home.vue 和 home.html 文件种将 id 更改</b>。

```js
//one.js文件。
import Vue from "vue";
import one from "./one.vue";
import router from "./router";

Vue.config.productionTip = false;
/* eslint-disable no-new */
new Vue({
  el: "#one",
  router, //加上路由的话可以在路由页
  render: (h) => h(one),
});
```

**访问**：http://127.0.0.1:8080/home.html#/[vue多页面应用配置教程。](https://blog.csdn.net/weixin_44135121/article/details/94445734)

## e1、px 转 rem 配置：

使用插件 postcss-plugin-px2rem，安装：npm i postcss-plugin-px2rem -D。然后在 vue-loader 下配置。！移动端使用。

```js
var px2rem = require("postcss-plugin-px2rem");
modules: {
  rules: [
    {
      test: /\.vue$/,
      loader: "vue-loader",
      options: {
        // 配置，rootValue值为1rem转换为px的大小。
        postcss: function () {
          return [px2rem({ rootValue: 100 })];
        },
      },
    },
  ];
}
```

该插件只负责转换尺寸和单位，根元素字体大小在 html 文件用 js 去改变，两者配合使用。

## f、代码分割：

用于将更多的公共模块从大的模块中分离出来。<b c=v>不过尽量将功能中依赖的 js 都放在一个 bundle，这样只用一次 http 请求。</b>

- 添加入口的方法来分离代码块：entry 多加一个想要分离的 js 文件，如果这个文件也使用了一些其它公共的模块，同样会同这个 js 文件进入一个 bundle 中。
- 使用 CommonsChunkPlugin：插件部分添加该插件和规则，示例如下：<b c=r>webpack4.x 后被废弃。改用 splitChunkPlugin</b>

```js
{
  plugins: [
    new webpack.optimize.CommonsChunkPlugin({
      name: "tools",
      // minChunks可以是数值，Infinity时表示无限制。
      minChunks(module, count) {
        // module.resource为文件路径，count是引用的次数。
        // 将/utils下的tools.js文件分离出来。    ！！为true时表示进入该chunk。
        return (
          module.resource &&
          /\.js$/.test(module.resource) &&
          module.resource.indexOf("/utils/tools.js") !== -1
        );
      },
      chunks: [], //也可以直接指定哪几个chunk在这个bundle
      minSize: 3, //最小包含的模块数量
    }),
  ];
}
```

- 使用 CopyWebpackPlugin 将 js 文件直接从 html 引入，将 js 文件放到对应的静态资源文件夹中即可。[Index.html 文件引入 js 文件。](https://blog.csdn.net/qq_15253407/article/details/89491255)
- 使用 commonsChunkPlugin 或新版的 splitChunk 都只能分割主入口同步导入的和各页面的代码，而各页面 import 等导入的不能控制。[import()使用](https://www.cnblogs.com/dahe1989/p/11543832.html)

## g、bable 插件：

webpack 只能将一部分 es6 语法转换为 es5，而一些高级的 es6 语法，和部分 es7 语法无法转译，这就需要 bable。bable 包含：preset-env、plugin-component、polyfill 等多个子插件。
<b class="violet">项目中的.bablelr 是 bable 的配置文件，而需要使用的话需要在 webpack 的 modules 中引入 bable-loader。</b><b class="gray">babel 中引入的分为转换插件（转换代码，编译）和语法插件（解析特定类型的语法，如果你已经使用了相应的转换插件，则不需要指定语法插件。）</b>
使用前先安装：`cnpm i babel-core babel-loader babel-plugin-transform-runtime -D`
**bable 中常用的插件**：7.0 以下的版本插件几乎以 abel-plugin-开头，7.0 以上的以@babel/开头，两个版本混用会导致解析失败。
<i class="lable2">preset 部分</i>

- @babel/env 对应 6.0+的 babel-env：为目标浏览器中没有的功能加载转换插件。不太推荐 preset-env。
- @babel/polyfill：可以使用诸如 Promise 和 WeakMap 之类的新的内置组件、 Array.from 或 Object.assign 之类的静态方法，不过是全局的，所以会对全局变量造成污染，现在已经不建议使用。安装时使用`--save`
- transform-vue-jsx：可以支持 jsx 语法（ts）。
- [制作可在 babel 中配置的插件。](https://github.com/jamiebuilds/babel-handbook/blob/master/translations/zh-Hans/README.md)
- stage 系列插件：它们用于解析 es6,7 等版本 js 语法的方案，包含 0-4，功能逐渐降低，对最新语法处理的程度，一般使用 stage-2。
- transform-runtime：只用于开发环境，由于 webpack 的打包机制会将模块中导入的都打包到一起，然而一些较大的公共包也会有被打入多个 chunk 组的情况，transform-runtime 可以提取分离它们

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

**webpack 中配置如下**：[bable 官网](https://www.babeljs.cn/docs/babel-preset-env)。[.babelrc 文件作用及属性，部分组件按需引入，需要配置。](https://www.cnblogs.com/wulinzi/p/8079509.html)

- `{ test:/\.js$/, use: 'babel-loader', exclude:/node_modules/ }`#exclude 指定排除掉的文件夹。 如果不排除 node_modules， 则 Babel 会把 node_modules 中所有的 第三方 JS 文件，都打包编译，这样，会非常消耗 CPU，同时，打包速度非常慢；
  [编写 plugin 参考学习地址。](https://www.cnblogs.com/wzndkj/p/10921340.html)

## Q、问题集：

- 解析 less 文件时提示：TypeError: loaderContext.getResolve is not a function：换使用较低的 less-loader 版本。4.1.0
- 解析 less，sass 等文件时提示：Module build failed: Unrecognised input。按 a2 中方法配置 loader 即可，一般用默认模板的话，utils 中是已经配置好的，安装好 loader 即可用。
- 编译运行时一直卡住的问题：可能是相应的 loader 版本较高，尝试安装低版本。
- file-loader 提示 Rule can only have one resource source：尝试低版本的 webpack。
- mini-css-extract-plugin 提示：Class extends value undefined is not a constructor or null。需要 webpack 版本>=4.1.0
- mini-css-extract-plugin 提示： Cannot read property 'createHash' of undefined。依然是 webpack 版本问题，npm install webpack@^4.29.6 可以支持。
