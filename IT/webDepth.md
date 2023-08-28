# 一、webGIS

## a、坐标系

用于定义实际位置的坐标框架，地球是一个椭球体，需要将位置展现在一个平面上，必然会出现一些偏差。

**地理坐标系**：直接建立在椭球体上，用经度和纬度表达地理对象位置。与投影坐标系==共同完成整个坐标体系==

**投影坐标系**：建立在平面上。将地球上的经纬度表示投影到平面上。
（a）实际投影时先将一些经线和纬线的交点展绘在平面上，再将相同经度的线连成经线，相同纬度的连成纬线形成经纬网。
（b）依靠这个经纬网，再在平面上去描绘具体的位置。
（c）**等角投影**：投影过程角度没有变形，**便于测量方向和角度**，但**面积变形很大**，不能做测量面积使用。
（d）**等积投影**：等面积投影，**便于面积的比较和量算**，常用于对面积测量要求高的情况。
（e）任意投影：以上两种投影的综合。

## b、底图

webGIS的二维底图主要有矢量地图和瓦片地图两种形式，可以读取本地数据文件解析，也可以从服务端拉取图片（常用）

**瓦片地图**：通过将影像数据进行预处理，采用高效缓存机制（金字塔结构）形成。
（a）web端使用时通过地图的级数（放大程度）行列号向服务端分别获取对应图片
（b）按照请求空间，行列号结构组织瓦片图在视图中显示。
（c）瓦片图是预先裁剪的缓存图片集，因此**加载速度一般较快**。

**矢量图**：
（a）web端通过网络请求gis服务，请求到矢量数据，前端实时生成矢量地图。
（b）矢量图**更能满足**web端上的**数据处理，分析要求**（如改变底图颜色）

# 二、webRTC

## a、简介

webrtc并非只用于互联网，或者简单的浏览器与服务器之间，下面是它可以搭配的一些设备及其场景。

**webrtc三角形**：两个浏览器从同一个服务器下载同一份webrtc程序运行，==两个浏览器之间建立对等连接，直接传输数据==，但浏览器与服务器都有连接（webrtc中信令并未实现标准化。有时候将浏览器与服务器之间的连接称为信令）

**webrtc梯形**：两个浏览器分别连着两台不同的web服务器，两台服务器之间有标准信令连接，两个浏览器间直接传输音视频数据（一些复杂场景也可以改为通过一些介质设备来传递数据）

**SIP启动协议**：web服务器内有一个内置的**信令网关**，浏览器与**SIP客户端**之间通过此网关来建立连接**形成媒体流**（建立对等连接会与SIP用户代理建立标准的**实时传输协议**`RTP`）

**jingle**：web服务器具有一个内置的可扩展消息现场协议（`XMPP[RFC6120]`也称jabber）服务器，该内置服务器通过另一个XMPP服务器与jingle客服端通信。

**webrtc和公共交换电话网**(`PSTN`)：PSTN 网关是纯音频媒体流的终结点，负责将 PSTN 电话呼叫与媒体相连。在 Web 服务器与 PSTN 网关之间需要有某种形式的信令，具体可以是 SIP，也可以是主/从控制协议。

<img src="./_v_images/webrtc-sip.png" style="height:200px;"/> <img src="./_v_images/webrtc-jingle.png" style="height:200px;"/><img src="./_v_images/webrtc-PSTN.png" style="height:200px;"/>

**webrtc多方会话**：
（1）**全网状模式：**多个浏览器之间都建立一个对等连接。**优劣**：不需要服务器基础架构，延迟最低，质量也最高，但不适合大型多方会议（带宽过高）
（2）**集中模式：**多个浏览器只用和一个服务器建立连接，然后服务器将多方的数据通过混合或不处理发送给各浏览器。**优劣**：适合大型会话，但会话人数少时效率反而显得较低。

**建立会话过程**：获取本地媒体，建立对等连接，关联媒体或数据，交换会话描述。

## b、获取本地媒体

**轨道**：(`MediaStreamTrack `)是 WebRTC 中的基本媒体单元。此轨道**代表**一种**设备或录制内容**(称为“源”) 可返回的单一类型的媒体。
（a）单个立体声源或 6 声道环绕声音频信号均可视为-个轨道，尽管二者都由多个音频声道构成。
（b）在使用对等连接进行传输时，**轨道的各个声道将被视为一个单元**，即使其在本地处于启用 /禁用或静音状态

**流**：(`MediaStream`) 是 MediaStreamTrack 对象的集合。有两种方式可用于创建这些 MediaStream对象
（a）一是通过从现有 MediaStream 中**复制轨道来请求**对本地媒体的访问。
（b）二是使用对**等连接来接收**新的流。
（c）请求和访问本地媒体只有一种方式，即通过调用` getUserMedia()`

```html
<video id="video">调用摄像头</video>
<canvas id="canvas"></canvas>
<button onclick="get()">打开摄像头</button>
<button onclick="show()">拍照</button>
<button onclick="deviceClose()">关闭所有设备</button>
```

**js部分**：只有本地文件(`file://, localhost://`)，和`https`情况才能访问

```js
var width = window.innerWidth;
var height = window.innerHeight;
var video = document.getElementById("video");
var stream = null;

// 点击调用摄像头【可以只获取音频/视频】
function get() {
  // obj传到getUserMedia()方法中
  var obj = {
    // 设置视图大小，允许录制音频
    video: {
      width: width,
      height: height,
      bitrate: 1500 * 1000,
      keyInterval: 2,
      // 帧率设置
      frameRate: {
        min: 5,
        ideal: 10, // 期望最合适的帧率
        max: 15,
      },
      facingMode: "user", // 前后置摄像头设置，user:前，environment:后
    },
    audio: true,
  };
  /*=======兼容性处理==================*/
  let photo =
    navigator.mediaDevices.getUserMedia(obj) ||
    navigator.webkitGetUserMedia(obj) ||
    navigator.mozGetUserMedia(obj) ||
    navigator.msGetUserMedia(obj);
  // 会先获取权限(用户控制)，调用成功的话则运行then()方法
  photo.then(function (MediaStream) {
    // srcObject属性，兼容性处理。
    stream = MediaStream;
    
     var t = stream.getVideoTracks()[0];
    console.log("capabilit--", JSON.stringify(t.getCapabilities()));
    /*****设置约束*****/ 
    var constraints = {
      mandatory: { aspectRatio: 1.33333333 },
      optional: [{ width: { min: 640 } }, { height: { max: 400 } }],
    };

    t.applyConstraints(constraints,() => {
        console.info("success--", JSON.stringify(t.getSettings()));
      },() => {
        console.error("err--");
    });
      
    if ("srcObject" in video) {
      video.srcObject = stream; //图像显示到video元素中
    } else {
      video.src = window.URL.createObjectURL(stream);
    }
    // 导入完毕时显示。
    video.onloadedmetadata = function (e) {
      video.play();
    };
  });
  // 调用失败则运行catch()方法
  photo.catch(function () {
    alert("调用摄像头失败");
  });
}
// 点击拍照
function show() {
  var canvas = document.getElementById("canvas");
  var ctx = canvas.getContext("2d");
  // 上面获取到的but是RGB数组对象。
  ctx.drawImage(video, 0, 0, width, height);
}
// 关闭所有设备
function deviceClose() {
  const devices = stream.getTracks();
  /**数据格式。
        [{contentHint: ""
        enabled: true
        id: "0f4862bc-40cf-4e12-9134-a87f88f8a5b0"
        kind: "audio"
        label: "默认 - 麦克风 (Realtek(R) Audio)"
        muted: false
        onended: null
        onmute: null
        onunmute: null
        readyState: "ended"
        }]
    */
  devices.forEach((v) => v.stop());
}
```

## c、信令

**信令作用**：浏览器与服务端的连接
（1）协商媒体功能和设置。
（2）标识和验证会话参与者的身份
（3）控制媒体会话、指示进度、更改会话和终止会话
（4）当会话双方同时尝试建立或更改会话时，实施双占用分解 (Glare Resolution)
（5）**注：**两个浏览器与服务器的**信令协议可以不同**，但信令或控制服务器==无法向终端设备中推送信令代码==。因此，**实现互操作功能**的唯一方式是，让两个终端使用**同一标准化信令协议**例如 SIP 或 Jingle 。

**信令传输**：
（1）http传输。
（2）websocket传输。

**信令协议**：
（1）各协议都有信令状态机（空闲、正在连接、已连接）
（2）`SIP`：一种信令协议，通常用于IP 语音 ( Voice over IP，VoIP) 和视频会议系统。
（3）`Jingle`：是对可扩展消息传递和联机状态协议的扩展，又称为 Jabber，它向XMPP 中添加了媒体信令功能。利用Jingle,可将SDP会话描述映射至XML格式，再通过TCP或TLS 传输至XMPP 服务器。

**信令通道建立**：可以在获取“本地媒体流”之前，执行此步操作（这是一个webrtc三角形例子）
（1）开始：可将状态机（自定义的）设置为**空闲状态**。
（2）本地浏览器先向web服务器发送一个`密钥key`。
（3）本地浏览器等待web服务器告知“另一个端浏览器”是否有响应（是否已准备进行连接）【可使用http轮询，或websocket】
（4）未得到对方浏览器的应答（来自服务器），则都将状态机状态置为**“等待状态”**。
（5）收到另一方浏览器应答后（来自服务器），将状态机状态设置为**“已连接”**。
（6）然后向web服务器发送信令相关信息（web服务器要将其发送给对端浏览器）

对等连接：WebRTC 对等连接并不是TCP 意义上的那种连接。它是一组路径建立进程(ICE)以及一个可确定应建立哪些媒体和数据路径的协商器。RTCPeerConnection 对象的构造函数有一个配置对象，该配置对象包含一系列属性其中最重要的是 iceServers，此属性是一个服务器地址列表，用于帮助通过 NAT 和防火墙建立会话。

## m、其它方案参考

**webrtc相关库**：[腾讯的一套 webrtc 直播 sdk](https://github.com/tencentyun/tweblive)、[一个开源webrtc](https://github.com/mpromonet/webrtc-streamer)、[方案参考](https://juejin.cn/post/7210574986780426277?searchId=2023082311312768B28DB46AC2D3039196)、

**rtsp**：实时流[传输协议](https://link.juejin.cn/?target=https%3A%2F%2Fbaike.baidu.com%2Fitem%2F%E4%BC%A0%E8%BE%93%E5%8D%8F%E8%AE%AE%2F8048821%3FfromModule%3Dlemma_inlink)（RTSP）是**公有**协议，流媒体传输协议。

- 是`TCP/IP`协议体系中的一个应用层协议。
- 该协议定义了[一对多](https://link.juejin.cn/?target=https%3A%2F%2Fbaike.baidu.com%2Fitem%2F%E4%B8%80%E5%AF%B9%E5%A4%9A%2F1327103%3FfromModule%3Dlemma_inlink)[应用程序](https://link.juejin.cn/?target=https%3A%2F%2Fbaike.baidu.com%2Fitem%2F%E5%BA%94%E7%94%A8%E7%A8%8B%E5%BA%8F%2F5985445%3FfromModule%3Dlemma_inlink)如何有效地通过IP网络传送多媒体数据。
- 服务端可以自行选择使用TCP或UDP来传送串流内容。
- 它的语法和运作跟HTTP 1.1类似，但并**不特别强调时间同步**，所以比较能容忍网络延迟。
- url格式：类似`rtsp://host[:port]/[abs_path]/content_name`。
- **无法直接使用**现有的web技术进行播放rtsp直播数据流的（hls，rtmp其实是对该方案的替代实现）

**HLS**：常用与流媒体播放，也有利用其推流的技术
（1）的工作原理是把整个流**分成一个个小的基于 HTTP 的文件**来下载，每次只下载一些。
（2）当媒体流正在播放时，客户端可以选择从许多不同的备用源中以不同的速率下载同样的资源，
（3）允许流媒体会话适应不同的数据速率。
（4）客户端首先需要下载描述不同码流元数据的**M3U8索引文件**
（5）**m3u8**：该文件实质是一个播放列表（playlist）其可能是一个媒体播放列表（Media Playlist），或者是一个主列表（Master Playlist）。但无论是哪种播放列表，其内部文字使用的都是 utf-8 编码。

```js
/*===*-----  直播端逻辑  ----*===*/
var stream = await navigator.mediaDevices.getUserMedia({ audio, video });
var rtc = new RTCPeerConnection(null);
// 将每帧流添加到rtc中。
stream.getTracks().forEach(function (track) {
  //将一个新的媒体音轨添加到一组音轨中，这些音轨将被传输给另一个对等点。
  rtc.addTrack(track);
});
var offer = await rtc.createOffer(); // 返回一个本地会话描述。
await rtc.setLocalDescription(offer); // 设置本地描述,然后通过其信令通道将此会话描述发送
// 将信令sdp发送，并获取服务端用于与该客户端连接的sdp。
const sdp = await ajax({ url, data: { sdp: offer.sdp, streamurl: "" } });
// 将此获取到的sdp设为远程会话描述。
await offer.setRemoteDescription(
  new RTCSessionDescription({ type: "answer", sdp: sdp })
);
/*=========
    收看端
===========*/
// 使用hls.js进行拉流，内部原理暂未了解！。
if (video.canPlayType("application/vnd.apple.mpegurl")) {
  video.src = "http://fjjla.m3u8";
  video.play();
} else if (Hls.isSupported()) {
  // hls.js播放m3u8视频流
  that.flvPlayer = new Hls();
  that.flvPlayer.loadSource("http://fjjla.m3u8");
  that.flvPlayer.attachMedia(video);
  video.play();
}
```

**websocket方案**：`flv.js`是此方案实现的
（a）服务器端用 websocket 接受 [rtsp](https://link.juejin.cn/?target=https%3A%2F%2Fso.csdn.net%2Fso%2Fsearch%3Fq%3Drtsp%26spm%3D1001.2101.3001.7020) ，然后，推送至客户端。
（b）客户端将其解析转变转成mp4，放到vidoe标签中进行播放。

**flv.js**：用于在Web浏览器中播放FLV格式的视频文件。
（a）flv.js的原理是通过将FLV文件从HTTP请求中通过AJAX异步请求获取到，然后将FLV文件转换成JavaScript对象的形式，
（b）然后将音视频数据按照FLV协议解析出来，并通过HTML5的Video组件或Flash组件进行展示播放。
（c）是**使用WebSocket**在服务端和客户端之间进行数据传输

**rtmp**：是`Adobe`的**私有协议**，流媒体传输协议

- 推流协议使用 rtmp，之前的借助` flash` 插件实现 rtmp 推流，但 flash 插件各浏览器几乎已不支持。
- 这个协议建立在 TCP 协议或者轮询 HTTP 协议之上。所以理论上可以用 js 实现 rtmp 协议，似乎也有人这么做，但**没找到相关**的解析 rtmp 协议的 js 库。
- [流媒体服务框架](https://github.com/ZLMediaKit/ZLMediaKit)、[EasyMedia 浏览器 rtmp 播放](https://gitee.com/52jian/EasyMedia#https://download.csdn.net/download/Janix520/15785632)、[git 地址](https://github.com/chxj1992/rtmp-streamer)

**JSMpeg方案**：ffmpeg + http server(接流)+ websocket(server中继转发,client接收流) + [jsmpeg.js](https://link.juejin.cn/?target=https%3A%2F%2Fgithub.com%2Fphoboslab%2Fjsmpeg)
