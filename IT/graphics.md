# 一、图形学简介

也称计算机图形学，它是研究图形的输入、模型(图形对象)的构造和表示、图形数据库管理、图形[数据通信](https://baike.baidu.com/item/数据通信/897073?fromModule=lemma_inlink)、图形的操作、[图形数据](https://baike.baidu.com/item/图形数据/5199438?fromModule=lemma_inlink)的分析，以及如何以[图形信息](https://baike.baidu.com/item/图形信息/5199461?fromModule=lemma_inlink)为媒介实现人机交互作用的方法、技术和应用的一门学科。它包括图形系统硬件(图形输入-输出设备、[图形工作站](https://baike.baidu.com/item/图形工作站/7557182?fromModule=lemma_inlink))图形软件、算法和应用等几个方面。

# 二、术语

**抗锯齿**：是一种能够消除显示器输出的画面中图物边缘出现凹凸锯齿的技术，在开启抗锯齿后会使得图像边缘看起来更平滑，更接近实物的物体
**图像alpha通道**：是指一张[图片](https://baike.baidu.com/item/图片?fromModule=lemma_inlink)的[透明](https://baike.baidu.com/item/透明?fromModule=lemma_inlink)和[半透明度](https://baike.baidu.com/item/半透明度?fromModule=lemma_inlink)。
**色调**：各种图像色彩模式下原色 的明暗程度（**红、绿、蓝**三种原色的明暗程度）
**色相**：就是颜色，调整色相就是调整景物的颜色。
**饱和度**：指图像中颜色的浓度。饱和度越高，颜色越饱满，即所谓的青翠欲滴的感觉。饱和度越低，颜色就会显得越陈旧、惨淡。
**对比度**：指不同颜色之间的差别。对比度越大，不同颜色之间的反差越大。
**亮度**：各种图像色彩模式下原色的明暗程度。图像亮度增加时，就会显得耀眼或刺眼，亮度越小时，图像就会显得灰暗。

**渲染管线**：对象从原始定义空间通过一系列的中介空间直至最终映射至屏幕对的象数据转换操作（如高效的光照计算、视椎体擦除）

物理渲染：物理渲染器采用光谱的计算原理，是一个基于真实光线物理特性的全新渲染引擎，按照完全精确的算法和公式来重现光线的行为。

实时渲染：对图形数据的实时计算和输出。要求能在短时间内渲染出一张图片。

离线渲染：根据预定的数据 设置对场景进行渲染生成，一般用于影业特效，超真实的渲染。

**空间**：有纹理空间、三维空间、屏幕空间等术语。三维空间到屏幕空间显示是一个**透视投影的操作**。物体空间（曲面体常用参数`(Θ,φ)`表示，也称**参数空间**）

视点：指用户观察三维场景时所处的点，一般用摄像机的理念来代替，视线：指视点观察的方向，用一条线描述。上方向：与视点，视线一起
**坐标系**：
（1）世界坐标系：定义三维场景的方向参考，z轴正方向垂直指向屏幕。
（2）物体坐标系：定义物体本身的方向参考，物体变换后坐标方向也跟着旋转。
（3）观察坐标系：观察者即视点的坐标系，z轴正方向是从==外部指向屏幕内部==的。
（4）屏幕坐标系：用于表示三维对象透视，投影到屏幕的最终显示结果。z轴坐标一般都默认为0，==正方向指向屏幕内==。
（5）纹理坐标系：`(u,v)，0~1`表示的标准纹理坐标，对应到真实纹理坐标。

**VR**：虚拟现实技术(英文名称：Virtual Reality，缩写为[VR](https://baike.baidu.com/item/VR/764830?fromModule=lemma_inlink))，又称[虚拟实境](https://baike.baidu.com/item/虚拟实境/10403543?fromModule=lemma_inlink)或灵境技术，是20世纪发展起来的一项全新的[实用技术](https://baike.baidu.com/item/实用技术/9916621?fromModule=lemma_inlink)。虚拟现实技术囊括计算机、[电子信息](https://baike.baidu.com/item/电子信息/5578438?fromModule=lemma_inlink)、[仿真技术](https://baike.baidu.com/item/仿真技术/7181700?fromModule=lemma_inlink)，其基本实现方式是以[计算机技术](https://baike.baidu.com/item/计算机技术/1127562?fromModule=lemma_inlink)为主，利用并综合[三维图形](https://baike.baidu.com/item/三维图形/5612976?fromModule=lemma_inlink)技术、[多媒体技术](https://baike.baidu.com/item/多媒体技术/143527?fromModule=lemma_inlink)、仿真技术、[显示技术](https://baike.baidu.com/item/显示技术/5851114?fromModule=lemma_inlink)、伺服技术等多种高科技的最新发展成果，借助计算机等设备产生一个逼真的三维视觉、触觉、嗅觉等多种感官体验

**AR**：增强现实([Augmented Reality](https://baike.baidu.com/item/Augmented Reality/5372911?fromModule=lemma_inlink)，[AR](https://baike.baidu.com/item/AR/3404706?fromModule=lemma_inlink))技术是一种将虚拟信息与[真实世界](https://baike.baidu.com/item/真实世界/631440?fromModule=lemma_inlink)巧妙融合的技术，广泛运用了多媒体、[三维建模](https://baike.baidu.com/item/三维建模/4672401?fromModule=lemma_inlink)、实时跟踪及注册、智能交互、传感等多种技术手段，将计算机生成的文字、图像、[三维模型](https://baike.baidu.com/item/三维模型/6846264?fromModule=lemma_inlink)、音乐、视频等虚拟信息模拟仿真后，应用到真实世界中，两种信息互为补充，从而实现对真实世界的“增强”

# 三、颜色

**光谱**（spectrum）
（1）是[复色光](https://baike.baidu.com/item/复色光/1169071?fromModule=lemma_inlink)经过色散系统（如棱镜、光栅）[分光](https://baike.baidu.com/item/分光/8370907?fromModule=lemma_inlink)后，被[色散](https://baike.baidu.com/item/色散/862554?fromModule=lemma_inlink)开的[单色光](https://baike.baidu.com/item/单色光/1168886?fromModule=lemma_inlink)按波长（或频率）大小而依次排列的图案，全称为光学频谱。
（2）光谱中最大的一部分**可见光谱**是[电磁波谱](https://baike.baidu.com/item/电磁波谱/907208?fromModule=lemma_inlink)中人眼可见的一部分，在这个[波长范围](https://baike.baidu.com/item/波长范围/5463020?fromModule=lemma_inlink)内的[电磁辐射](https://baike.baidu.com/item/电磁辐射/484252?fromModule=lemma_inlink)被称作可见光。
（3）光谱并没有包含人类大脑视觉所能区别的所有颜色，譬如褐色和粉红色。
（4）**红外光谱**：在一些[可见光谱](https://baike.baidu.com/item/可见光谱/10914339?fromModule=lemma_inlink)的`红端之外`，存在着波长更长的[红外线](https://baike.baidu.com/item/红外线/115851?fromModule=lemma_inlink)；
（5）**紫外光谱**：同样，在紫端之外，则存在有波长更短的[紫外线](https://baike.baidu.com/item/紫外线/95551?fromModule=lemma_inlink)。红外线和紫外线都不能为肉眼所觉察，但可通过仪器加以记录
（6）SPD（光谱功率分布）如下图，不同的波长有对应不同的颜色，因此需要一个`SPD函数`来**表达它们之间的关系**。

<img src="E:/VNote/IT/_v_images/light-rgb.webp" style="height:300px;"/>

**颜色表示**：有rgb，cmyk，hsl表示法

- rgb：10进制的表示方法，将rgb转hsl只需每位转为16进制再拼接在一起即可。

- hsl：16进制的表示方法，hsl转rgb只需每两位分开，各转为10进制，对应的就是rgb色值。

  ```js
  /****rgb转为hsl格式***/
  function rgb2hls(that) {
        //var that = this;
        //十六进制颜色值的正则表达式
        var reg = /^#([0-9a-fA-f]{3}|[0-9a-fA-f]{6})$/;
        // 如果是rgb颜色表示
        if (/^(rgb|RGB)/.test(that)) {
          var aColor = that.replace(/(?:\(|\)|rgb|RGB)*/g, "").split(",");
          var strHex = "#";
          
          for (var i = 0; i < aColor.length; i++) {
            var hex = Number(aColor[i]).toString(16);
            if (hex.length < 2) {
              hex = '0' + hex;
            }
            strHex += hex;
          }
          if (strHex.length !== 7) {
            strHex = that;
          }
          return strHex;
        } else if (reg.test(that)) {
          var aNum = that.replace(/#/, "").split("");
          if (aNum.length === 6) {
            return that;
          } else if (aNum.length === 3) {
            var numHex = "#";
            for (var i = 0; i < aNum.length; i += 1) {
              numHex += (aNum[i] + aNum[i]);
            }
            return numHex;
          }
        }
        return that;
  };
  /***hsl转为rgba格式***/
  function hsl2rgb(rcolor, opacity) {
        const _opc = typeof opacity === "number" ? opacity : 1;
        var sColor = rcolor.toLowerCase();
        // 十六进制颜色值的正则表达式
        var reg = /^#([0-9a-fA-f]{3}|[0-9a-fA-f]{6})$/;
        // 如果是16进制颜色
        if (sColor && reg.test(sColor)) {
          if (sColor.length === 4) {
            var sColorNew = "#";
            for (var i = 1; i < 4; i += 1) {
              sColorNew += sColor.slice(i, i + 1).concat(sColor.slice(i, i + 1));
            }
            sColor = sColorNew;
          }
          // 处理六位的颜色值
          var sColorChange = [];
          for (var i = 1; i < 7; i += 2) {
            sColorChange.push(parseInt("0x" + sColor.slice(i, i + 2)));
          }
          return "rgba(" + sColorChange.join(",") + "," + _opc + ")";
        }
        return sColor;
  };
  const qp = rgb2hls('rgb(255,255,255)');
  const pc = hsl2rgb('#ffffff');
  ```

  **rgb表示原理**：r表示红色，g为绿色，b为蓝色。取值范围都为0~255。所有的颜色都有这3种颜色值组合而来，如下：
  （1）`rgb(255,0,0)，rgb(0,255,0)，rgb(0,0,255)`为红色、绿色、蓝色。
  （2）`rgb(255,250,0)`安照下图所示为深黄色，==b值逐渐增加时逐渐变为明亮==（淡黄向白色逼近）其它两种情况也是如此。
  （3）按照这种规律，看到色值时可以大致判断出它的颜色。
  （4）与SPD的映射计算：
  $$
  \left[\begin{matrix} r\\g\\ b\end{matrix}\right]=\left[\begin{matrix}\int R(λ)X(λ)d_λ &\int R(λ)Y(λ)d_λ&\int R(λ)Z(λ)d_λ \\ \int G(λ)X(λ)d_λ&\int G(λ)Y(λ)d_λ &\int G(λ)Z(λ)d_λ \\ \int B(λ)X(λ)d_λ &\int B(λ)Y(λ)d_λ &\int B(λ)Z(λ)d_λ   \end{matrix}\right]\left[\begin{matrix} x_λ\\ y_λ\\ z_λ\end{matrix}\right]
  $$
  <img src="E:/VNote/IT/_v_images/rgb.webp" style="height:260px;"/>

  **xyz颜色**： 就是在[RGB](https://baike.baidu.com/item/RGB/342517?fromModule=lemma_inlink)系统的基础上，用数学方法，选用三个理想的原色来代替实际的三原色，与rgb对应，值范围都在`0~1`

# 四、线相关

这里记录的是底层绘制直线的实现相关方法。主要解决的是**线段穿过两像素点之间时**，怎么取y值用**上/下**侧的像素点。

**DDA算法**：使用微分思想计算下一个y值：$\begin{cases}x_{i+1}=x_i+\Delta x\\ y_{i+1}=y_i+k*\Delta x\end{cases}$绘制时$\Delta x$都是取1（即每次增加1个像素单位）DDA算法根据k值来取使用哪一个y位置的像素点，如下：$y_{i+1}=\begin{cases}y_i+1 &,k>=0.5\\ y_i &,k<0.5\end{cases}$（yi表示上一个点的y值）
【缺点】：涉及浮点运算，对y取整要花费时间，不利于硬件实现。

**Bresenham算法**：起始点`(xi,yi)`主方向增加1个单位（这里用`y'`表示直线数学公式计算的理想y值，`di=-0.5`）
（1）主方向增量加1后，计算$d_{i+1}=y^{'}_{i+1}-y_i$。然后：$y_{i+1}=\begin{cases}y_i+1 &,d_{i+1}>=0\\ y_i &,d_{i+1}<0\end{cases}$
（2）再下一个增量，若$y_{i+1}-y_{i}<0$,则计算$d_{i+2}=y^{'}_{i+2}-y_{i+1}+d_i-0.5$
（3）若$y_{i+1}-y_{i}>=0$则将刚计算的$d_{i+2}-1$。
（4）d的计算每次都会`-0.5`这里为了消除浮点数的影响（不同DDA算法中那样用了浮点数0.5）
【缺点】计算中$y_{i+1}-y_{i}$依然会出现浮点数，比纯整数计算慢。

**整数Bresenham算法**：对上面的改进（消除小数部分）初始的$d_i=-\Delta x=-1$,差值计算$d_{i+1}=d_{i}+2(y'_{i+1}-y_i)
$。
主方向xi+1后，$y_{i+1}=\begin{cases}y_i+1 &,d_{i+1}>=0\\ y_i &,d_{i+1}<0\end{cases}$。

**渐变色直线**：使用颜色线性插值公式
（1）公式$p=(1-t)p_0+tp_1$，将p0为直线1起点p1为终点，将x，y分别代入。
（2）`t`就是中间点离两断点距离的一个比例。延y方向插值时$t=\frac{y-y_0}{y_1-y_0}$（==p点逐渐移动y值改变==，【<i id="cha_mark1">跳转标记</i>】）
（3）再根据这个公式$c=c_0(1-t)+tc_1$代入颜色，即可得到各点处的颜色值（rgb）

**反走样**：当绘制非垂直、水平、45度直线时由于上面类似算法的像素点选择会**分部在理想直线两侧**，当分辨率不够高时就易看出来。
这是数字化图像无法避免的问题，只能改善。硬件的改善就是靠增加分辨率（由于制作成本等很少会）

**反走样算法思想**：线两侧的像素点都参与显示直线，如背景白色，线黑色，若理想点直接计算在像素点上那直接显示黑色就行，若计算得在**两像素点中间**，那上下两个像素点颜色根据靠近理想点的距离决定（**靠得近越黑，离得远越灰色**，它们==总值和要为1==，实现中可用透明度控制）
可就用`Bresenham算法`中的计算d决定（但不再减去0.5）

**曲线**：二维，3维图形中用到的曲线，曲面多都是用2阶/3阶贝塞尔曲线完成，

**二阶贝塞尔**：用3个点p0，p1，p2控制
（1）p0，p1之间插值：$p_{01}=(1-t)p_0+tp_1$。系数`0<t<1`求两个点的中间某一点。
（2）p1，p2之间进行插值：$p_{12}=(1-t)p_1+tp_2$。
（3）合并1,2中俩式得：$p=(1-t)^2p_0+(-2t^2+2t)p_1+t^2p_2$，t可从`0~1`逐渐取值（如`0.05,0.1,0.15,...`），x，y坐标都使用此计算。

**三阶贝塞尔**：用4个点p0，p1，p2，p3控制，p1，p2是中间控制弯曲的点。
（1）p0，p1间插值：$p_{01}=tp_1+(1-t)p_0$。
（2）p1，p2间插值：$p_{12}=tp_2+(1-t)p_1$。
（3）p2，p3间插值：$p_{23}=tp_3+(1-t)p_2$。
（4）p01，p12间插值：$p_{01-12}=tp_{12}+(1-t)p_{01}$。
（5）p12，p23间插值：$p_{12-23}=tp_{23}+(1-t)p_{12}$。
（6）合并以上得：$p=(1-t)^3p_0+(3t^3-6t^2+3t)p_1+(-3t^3+3t^2)p_2+t^3p_3$。t同上使用。

# 五、面相关

**表面模型**：使用三角形可以逼近任意的面。
（1）点元表示法：使用三角形的3个顶点来表示，但进行填充时需要计算哪些点在其内。
（2）片元表示法：使用三角形内所有像素点来表示这个三角形，可直接进行填充。

**三角形着色模式**：
（1）平面着色模式：即使三角形各点颜色不一样，也只取其中一个颜色填充整个三角形。边界处会出现明显的对比度。
（2）光滑着色模式：从一个顶点向另外两个点的方向使用**双线性插值**（两个方向都计算插值）
（3）边界处理：填充三角形时对于边界，应只绘制其下侧边界，其它边界由其它三角形绘制时填充。

**生成球体**：
（1）设置1个角度`angle`（可被180整除，angle越小越精度越高），按该角度从下向上做切面。
（2）每个切面依然按`angle`划分，可得到`360/angle`个点。
（3）将球心坐标设置为`(0,0,0)`方便计算，且可省去各点法向量的计算（`球面点 - 球心`）
（4）按以下两个角度直接计算出各点的坐标（用α和R计算bp，再利用角θ计算p点的`x,z`坐标）
<img src="E:/VNote/IT/_v_images/yield-sphare.png"/>

（5）为了保证一致的索引读取，得保证每个切面的点数相同，因此 最上/下端切面即使只有1个点，也复制多个保存。

```js
// 顶点生成
function SphareArray(r, precision) {
  const a = 0, b = 0, c = 0;
  const angle = precision; // 每份所占角度
  const hudu = (s) => (s / 180) * Math.PI;
  const directorFen = 180 / angle + 1;
  const horizonFen = 2 * directorFen - 1;
  const sin = Math.sin, cos = Math.cos;
  const points = []; // 球面顶点
  const normalization = []; // 各点法向量
  // 底部顶点（全同）
  for (let i = 0; i < horizonFen; i++) {
    points.push(a, b - r, c);
    //normalization.push(0, 1, 0);
  }
  // 第1个 和最后1个 单独添加
  for (let i = 1, by, br; i < directorFen - 1; i++) {
    by = (b - r * cos(hudu(i * angle))).toFixed(4); // y坐标
    br = Math.abs(r * sin(hudu(i * angle)));
    for (let j = 0, bx, bz; j < horizonFen; j++) {
      bx = (a + br * sin(hudu(j * angle))).toFixed(4);
      bz = (c + br * cos(hudu(j * angle))).toFixed(4);
      points.push(Number(bx), Number(by), Number(bz));
      //normalization.push(Number(bx) - a, Number(by) - b, Number(bz) - c);
    }
  }
  // 顶部顶点（全同）
  for (let i = 0; i < horizonFen; i++) {
    points.push(a, b + r, c);
    //normalization.push(0, -1, 0);
  }
  return {
    points, directorFen, horizonFen
  };
}
/**
* 将数据按 三角形绘制 的索引读出（点的生成需要是 从低到高生成的）
* @param {number} rows 行数
* @param {number} columns 列数
* @param {boolean} [circle=true] 是否为环形
*/
yieldTriangleIndexs(rows, columns, circle = true) {
  /***
   * 5, 6, 7, 8, 9, 5
   * 0, 1, 2, 3, 4, 0
   * -----0,1,5为第1个三角形。1,5,6位第2个
   * 第1个三角形 i,i+1,i+columns
   * 第2个三角形 i+1, i+1+columns, i+columns
   * ***/
  const indexs = [];
  // j为行号，m为当前行偏移值， i为实际数组中的索引号
  for (let j = 0, i; j < rows - 1; j++) {
    let s = j * columns;
    for (let m = 0; m < columns - 1; m++) {
      i = s + m;
      indexs.push(i, i + 1, i + columns, i + 1, i + 1 + columns, i + columns);
    }

    if (circle) {
      ++i;
      indexs.push(i,i - columns + 1,i + columns,i - columns + 1,i + 1,i + columns);
    }
  }

  return indexs;
}
const data = SphareArray(5,20);
```

**二次贝塞尔曲面**：二次贝塞尔曲线的延伸，一个曲面需要9个顶点来进行控制。参数上也需要两个参数（`u,v`）控制，替代之前的t。
<img src="E:/VNote/IT/_v_images/bsr-plain.jpg" style="width:500px;"/>
$$
p(u,v)=\sum^2_{i=0}\sum^2_{j=0}p_{ij}B_i(u)*B_j(v),~~\begin{cases}B_0(u)=(1-u)^2 \\ B_1(u)=-2u^2+2u ,~~ B_2(u)=u^2 \\ B_0(v)=(1-v)^2\\ B_1(v)=-2v^2+2v ,~~ B_2(v)=v^2 \end{cases},~~ u,v\in[0,1]
$$
利用此公式在曲面中绘制多个点。实现如下：可用上面球体中读取索引生成三角形的方式来读取下方曲面的三角形。

```js
function Bezier2Plain() {
  /*
    p20     p21      p22
    p10     p11      p12
    p00     p01      p02
    */
  const pmap = {
      p20: [-1.0, 0, -1.0],p21: [0, 0, -1.0],p22: [1.0, 0, -1.0],
      p10: [-1.0, 0.4, 0],p11: [0, 0.8, 0],p12: [1.0, 0, 0],
      p00: [-1.0, 0, 1.0],p01: [0, 0.2, 1.0],p02: [1.0, 0, 1.0],
  };
  // 插值序数
  const B = [
    (t) => Math.pow(1 - t, 2),
    (t) => -2 * Math.pow(t, 2) + 2 * t,
    (t) => Math.pow(t, 2)
  ];

  function _calc(tu, tv) {
    let s = [0, 0, 0];
    for (let i = 0; i < 3; i++) {
      for (let j = 0; j < 3; j++) {
        s[0] += pmap[`p${i}${j}`][0] * B[i](tu) * B[j](tv);
        s[1] += pmap[`p${i}${j}`][1] * B[i](tu) * B[j](tv);
        s[2] += pmap[`p${i}${j}`][2] * B[i](tu) * B[j](tv);
      }
    }
    return s.map(v => Number(v.toFixed(4)));
  }
    
  let points = [], point;
  // 插值参数从0开始
  for (let u = 0; u <= 1; u += precise) {
    for (let v = 0; v <= 1; v += precise) {
      point = _calc(u, v);
      points.push(...point);
    }
  }
  // TODO: 计算周围三角的法向量平均值 作为各点法向量
  return points;
}
```

**三次贝塞尔曲面**：与二次类似，需要16个点来控制。
$$
p(u,v)=\sum^3_{i=0}\sum^3_{j=0}p_{ij}*B_i(u)*B_j(v),~~\begin{cases}B_0(u)=(1-u)^3,~~B_1(u)=-3u^3-6u^2+3u\\ B_2(u)=-3u^3+3u^2,~~B_3(u)=u^3\\ B_0(v)=(1-v)^3,~~B_1(v)=-3v^3-6v^2+3v\\ B_2(v)=-3v^3+3v^2,~~B_3(v)=v^3\end{cases}
$$
同二次曲面一样，生成出一些插值点，然后读取生成三角形绘制出来。**可优化**：足够平坦时可停止插值，使用简单的点就可绘制平坦的部分

# 六、变换

**二维变换**：有移动、旋转、缩放、反射、错切5种变换。
利用矩阵乘积后得到变换后的x，y值反推各矩阵值，如下：
$$
\left[\begin{matrix}a&c&e\\b&d&f\\0&0&1\end{matrix}\right]*\left[\begin{matrix}
x \\ y \\ 1\end{matrix}\right]=\left[\begin{matrix}
  ax+cy+e \\ bx+dy+f \\ 0+0+1\end{matrix}\right]
$$
==移动情况==：水平移动的话，只需修改`e，f`即可，a=d=1，c=b=0，其它为0

==缩放情况==：修改第`a，d`值即是缩放，其余值为0（这里的缩放中心是坐标原点，改变缩放中心可以通过`e,f`来调节）

**旋转变换**：通过正余弦表达计算旋转后的点，得$a=cos(β),c=-sin(β),b=sin(β),d=cos(β),e=f=0$（这里的旋转中心为原点，β为逆时针旋转角度）

**反射变换**：较为简单，用坐标轴做反射情况改变x，y正负即可。
（1）原点反射：$a=d=-1$其余为0。
（2）x轴反射：a=1，d=-1。其余为0。
（3）y轴反射：a=-1，d=1。其余为0。

错切变换：点p迎x，y轴发生不等量变换到p1的过程。a=d=1，e=f=0，控制c，b达到错切效果

**三维变换**：与二维类似。与css3中的变换矩阵同理（利用相乘得到变换后的坐标和计算过程**反推哪些值的作用即可**！）
$$
\left[\begin{matrix}x^`\\y^`\\z^`\\1\end{matrix}\right] = \left[\begin{matrix}a&b&c&d\\e&f&g&h\\i&j&k&l\\m&n&o&p\end{matrix}\right]*\left[\begin{matrix}
x \\ y \\z\\ 1\end{matrix}\right] 
&相当于\begin{cases}x^`=ax+by+cz+d\\ y^`=ex+fy+gz+h\\ z^`=ix+jy+kz+l\\ 1=mx+ny+oz+p\end{cases}
$$
平移效果：`d,h,l`为x，y，z轴上的平移量，主对角线为1，其它为0即可。
缩放效果：`a,f,k为x,y,z`轴的缩放程度，p=1，其余为0即可。

旋转效果：`a,b,e,f`为相关三角函数值，其余主对角线值为1，剩余值为0；绕各轴时具体情况如下：
$$
T_x=\left[\begin{matrix} 1&0&0&0\\ 0&\cos\beta &-\sin\beta &0\\0&\sin\beta&\cos\beta&0\\0&0&0&1 \end{matrix}\right],~~
T_y=\left[\begin{matrix} \cos\beta&0&\sin\beta&0\\ 0&1 &0 &0\\-\sin\beta&0&\cos\beta&0\\0&0&0&1 \end{matrix}\right],~~
T_z=\left[\begin{matrix} \cos\beta&-\sin\beta&0&0\\ \sin\beta&\cos\beta&0 &0\\0&0&1&0\\0&0&0&1 \end{matrix}\right]
$$

**层次模型**：对于一个复杂的联合模型（物理意义上一体）进行变换时控制比较复杂，如上手臂转动，下手臂也要转动，下手臂转动而上手臂无需转动
（a）对于这种模型可以按照它们的层次结构，控制关系来进行先后顺序的控制。
（b）==矩阵栈==：可以把有单独变换要求的模型的“变换”矩阵都放入一个栈中进行管理。
（c）如：绘制上手臂A时，将A的变换矩阵压入栈中（`ma`），对下手臂B进行绘制时其变换矩阵`mb`压入如栈中，对B进行的变换就是`mb * ma`。

# 七、投影

**正交投影**：坐标以垂直方向投影到对应的面，投影后与面垂直方向的轴坐标变得与平面此轴坐标一致，其它两个轴左边不变。

**斜投影**：向着所在的3维场景内投影，但投影方向不垂直与。例：点p1斜投影到xoy面的p2点，p3为其正交投影点，投影后的p2坐标计算：
$$
\left[\begin{matrix} x'\\y'\\z'\\1\end{matrix}\right]=\left[\begin{matrix} 1&0&-\cot\alpha\cos\beta &0 
\\0&1&-\cot\alpha\sin\beta &0\\0&0&0&0\\0&0&0&1 \end{matrix}\right]\left[\begin{matrix} x\\y\\z\\1\end{matrix}\right]~~,\alpha为
线(p1,p2)与xoy面夹角,\beta 为线(p2,p3)与x轴夹角
$$
<img src="E:/VNote/IT/_v_images/xie-shadow.jpg" style="width:500px;"/> <img src="E:/VNote/IT/_v_images/tou-shi.webp" style="width:500px;"/>

**透视投影**：仅是使用三维变换操作物体得到的视图并不真实，通过透视投影后得到的图形**更接近人眼观察**到的有3维感。
在人与物体之间，设立一个**透明的平面**，称作画面(即投影面)，人眼的位置称**视点**(即投影中心)，由视点至物体上各个点连线。
（1）观察物体的各点到视点的连线称为**视线**。观察中只存==在一个视平面==（不一定用**屏幕**）**主视线**：中心视线向量，与视平面垂直
（2）==垂直于==`视平面`的视线与视平面的交点为**视心**。视点到视心的**距离**称为**视距**`d`。视点到观察点的**距离**称为**视径**`R`
（3）**确定观察坐标系**：需要用视点和观察点确定 观察坐标系的`z轴向量`，用人眼**上方向**确定观察坐标系的`y轴向量`。用这两个向量来计算观察坐标系的`x轴向量`。
（4）世界坐标系转观察坐标系：物体的世界坐标系方向，距离都是相对于原点的，需要将它们都改为观察坐标系中的方向及位置。（如图需要将p点处x0方向坐标映射到xv方向，z0方向变换到zv方向，y轴坐标也类似）
<img src="E:/VNote/IT/_v_images/toushi-touy.png"/>

（4）观察坐标系到屏幕坐标系的变换：这一步通过投影完成，计算同斜投影方法类似。如p点映射到p1点。
（5）两步变换分别用两个矩阵表示，具体js代码如下：

```js
/**** 构造透视矩阵 ****/
function createViewMatrix(eyeX, eyeY, eyeZ, atX, atY, atZ, upX, upY, upZ) {
  // 向量归一化
  const normalize = (v) => {
    const length = Math.sqrt(v[0] * v[0] + v[1] * v[1] + v[2] * v[2]);
    return [v[0] / length, v[1] / length, v[2] / length];
  };
  // 相减生成向量
  const subtract = (v1, v2) => {
    return [v1[0] - v2[0], v1[1] - v2[1], v1[2] - v2[2]];
  };
  // 向量的叉乘得到它们的法向量
  const cross = (v1, v2) => {
    return [
      v1[1] * v2[2] - v1[2] * v2[1],
      v1[2] * v2[0] - v1[0] * v2[2],
      v1[0] * v2[1] - v1[1] * v2[0],
    ];
  };
  // 计算视向量，并归一化
  const zAxis = normalize(subtract([eyeX, eyeY, eyeZ], [atX, atY, atZ]));
  // 得到 视向量 与 上方向 的法向量 并归一化 （即：视觉坐标系的x轴方向）
  const xAxis = normalize(cross([upX, upY, upZ], zAxis));
  // 得到 视向量 与 x轴 的法向量 并归一化 （即：视觉坐标系的y轴方向）
  const yAxis = normalize(cross(zAxis, xAxis));

  return new Float32Array([
    xAxis[0],yAxis[0],zAxis[0],0,
    xAxis[1],yAxis[1],zAxis[1],0,
    xAxis[2],yAxis[2],zAxis[2],
    0,
    -(xAxis[0] * eyeX + xAxis[1] * eyeY + xAxis[2] * eyeZ),
    -(yAxis[0] * eyeX + yAxis[1] * eyeY + yAxis[2] * eyeZ),
    -(zAxis[0] * eyeX + zAxis[1] * eyeY + zAxis[2] * eyeZ),
    1,
  ]);
}

function angleToRadian(angle) {
  return (Math.PI * angle) / 180;
}

/***** 构建投影矩阵 ****
fov： 表示观察者的可视范围的角度。
aspect： 投影面的宽高比 ，一般就用 canvas.width / canvas.height
newar: 近距离，1。 far：观测最远距离 100
*/
function createPerspective(fov, aspect, near, far) {
  fov = angleToRadian(fov); // 角度转弧度
  const f = 1.0 / Math.tan(fov / 2);
  const nf = 1 / (near - far);
  // prettier-ignore
  return new Float32Array([
        f / aspect, 0, 0, 0,
        0, f, 0, 0,
        0, 0, (far + near) * nf, -1,
        0, 0, 2 * far * near * nf, 0,
      ]);
}
// 透视矩阵
const viewMatrix = createViewMatrix(
        3, 4, 8, // 观察点
        0, 0, 0, // 视点
        0, 1, 0 // 上方向
      );
// 投影矩阵
const projMatrix = createPerspective(30, canvas.width / canvas.height, 1, 100);

/****再用 透视矩阵 x 投影矩阵 x 物体坐标***/
```

**zBuffer算法**：透视投影时如果有多个物体互相遮挡，用于分清哪个点投影到视图上。
（1）设置帧缓冲器颜色为背景色，
（2）设置帧缓冲器的宽、高、初始深度（一般初始深度设为最大值）
（3）对多边形表面的每个像素`(x,y)`，计算其深度值`z(x,y)`。
	使用平面公式，代入该点的（x，y）就能求z。平面上任意两条交叉直线可计算出法向量（3个点）
$$
\begin{cases}A=(y_1-y_0)(z_2-z_0)-(z_1-z_0)(y_2-y_0)\\ B=(z_1-z_0)(x_2-x_0)-(x_1-x_0)(z_2-z_0)\\ 
C=(x_1-x_0)(y_2-y_0)-(y_1-y_0)(x_2-x_0)\end{cases}~~,平面某点深度z(x,y)=-\frac{Ax+By+D}{C}
$$
​	C为0时说明该面法向量与Z轴重合，投影的点不变，不用此式计算。

（4）将z与存储在深度缓冲器中（x,y）处的深度值`zBuffer(x,y)`进行比较。
（5）若`z(x,y)<=zBuffer(x,y)`说明其越接近视点，将此像素颜色写入帧缓冲器。
（6）**注**：zbuffer算法中，==z轴正半轴是指向屏幕内，视点在z负半轴==，因此进行自己拿来使用时得注意这与绘制时的坐标系不同。

**背面剔除算法**：利用平面的法向量与视向量计算它们的夹角，大于90度则视为背面不再渲染。
（1）==平面法向量==：$N=p_4p_5\times p_4p_6$（两向量叉乘）
（2）视向量：$V=(x_v-x_4,y_v-y_4,z_v-z_4)$（看向各点的视向量要单独计算）
（3）归一化：将N归一化为`n`，V归一化为`v`。
（4）计算夹角：$n\cdot v=cos\theta$，$0\leq\theta\leq 90时\cos\theta>0$，表面可见。$90\leq\theta\leq 180,\cos\theta <0$，表面不可见。

# 八、模型导入

常用模型文件为`.obj`文件，文件中放置了模型的顶点、法向量、纹理坐标等数据，`.obj`文件格式如下：
（1）`#`开头为注释行，可以忽略。
（2）`o`表示一个图形对象名称，可以忽略。
（3）`s`后接`off`表示平面不应该做平滑处理（法向量不再计算均值）。
（4）`v`表示一个顶点坐标。
（5）`vt`表示对应序号的顶点的纹理坐标。
（6）`vn`表示对应顶点的法向量。
（7）`f`表示一个三角形的3个顶点对应的**索引**（==索引从1开始==而不是0）：`顶点/纹理坐标/法向量`
（8）obj文件中可以没有法向量，纹理坐标，此时`f`项中对应的就是空着的

```objc
# Blender v2.70
o Pyramid
v 1.00000 -1.00000 -1.00000
vt 0.51234 0.234434
vn 0.32434 -1.23434 0.3454354
s off
f 2/1/1 3/2/1 4/3/1
```

# 九、光照

**简述**：完善的光照处理非常复杂，这些因素都影响渲染效果：光源与物体的距离、光的颜色、光的类型（环境光、自发光）物体与视点的距离（距离远则看到的光照效果弱）材质对光的反射、透射、吸收，其它物体的反射光影响等等。

**全局光照模型**：接近真实世界的光照考虑，包括环境光、其它物体的反射光、本身的透光效果、反光效果多种最终的结合非常复杂。
**局部光照模型**：一个点光源，仅考虑光照射到物体表面所产生的效果。
（a）定义为$I=I_e+I_d+I_s$（环境光强+漫反射光强+镜面反射光强）以下均是简单光照模型部分

**材质属性**：指物体表面对光的吸收，反射、透射性能，也会影响光照效果。也由环境反射率、漫反射率、镜面反射率、高光（镜面反射光的汇聚程度）等组成，==各种反射率与对应的光计算==得结果（**各通道颜色**对应的反射率不一样，这对应光的颜色，不同颜色通道光照都要进行计算）

| 材质 | RGB分量 | 环境反射率 | 漫反射率 | 镜面反射率 | 高光指数 |
| ---- | ------- | ---------- | -------- | ---------- | -------- |
|      | R       | 0.247      | 0.752    | 0.628      | 50       |
| 金   | G       | 0.2        | 0.606    | 0.556      | 50       |
|      | B       | 0.075      | 0.226    | 0.366      | 50       |
|      | R       | 0.192      | 0.508    | 0.508      | 50       |
| 银   | G       | 0.192      | 0.508    | 0.508      | 50       |
|      | B       | 0.192      | 0.508    | 0.508      | 50       |

**发射光模型**：描述物体的自发光，不参与它附近物体的光照。
**环境光模型**：天空，大地，周围场景的投射光。简单光照模型中用一个常项来近似模拟。$I_e=K_aI_a~~,K_a\in [0,1]为材质反射率,I_a$为环境光强.

**漫反射光模型**：对于粗糙物体处理反射光的一种模型，其从一点照射，从个方向散射，漫反射光只与光源位置有光，==与视点位置无关==。
Lambert余弦定律给出的`p点`漫反射模型：$I_d=K_dI_p\cos\theta,~~\theta\in [0,2\pi],K_d\in[0,1],~~I_p$为点光源入射光强，K_d_为材质漫反射率，θ为入射光与表面p点的法向量夹角，可有$\cos\theta = N*L$，NL为p点法向量与入射光点积（==小于0时也取0，表示非正面照射到p点==）

**镜面反射光模型**：有很强的方向性，只有在反射方向才能看到反射光效果，因此与视点位置有关。
（a）`R`是反射向量，记入射向量`L=光点 - 当前点`（注意这个方向）`webgl 中 R=reflect(-L,N)`==负的入射向量拿去计算==
（b）`V`为当前点到视点向量：`V=视点 - 当前点`（注意这个方向）
$$
I_s=K_sI_p\cos^n\alpha~~,0\leq\alpha\leq2\pi,K_s\in [0,1]~~,\begin{cases}I_p为p点处入射光强\\ K_s为材质镜面反射率\\ 
\alpha为视点位置方向V与反射方向R的夹角\\ \cos\alpha=RV, 小于0时也取0 \\ n为材质的高光指数 \end{cases}
$$
 **光源衰减**：光源位置到照射点应该逐渐衰减光照强度（视点一般距离物体太远时都不再渲染物体，因此不考虑到视点的衰减）
（a）$f(d)=\min(1,\frac{1}{c_0+c_1d+c_2d^2})$，c0，c1，c2都为衰减因子，自己取值调节即可。

**最终简单光照模型Phong**：还要**添加颜色**，材质是有多种颜色的，因此计算上3个颜色通道都要进行如下公式计算。
（a）$I=K_aI_a+\sum^{n-1}_{i=0}f(d)*[K_dI_{p,i}*max(NL,0)+K_sI_{p,i}*max(RV,0)^n]$，求和是多个点光源时的写法。每个点将各颜色通道值代入此式计算
（b）对最终结果==再进行归一化处理==（其可能会超过色值）与物体材质对应像素点设置进行 乘 或 加的操作。

**多边形的光滑着色**：每个平面都单个颜色时着色效果依然是有马赫带的，虽然增添三角形数量可以改善，但这带来更多消耗。
**GrouraudShader算法**：相邻的三角形都有1个共享点，该共享点法向量使用这些相邻平面的法向量求平均得到（最后每个三角形点都有其法向量），在渲染光照效果时使用此法向量代替光照模型中使用到的法向量，具体过程如下：

- 计算三角形各顶点的法向量（用其周围三角形平面的法向量均值）相邻三角形法向量和比上它们的模$N=(\sum^{n-1}_{i=0}N_i) / |\sum^{n-1}_{i=0}N_i|$。

- 对三角形各顶点调用呱噪模型计算光强。

- 再依据3个顶点的光强，用插值算法计算各边界上各顶点的光强插值。

- 三角形内部点光强计算：使用扫描线，用同一水平扫描线上的两个边界点进行插值。t的意义与计算同 <a href="#cha_mark1">查看</a>
  $$
  如a，c两点间插值: ~~I_d=(1-t)I_a+tI_c=\frac{y_c-y_d}{y_c-y_a}I_a+\frac{y_d-y_a}{y_c-y_a}I_c
  $$
  依次扫描各个要插值的点，代入计算即可。

- 特点：由于顶点处用的是计算光强，而中间则是用的插值光强，在高光处会出现少许痕迹。

**PhongShader算法**：与GrouraudShader稍有区别。

- 计算各三角形顶点的平均法向量。
- 利用插值计算三角形边界点的法向量。再插值计算三角形面内各点的法向量。
- 然后对各顶点的法向量计算光强。
- 对比GrouraudShader算法，有**更柔和，更平滑**。

# 十、阴影

**投影阴影**：利用投影中的“斜投影”，来计算一个物体投影到平面上的图形。
（1）用点光源的位置与物体表面当前点，用斜投影计算其在平面上的位置。
（2）若当前点的法向量与当前点的光源向量夹角`>90`则不计算该点。
（3）用计算了投影的点按其以前的三角形顶点顺序绘制为阴影。
（4）优缺点：计算快，适合高性能要求的场景。但是只适合投影到平面上。

```js
/**
   * 投影阴影计算
   * @param {number[]} lightPoint 点光源位置
   * @param {{points,indexs,normalizations}} objData 图形数据（） 
   plainY: 投影面的 y值
  */
  function castShadow(lightPoint, objData,plainY=-1) { 
    const { points, indexs, normalizations } = objData;
    const len = points.length;
    // 利用空间直线方程，与平面相交的计算
    let ry;
    let shadowArr = [],ligNOrmal,ixs = [];
    for (let i = 0,j=0, x; i < len; i+=3,j++){
      x = i;
      // 计算是否光线可照射到
      ligNOrmal = Vector3.calc(lightPoint, points.slice(x, x + 3), '-');
      if (Vector3.dot(ligNOrmal, normalizations.slice(x, x + 3)) < 0) continue;
      // 这里假设投影的平面为 xoz 平面，因此 y=plainY
      ry = (points[x + 1] - plainY) / (lightPoint[1] - points[x + 1]);

      shadowArr.push(points[x] - (lightPoint[0] - points[x]) * ry, plainY, points[x + 2] - (lightPoint[2] - points[x + 2]) * ry);
      ixs.push(j);
    }
    // 检测每个索引三角，如果1个三角形的3个索引 都在
    let indexArr = [];
    for (let j = 0, xi, yi, zi; j < indexs.length; j += 3){
      xi = ixs.indexOf(indexs[j]);
      yi = ixs.indexOf(indexs[j + 1]);
      zi = ixs.indexOf(indexs[j + 2]);
      
      if (xi>-1 && yi>=-1 && zi>=-1) indexArr.push(xi,yi,zi);
    }

    return {shadowArr,indexArr};
  }
```

**阴影贴图**：光源看不到的点都在阴影中！
（1）第一轮：将摄像机放到光源位置，使用`z-buffer`来计算得到深度缓冲区（并不渲染出来，因此不用进行光照着色等计算）
（2）保存当前使用的`MVP`矩阵（`投影矩阵x透视矩阵x模型变换矩阵`）称为`shadowMVP`矩阵。
（3）第二轮：正常渲染场景，对于每个像素点使用`shadowMVP`矩阵**转换到第一轮时对于的点**，然后查找其深度缓冲区中对应的点。
（4）若光源到该像素点距离“大于” 其在深度缓冲区点点与光源的 距离，则说明该点在阴影中。
（5）对此点的光源计算可只**采用环境光**，然后`shadowS = z1>z2 ? 0.5 : 1.0`与其相乘得到最后颜色值。

- **注意1**：一些库获取到的**深度值**是特殊归一化过的，第2轮计算深度值时也要==同样方法归一化==（`opengl:`$z=(Position.xyz/Position.w)/2.0+0.5$）
- **注意2**：`opengl`使用的纹理需要是`2^n`大小，因此你第一轮生成的纹理也要如此大小。
- **注意3**：因为zbuffer算法的z轴与绘制时的z轴方向相反，所以比较深度值时要反过来。
- **伪影1**：一些非阴影的地方也会变成阴影。比较时要给纹理上得到的深度值加偏移量`0.005`，
  **因为：**纹理的RGBA分量都是8位，而第2次计算的深度值一般`>16`位，所以纹理中的深度值会稍小。
- **伪影2**：一个阴影面中可能会出现部分分离出去的阴影块，可以对得到的纹理设置到夹紧边缘。
  `gl.texParameteri(gl.TEXTURE_2D,gl.texture_wrap_S,gl.CLAMP_TO_EDGE);  gl.texParameteri( 同左侧 ,gl.texture_wrap_T, 同左侧);`
- 阴影锯齿：常因为光源离物体较远造成。

**柔和阴影**：以上两种阴影绘制中都是绘制出的硬阴影，柔和阴影也可以优化阴影锯齿问题。
（a）而生活中常见的阴影有距离物体近阴影重，距离阴影远淡的特点（有个渐变效果）
（b）因为生活中多数时候都是平行光，而非点光源（最真实情况是平行光面上 每个点都对物体上各点进行投影得到阴影）
（c）渲染实现中则需要使用更节省性能的方法。即使用`PCF`（百分比邻近滤波，**在阴影贴图上查找**其周围像素）
（d）**方法一**：对邻近阴影的**64个**像素点使用其周围像素的均值，采样像素点多则效果好（更耗性能）
（e）**方法二**：只对当前像素点的周围`4个`像素点采样，因为像素点少，直接使用邻近像素**会造成结块**情况，因此需要加入抖动（随机）决定

- 用当前像素点在阴影贴图上的位置`texture_coord mod 2`（**模运算**）会得到4种结果：`(0,0), (0,1), (1,0), (1,1)`对应采样点如下：
  结果`(0,0)`：$p_1=(s_x-1.5,s_y+1.5),~p_2=(s_x-1.5,s_y-0.5),~p_3=(s_x+0.5,s_y+1.5),~p_4=(s_x+0.5,s_y-0.5)$
  结果`(0,1)`：$p_1=(s_x-1.5,s_y+0.5),~p_2=(s_x-1.5,s_y-1.5),~p_3=(s_x+0.5,s_y+0.5),~p_4=(s_x+0.5,s_y-1.5)$
  结果`(1,0)`：$p_1=(s_x-0.5,s_y+1.5),~p_2=(s_x-0.5,s_y-0.5),~p_3=(s_x+1.5,s_y+1.5),~p_4=(s_x+1.5,s_y-0.5)$
  结果`(1,1)`：$p_1=(s_x-0.5,s_y+0.5),~p_2=(s_x-0.5,s_y-1.5),~p_3=(s_x+1.5,s_y+0.5),~p_4=(s_x+1.5,s_y-1.5)$
  得到的4个采样点坐标，获取它们是否在阴影中（如`shadow=在阴影中?0.5: 1.0`），`相加/4.0`作为光照中的系数使用。

- **注意**：1.5，0.5这些值对于物体模型中的坐标来说**太大，可以适当减小**。

  ```glsl
  float shadowFactor = 0.0;
  // 模型坐标点 都是 0.5 ,1.5 对于理论上提到的 —1.5， 0.5 有点大
  // 因此这里 对计算后的坐标进行缩小，这样柔和阴影的点就只会出现在 实质阴影附近
  float scale = 0.112;
  // 4中情况的偏移坐标 计算小技巧
  vec2 p1xy = vec2(-1.5+fxy.x,1.5-fxy.y) * scale;
  vec2 p2xy = vec2(-1.5+fxy.x,-0.5-fxy.y)  * scale;
  vec2 p3xy = vec2(0.5-fxy.x,1.5-fxy.y)  * scale;
  vec2 p4xy = vec2(0.5+fxy.x,-0.5-fxy.y)  * scale;
  // 4次纹理深度查找 得到
  shadowFactor += textz(p1xy);
  shadowFactor += textz(p2xy);
  shadowFactor += textz(p3xy);
  shadowFactor += textz(p4xy);
  shadowFactor = shadowFactor / 4.0;
  ```

  

**阴影体**：
（1）计算物体阴影所绘覆盖的空间范围，然后计算在次范围内的物体，给它们着色时绘制阴影效果
（2）此方法不容易产生伪影，但十分消耗性能。

# 十1、纹理

**简介**：纹理定义在纹理空间中，用规范的`(u,v)`坐标表示（左下为`(0,0)`，右上为`(1,1)`**真实的纹理坐标**为其**图像的宽高空间**）纹理映射要建立物体表面各点与纹理各点的对应，取图像上各像素点的色值映射到物体。
（a）这需要两次映射，第一次是从纹理空间映射到参数空间（物体空间），第二次是从参数空间映射到屏幕空间（透射投影完成）

颜色纹理：定义好纹理的漫反射率，镜面反射率等，用光照渲染时依然可以呈现相应的明暗效果。
**简单纹理读入**：（曲面拉伸也会导致纹理随着拉伸）
（1）先得到真实纹理的坐标空间。
（2）确定当前曲面空间（如曲面x，y值的最大最小）
（3）曲面上某一点(x0,y0,z0)，用插值公式和当前曲面空间计算得出两个方向的`t`。
（4）再在纹理空间上，根据插值公式计算得出对应纹理坐标（u,v）取像素点色值。

**几何纹理**：适当的扰乱物体网格表面部分法向量，使光照渲染时产生阴暗，光亮交错产生凹凸效果。可使用正弦函数对其扰动

```glsl
float a = 0.25,b = 100.0; // a 控制凸起高度,b控制凸起宽度
float x = originalVertex.x, y = originalVertex.y, z = originalVertex.z;
vec3 N = originalVertex + vec3(a*sin(b*x), a*sin(b*y), a*sin(b*z));
```

**法线贴图**：直接将**法向量存储在一张贴图**中，替代几何纹理的一种方法。
（a）法向量的`x,y,z`对应图像中的`r,g,b`来存储。
（b）rgb的存储范围是`[0,1]`但法向量单位化后的存储空间为`[-1,1]`所以需要转换。$R=(N_x+1)/2,G=(N_y+1)/2,B=(N_z+1)/2$。

高度图：使用纹理图像来存储高度值，贴图时提升顶点的高度方法。

**两步纹理映射**：先将纹理映射到一个中介曲面（`S映射`），再从其映射到三维物体上（`O映射`），解决了无参数化的纹理映射。
（1）目标物体为回转体，中介曲面一般选用圆柱。圆柱用参数公式（极坐标）表示：【1】$\begin{cases}x=r\sin\theta\\ y=hφ\\z=r\cos\theta\end{cases},~~0<\varphi <1,0<\theta <2\pi$。
（2）与纹理坐标空间的**对应关系**：$u=\frac{\theta}{2\pi},~~v=\varphi=\frac{y}{h}$。
（3）**3维物体**上一点$(x_w,y_w,z_w)$先计算对应的：$(\theta,\varphi)=(\arctan(x_w/z_w),y_w/h)$（==O映射中会得到该物体的点==）
（4）然后计算S映射：$(\theta,h)=[c(\theta,\theta_0),(h-h_0)/d]$，将**最后得到的**h，θ，φ代入【1】【2】中就可得到圆柱上那个点用哪个纹理像素
（5）上式中：`c,d`是纹理比例系数。$\theta_0,h_0$是初始值，对应纹理在柱面上的**初始位置**。
（6）O映射：可用此方法将其映射到任何物体上。有以下几个方法（把圆柱体放到空间中计算它们的相交？？）

- 反射光线法：视点出发向物体发出一条光线，跟踪其与物体表面发出的反射光线（这个点代入（3）中）直至其与中介曲面相交（**常用**）

- 物体法向法：跟踪物体表面的法线，直至其与中介曲面相交。然后将这个物体表面的点代入（3）

- 物体中心法：跟踪物体中心与物体上一点的连线，直至其与曲面相交。

- 中介曲面法向法：跟踪从中介曲面上的一点沿其法线方向发出的一条光线，与物体表面的交点。

  |                | 平面 | 圆柱面 | 立方体   | 球面     |
  | -------------- | ---- | ------ | -------- | -------- |
  | 物体法向法     | 冗余 | 不合适 | 不太合适 | 不太合适 |
  | 物体中心法     | 冗余 | 不合适 | 合适     | 合适     |
  | 中介曲面法向法 | 合适 | 合适   | 合适     | 冗余     |

**环境映射**：有镜面效果的材质需要映射出周围的环境。基于光线追踪的方法较为费时；速度快的方法是先将其它渲染好的物体作为一副场景图保存，然后渲染该物体计算环境映射时从其表面计算反射光线，用交于周围环境的点作为其映射上。

- **球面映射**：把物体当成球体看待，计算物体p点的法向量，然后计算其对应到的纹理坐标。
  （2）视向量V，p点处法向量N，p点反射向量R。$N=R+V=(r_x,r_y,r_z)$。（把已渲染好的场景当做一张纹理图）
  （3）N对应的**纹理坐标**为：$u=r_x/m + 1/2,~~v=r_y/m+ 1/2,~~m=2\sqrt{r^2_x+r^2_y+r^2_z}$。
  （4）在上下两极点处会出现比较严重的纹理变形。

- **立方体映射**：是闭球面映射更加常用的方法。
  （1）生成特殊的6张图形，对应立方体的6个面。通过物体点p处的反射向量`R=(rx,ry,rz)`（该物体形状的真实反射向量）
  （2）从R中找到绝对值最大的那个分量值（再根据正负号用对应那个方向的面的纹理图），然后其余两个分量 比上这个绝对值，再归一化处理。
  （3）如`R=(-3.2,5.1,-8.4)`则计算的纹理坐标：$u=(-3.2/8.4 + 1.0)/2,~~v=(5.1/8.4 + 1.0)/2$用==背面方向的纹理图==（-8.4为指向z负半轴）

- **反射映射**：
  （1）将摄像机放置到可反射的表面中间位置，绘制此处观察到的场景作为纹理。

  （2）第2论绘制此面时，使用其法向量和视线向量计算各点处的反射向量。
  （3）用该反射向量来查找纹理进行渲染。

**投影纹理映射**：该方法先将纹理投影到一个表面上，然后将这个表面投影到场景中。
（a）这不需要预先绑定纹理坐标，这与纹理图象无关，要更换纹理时改变投影机即可。
（b）可有效避免纹理扭曲。

**三维纹理**：平面纹理包裹曲面是一种非线性映射，3维物体为三角形拼接，在交点处很难保持连续性。三维纹理是计算机生成的纹理，在这些交点处使用特殊的处理函数来生成，或从纹理上采样得到当前点色值。	==webgl中没有内置 3d纹理？【待深入】==
（1）按照图形的表面顶点生成一个存储色值的三维数组。
（2）将字节数组加载到纹理对象中。
（3）确定对象顶点的适当3d纹理坐标。
（4）片段着色器中使用适当的采样器来纹理化对象。

```glsl
// 条纹的3d纹理图案
void generate3Dpattern(){
    for(int x=0;x<texWidth;x++){
        for(int y=0;y<texHeight;y++){
            if((y/10)%2==0) tex3Dpattern[x][y][z] = 0.0;
            else tex3Dpattern[x][y][z] = 1.0;
        }
    }
}
```

**MinMap纹理反走样**：一般纹理贴到3维物体上，如一个长方形透视投影后近处的纹理被放大，远处的缩小，所以常出现**摩尔纹**（数码相机也常遇到）
（1）MipMap思想是对原图进行几次缩小（每次缩小为原来一半）分别得到几张分辨率不同的纹理图片（缩小是用 ==每4个像素点的均值变为1个像素点==实现）
（2）然后如果哪个平面使用了此图，它会在**距离视点近的像素**部点部分使用高清的纹理图上的像素，**远离视点部分**使用分辨率较低的纹理图。
（3）可生成的不同分辨率图片数：$m=log_2n+1$，n为图片宽（**宽和高**都要满足$2^n$，可以不是正方形）
（4）所选取的高清，和低分辨率像素点的中间 部分，可使用线性插值完成填充。

# 十2、天空&背景

如果使用普通的添加模型，背景，再透视投影为3d场景这将会非常消耗性能。

**天空盒**：使用立方体贴图，将有天空，地平线背景的图像作为纹理使用。
（1）实例化1个立方体对象。
（2）准备立方体贴图素材，因为放到立方体中看起来又不能是立方体效果，所以需要特殊处理过的6张纹理图（用工具处理）
（3）相机放置于立方体中，立方体并不需要绘制得特别大，只需要合适的大小。
（4）然后绘制立方体贴图时**禁用深度测试**，这样贴图部分深度值就始终为1（最小值）
（5）绘制场景内物体时再开启深度测试。
（6）立方体贴图容**易受到接缝处畸变**的影响。

**穹顶**：是用带纹理的球体或半球体实现天空效果。
（1）`不易受到畸变、接缝的影响`。
（2）比立方体贴图需要更多的点，更复杂。

**简单天空盒实现**：
（1）准备6个面的6张图片。
（2）准备绘制一个立方体。
（3）依然使用2D纹理，对应的纹理绘制到立法体每个面上即可。

**立方体贴图实现**：多数图形学库都有支持立方体贴图api，可直接使用。
（a）注意：绘制的立方体顶点的**组绕顺序** ==需要是顺时针==的，因为相机是放到立方体中的。
（b）可以使用设置组绕顺序方向来绘制。
（c）立方体不用绘制太大，不然拉伸图片也会导致失真。

**穹顶实现**：
（1）绘制一个半球形物体。准备一张全景图。
（2）使用2d贴图，球体的每个顶点坐标都要有一个纹理坐标对应。
（3）对应关系就是（半球体顶点坐标展开也是一个长方形形状）中间点用`0~1`中的比例位置。
（4）以下是1个半球体，带底面的坐标生成。

```js
function shpareSkyArray(r, precision, circle = true) {
  if (90 % precision !== 0) {
    return console.error("[sky arr] precision 必须可被 90 整除");
  }
  const a = 0, b = 0, c = 0;
  const angle = precision; // 每份所占角度
  const hudu = (s) => (s / 180) * Math.PI;
  const rows = 90 / angle + 1; // 所拥有的行数
  const columns = 360 / angle; // 每行的列数
  const sin = Math.sin, cos = Math.cos;
  const points = []; // 球面顶点
  const normalization = []; // 各点法向量
  const textureCoord = []; // 对应的 纹理坐标

  const fix6Fn = (n) => Number(n.toFixed(6));
  const xsCoord = [];

  /* 底部顶点（全同，这里是底面的中心顶点）*/
  let _columns = circle ? columns + 1 : columns;

  for (let i = 0; i < _columns; i++) {
    points.push(a, b, c);
    normalization.push(0, -1, 0);
    xsCoord.push(fix6Fn(i / (_columns - 1)));
    textureCoord.push(xsCoord[i], 0.0);
  }

  // 中间顶点
  for (let i = 0, by, br; i < rows - 1; i++) {
    by = fix6Fn(b + r * sin(hudu(i * angle))); // y坐标
    br = Math.abs(r * cos(hudu(i * angle))); // 当前所在行的半径

    let fp, fn;

    for (let j = 0, bx, bz; j < columns; j++) {
      bx = fix6Fn(a + br * sin(hudu(j * angle)));
      bz = fix6Fn(c + br * cos(hudu(j * angle)));
      // 保存起始点
      if (j === 0) {
        fp = [bx, by, bz];
        fn = [bx - a, by - b, bz - c];
      }

      points.push(bx, by, bz);
      normalization.push(bx - a, by - b, bz - c);
      // 不需要底
      //textureCoord.push(xsCoord[j], fix6Fn(i / (rows - 1)));
      // 有底的处理
      textureCoord.push(xsCoord[j], fix6Fn((i + 1) / rows));
    }
    // 结尾点与起始点重合，这样在其球形纹理才能很好的贴合
    if (circle) {
      points.push(...fp);
      normalization.push(...fn);
      textureCoord.push(xsCoord[xsCoord.length - 1], fix6Fn((i + 1) / rows));
    }
  }
  // 顶部顶点（全同）
  for (let i = 0; i < _columns; i++) {
    points.push(a, b + r, c);
    normalization.push(0, 1, 0);
    textureCoord.push(xsCoord[i], 1.0);
  }

  return {
    points,
    rows: rows + 1, //rows+1 【不要底时为rows】
    columns: _columns,
    normalization,
    textureCoord,
  };
}
```



# 十3、雾

现实生活中大多数情况都存在雾，只是雾在较少时我们不太关注。场景中可**适当加入雾**来凸显真实。

**线性雾**：比较简单的实现，如下
（1）在指定范围内用当前点计算其距离雾的起点 和终点距离的比值，作为当前点颜色与雾的颜色的插值参数。
（2）**插值得到的色值**作为最终显示的色值。

```glsl
// 顶点着色器部分
varying float v_dist;

void main(){
    // 转换到视空间后的点计算其到视点的距离
    v_dist = distance(u_modelMatrix * a_position,u_eye);
}

// 片段着色器部分
vec4 u_fogColor = vec4(0.7,0.8,0.9,1.0); // 雾的颜色一般偏灰色，或淡蓝
float fogStart = 0.2; float fogEnd = 5.0; // 雾距离视点的起始 和结束距离
void main(){
    vec4 obj_color = vec4(1.0,0.2,0.8,1.0); // 图形的本色
    // 计算插值比例 并保证其在 0~1之间
    float fogFactor = clamp( (fogEnd-v_dist)/(fogEnd-fogStart),0.0,1.0 );
    // 使用插值函数，插值参数 计算当前得到的颜色
    gl_FragColor = mix(u_fogColor,obj_color,fogFactor);
}
```

# 十4、噪声

使用噪声可以模拟出许多自然现象，比如火影、水、烟雾、木纹、矿物、地形等。【[各种噪声参考](https://zhuanlan.zhihu.com/p/346844820)】
从数学上讲噪声函数实际上是一个从$R^n$到R的映射。它以n维点作为输入返回一个浮点数。1D噪声通常用于物体动画，2D和3D噪声用于生成物体表面纹理，另外3D噪声对于体积渲染特别有用。4D噪声则是加上第4个维度参数，比如时间，可以做动画。

**白噪声**：指随机无规律生成的噪声 。

**value噪声**：与perlin噪声类似，不过线性插值参数的平滑是使用周围9个点的权重平均处理得到的。

- **1维噪声生成**：

  ```js
  const MAX_VERICES = 10;
  // 线性插值
  function lerp(a,b,t){
      return a + t*(b-a);
  }
  
  function cosineRemap(t,a, b) {
  	// 简谐运动函数，对t进行偏移
      const tRemapCosine = (1 - Math.cos(t * Math.PI)) * 0.5;
      return lerp(a, b,tRemapCosine);
  }
  
  function valueNoise1D(x) {
  	const xFloor = Math.floor(x);
  	// 超过最大值就循环处理
  	const xMin = xFloor % MAX_VERICES;
  	const t = x - xFloor; // 小数部分用作插值参数
      // <9时用 其 +1 作为另一端插值，
      const xMax = (xMin === MAX_VERICES - 1) ? 0 : xMin + 1;
  
      return cosineRemap(xMin, xMax, t);
  }
  ```

- **二维噪声生成**：[掘金参考地址](https://juejin.cn/post/7147492992540999716)

  ```js
  // 线性插值参数平滑函数
  function smoothStep(min, max, t) {
      return t * t * (3 - 2 * t);
  }
  
  class ValueNoise2D {
    constructor() {
      this.vertices = [];
      this.K_MAX_TABLE_SIZE = 256;
      this.K_MAX_TABLE_SIZE_MASK = this.K_MAX_TABLE_SIZE - 1;
  	// 随机生成值作为
      for (let i = 0; i < this.K_MAX_TABLE_SIZE * this.K_MAX_TABLE_SIZE; i++) {
        this.vertices[i] = Math.random();
      }
    }
  
    computeX(p) {
      const xi = Math.floor(p.x);
      const yi = Math.floor(p.y);
      // 两个方向的插值参数
      const s = p.x - xi;
      const t = p.y - yi;
  
      const rx0 = xi & this.K_MAX_TABLE_SIZE_MASK;
      const rx1 = (rx0 + 1) & this.K_MAX_TABLE_SIZE_MASK;
      const ry0 = yi & this.K_MAX_TABLE_SIZE_MASK;
      const ry1 = (ry0 + 1) & this.K_MAX_TABLE_SIZE_MASK;
      //通过置换表查找四个顶点处的随机值
      const c00 = this.vertices[ry0 * this.K_MAX_TABLE_SIZE_MASK + rx0];
      const c10 = this.vertices[ry0 * this.K_MAX_TABLE_SIZE_MASK + rx1];
      const c01 = this.vertices[ry1 * this.K_MAX_TABLE_SIZE_MASK + rx0];
      const c11 = this.vertices[ry1 * this.K_MAX_TABLE_SIZE_MASK + rx1];
      //对得到的s和t做平滑处理
      const ss = smoothStep(s);
      const st = smoothStep(t);
      //双线性插值得到p的值
      const a = lerp(c00, c10, ss);
      const b = lerp(c01, c11, ss);
  
      return lerp(a, b, st);
    }
  }
  ```

**perlin噪声**：柏林噪声，一个噪声函数基本上是一个种子随机发生器。
它需要一个整数作为参数，然后根据这个参数返回一个随机数。如果你两次都传**同一个参数**进来，它就会**产生两次相同的数**（重要的点）

- **2维噪声生成**：对于2d坐标系中的一个点`p(x,y)`，如下操作（数学坐标系）
  （1）对p点，其整数部分作为晶格左下脚顶点`pn`，小数部分作为两个方向插值参数。
  （2）两个插值参数进行平滑处理（不然由于不自然变化的梯度值，会**导致块状**）
  （3）`pn`两个轴各`+1`得到其它3个晶格顶点（$(x+1,y), (x,y+1),(x+1,y+1)$）
  （4）再根据这4个晶格点从哈希表中获取它们对应的`hash`值的**梯度向量**。
  （5）用`p`减去4个晶格点，得到4个向量，4个向量分别与对应点的`hash梯度向量`，做==点积==，得到**4个标量**。
  （6）对4个标量进行双线性插值，得到最后1个浮点数即为`p点`对应的噪声值。
  （7）对最后的值校验，需要在（-1,1）区间，与rbg值相乘？？

  ```js
  // 生成0-255 哈希值表 （图片一般根据mipmap 宽/高为 2^n）
  const hash256 = [];
  for(let i=0;i<256;i++){
      hash256.push(parseInt(Math.random()*256));
  }
  const hash512 = [...hash256,...hash256]; // 防止索引溢出而放置的 两倍
  
  // 梯度的得来 hash = p[px mod 255 + py mod 255] 共有4个方向的梯度向量
  function dot(hash,x,y){
      // hash值与3 做与运算 得到0~3
      switch(hash & 3){
          case 0: return x+y; // 对应的梯度向量 (1,1)
          case 1: return -x+y; // 对应的梯度向量 (-1,1)
          case 2: return x-y; // 对应的梯度向量 (1,-1)
          case 3: return -x-y; // 对应的梯度向量 (-1,-1)
      }
  }
  
  // 对插值参数的平滑处理
  function fade(t){
      return Math.pow(t,3) * (t * (t*6 - 15) + 10);
  }
  // 线性插值
  function lerp(t,a,b){
      return a + t*(b-a);
  }
  
  function perlin2D(x,y){
      const p = {x:x,y:y};
  	// 计算作为 晶格网中的第一个点（坐下点）
  	var xn = Math.floor(p.x), yn = Math.floor(p.y);
  	// 用于双线性插值 的参数
  	const fx = p.x - xn, fy = p.y - yn;
      const u = fade(fx), v = fade(fy);
      xn = xn & 255; yn = yn & 255; // 与运算， 使值限定在0-255内
  	// 4个晶格 哈希值
      const aa = hash512[hash512[xn] + yn]; // 晶格左下脚哈希值
      const ab = hash512[hash512[xn+1] + yn]; // 晶格右下脚哈希值
      const ba = hash512[hash512[xn] + yn + 1]; // 晶格左上脚哈希值
      const bb = hash512[hash512[xn + 1] + yn + 1]; // 晶格右上脚哈希值
      // 分别插值
      const v1 = lerp(u, dot(aa,fx,fy), dot(ab,fx-1, fy)); // x轴下方两个值 插值
      const v2 = lerp(u, dot(ba,fx,fy-1), dot(bb,fx-1,fy-1)); // x轴上方两个值 插值
      const v3 = lerp(v, v1, v2);
      return v3;
  }
  ```

- **3维柏林噪声**：在2维的基础上增加晶格点数，计算的向量数，哈希值数也增加，最后变为3维线性插值，即该柏林算法时间复杂度为$O(2^n)$

- 噪声归一化：最好的归一化方法是能知道最大的噪声值，然后`每个噪声值/最大噪声值`，或者用1个较大的噪声值代替最大值，最后值用于颜色值。

- **使用参考**：

  ```js
  let arr = [];
  let temp = 0;
  // 中间需要有小数，所以每次 +=0.1。25.5就相当于生成1个 255x255的图像
  for (let i = 0; i < 25.5; i += 0.1) {
  	for (let j = 0; j < 25.5; j += 0.1) {
          // +1  /2 是为了将区间调整到 0-1
          temp = Math.round((ns.perlin2D(i, j) + 1) / 2 * M);
          arr.push(temp, temp, temp, 255);
      }
  }
  ```

  

**FBM分形噪声**：`(Fractal Brown Motion)`分形布朗运动，分形噪声叠加。是1968年Mandelbrot和Ness两人提出的一种数学模型，它主要**用于描述**自然界的山脉、云层、地形地貌以及模拟星球表面等不规则形状阶。它又是理想的不规则扩散和分形随机行走的基础。

```js
// 引入振幅amplitude，频率frequency，与噪声函数运算 叠加几次后往往得到更接近自然的随机
const amplitude = 1;
const frequency = 1;
// 分形叠加次数 通常被设置为 3，5 或者 7
const layers = 5;
let noiseSum = 0;
for (let i = 0; i < layers; i++) {
	noiseSum += perlin2D(x * frequency, y*frequency) * amplitude;
    // 对噪声取绝对值一般可以得到 尖锐的湍流（turbulence）效果
    // noiseSum += Math.abs(perlin2D(x * frequency, y*frequency)) * amplitude;
    amplitude *= 0.5;
    frequency *= 2;
}

```

**simplex噪声**：与perline噪声类似，且也是同一作者。
（a）指在N维下， N+1个点即可构成凸多面体。比如在二维下，平面可以看成**正三角形的拼接**。在三维下，空间可以看成正四面体的拼接。
（b）可以减少我们插值时所需要的顶点的个数，加快运行速度。运行**时间复杂度**由$O(2^n)$降低为$O(n^2)$，因此噪声维度越高，优化效果就越明显。
（c）单形网格与直角坐标网格的互相变换：
$$
单形网格到坐标网格=\begin{cases}F=\frac{\sqrt{3}-1}{2}\\ x'=x+(x+y)*F\\ y'=y+(x+y)*F\end{cases},~~
更多维时=\begin{cases}F=\frac{\sqrt{N}-1}{N}\\ x'=x+(x+y+z+..)*F\\ y'=y+(x+y+z+..)*F\end{cases},~~
坐标到单形=\begin{cases}G=\frac{3-\sqrt{3}}{6}\\ x=x'-(x'+y')*G\\ y=y'+(x'+y')*G\end{cases}
$$
（d）有了以上转换后，对于输入的点`p(x,y)`同样找到晶格网中的4个直角坐标点，再转换到单形网格中。
（e）`simplex`中只需要**3个点**即可，通过判断输入点是在**上三角形**还是在**下三角形**，来选择用哪3个点。
（f）对**点p**，`x<=y`则用上三角形，`x>y`则用下三角形。

<img src="E:/VNote/IT/_v_images/simplex.webp" style="height:250px;"/>

（g）依然同perlin噪声一样，计算p到3个单形网格点的向量、3个点的hash梯度向量，计算点积。
（h）**衰减函数**：晶格网中不适合线性插值，是衰减函数替代它。$f(r,x,y)=(max[0,(r^2-x^2-y^2)])^4$（==单形网中的x，y==）r是以点`(x,y)`为中心，到对面三角形底的高度值。
（m）最后归一化：`70.0 * (n0 + n1 + n2)`，70.0是二维情况使用。