# A、javascript

:::alert-info
**简介**：JavaScript 由 3 部分组成：**ECMAScript**：解释器。翻译兼容性：完全兼容。**DOM**：Document Object Model （文本对象）兼容性：部分不兼容。**BOM**：Browser Object Model （浏览器对象）兼容性：不兼容（例如 IE，谷歌，火狐，不可能兼容），核心是 window，全局对象。dom 针对的是标准的客户端控件，html 标记的这些浏览器展现的内容。bom 针对的是浏览器，BOM 是浏览器对象模型，DOM 是文档对象模型，前者是对浏览器本身进行操作，而后者是对浏览器（可看成容器）内的内容进行操作。js 是**脚本语言**、**单线程**语言。
:::

## 1、数据类型：

数据类型包括：数值、字符串、布尔、null(表示尚未存在的对象)、undefined(当声明的变量还未被初始化时，变量的默认值为 undefined。)、对象(对象又包括列表、函数、字典)，6 种。#alert(null == undefined); //output "true" 。ert(null === undefined); //output "false"

### 一、数值：

`parseInt("fjdk889")`//转为整型 889,剔除字符串。
`parseFloat()`//转为 float 型。
`num.toFixed(2)`;//保留小数位数。8
进制，十六进制数也可直接写入：`var v = 070`#八进制的 56。`var c = 0XA`#16 进制的 10。
**转为字符串**：num.toString();

- **含 e 的数**：一般表示极大极小值`var m = 3.125e7`#等价于`3.125 * 10^7`。`var c = 3e - 7`#0.00....03。
- **浮点数计算精度丢失问题**：`console.log(24314310.3412 / 100000)>>243.14310341200002`。
  所有编程语言都存在的问题，这是由于计算机本身特性导致的。小数位数过长，或有时计算中小数点参与移动。所以前端尽量不要使用浮点数的计算。
  **解决思路**：将小数转为整数，按特别方法计算后再移动小数点。
  数值与字符串的运算：`1 + "1" == "1" + "1" = '11'`#除了+是字符串连接，其它运算操作符情况会被先当做数值计算。
- **NaN**：用于表示一个本应该是数值，返回却是非数值的情况，如数值比上 0，NaN 与其它数值操作同为 NaN，`NaN == NaN返回false`。用 isNaN()可检测。

### 二、字符：

其它类型转为 string：`String(val)`#无论 val 是什么类型都会转为对应的字符串。

```js
parseInt("0xAA", 16); //parseInt第二个参数可以指定将字符串转为直接的进制数。0xAA本身是16进制。
x.toString(); //转为字符串。`x.replace(/target/g,'')`//替换,g表示所有满足的都替换。`x.concat(“a”,”b”)`//可与x连接多个字符串。
x.charAt(index); //查找字符串的对应下标的值,`“justice”.charAt(1)=”u”`。
"a".toUpperCase(); //方法将小写字母转换为大写,`"A".toLowerCase()`#将大写字母转为小写。
str.substring(start, end); //提取字符串中介于两个下标间的字符串，一个参数时为start，截取后面所有。不改变原数据的值。
str.substr(start, length); //第二个参数为选择从start起截取多少个长度字符。<b c=r>不改变原数据的值。</b>
str.indexOf("aa"); //查找字符串位置。
s = "fdfd_fdf".replace(/f/g, "a");
str.search("abc"); //找到子串开始位置。
str1.concat(str2); //连接两个字符串，返回一个新的值。
"*".repeat(3); //生成3个重复的字符。
"mm9plk4klj1hg".split(/\d/); //分割，也可指定字符分割。

"aaj,b_b".lastIndexOf("b", 2); // 返回最后一个字符出现的位置，第二个参数表示开始检索的位置。
var str = "大米:2.57斤/元,白菜:3.65元/斤";
var arr = str.match(/\d+(.\d+)?/g); //match()方法找到所有匹配的项，返回一个数组。
```

- **js 的正则表达式**：

```js
//i表示不区分大小写，g表示匹配全局，m表示可匹配多行。
var a = /e/i;
var b = new RegExp("e");
let reg = /ac/i;
reg.compile(reg);
//compile方法：该方法的作用是能够对正则表达式进行编译，被编译过的正则在使用的时候效率会更高，适合于对一个正则多次调用的情况下
console.log(a.test("aaebc")); // 返回布尔值
console.log(a.exec("kke,mme")); //只能找到第一个匹配项，放回一个列表形式的记录（有匹配到的值）。
```

### 三、数组：

```js
list.indexOf(1); //找到第一个1在列表中的位置，不在则返回-1。
list.includes(1); //是否包含1，返回布尔值。
list.join("-"); //将各元素用字符链接。
list.push(1); //在列表最后添加值。
list.pop(); //删除最后一个元素。
list.unshift(); //在数组最前端添加一个新的值。
var b = Array.from(carr); //from可实现浅拷贝
Array.from("dafl"); //[d,a,f,l]
[1, 2, 3].toString(); //"1,2,3"
Array.isArray({}); //false
arr.sort(); //不传参数的话，默认将arr中的值看成字符串来排序。
k = arr.from(T); //T转换成数组，T可以是字符串、列表、set。
var k = arr.concat([1, 2, 3]); //or concat(6)
var a = arr.some(function (item, index, arr) {
  if (item > 2) {
    return true;
  }
}); //返回true时会结束遍历，arr是整个数组本身。a为布尔值。
var a = arr.find((x) => {
  return x >= 4;
}); //与some类似用法。返回为true时对应的值。
var b = arr.filter((x) => {
  return x % 2 == 0;
}); //返回所有满足条件的值，是一个数组。
list.reverse(); //将数组倒置，[1,2,3].reverse();//[3,2,1]。
list.shift(); //移除第一个元素。
//instanceof//检查一个对象是否为了一个对象中的实例，Console.log(p1 instanceof p2);//p1是否为p2中的实例；
/*=============
    数组迭代器
===============*/
var e = ["a", "b", "c"].entries();
e.next().value; //[0, 'a'];
/*===============
    全条件满足（全满足时为true）
=================*/
const _all = [1, 2, 3].every((v) => {
  if (v < 4) {
    return true;
  } else {
    return false;
  }
});

var arr = [1, 8, 2, 4, 3, 9, 0];
// filter函数接收一个函数，这个函数作用于每一个值，返回true或false决定是否丢弃该值。
var r = arr.filter(function (s) {
  return s == 2; // 注意：IE9以下的版本没有trim()方法
});
//----sort()实现的排序的思想，传入函数作为参数，以灵活的用于各种情况。
arr.sort(function (a, b) {
  //火狐使用归并排序，google使用快速+插入。b在a之前，循环用a与b比较。
  if (a > b) {
    return 1; //1表示不变。
  } else if (a < b) {
    return -1; //表示a,b交换位置。
  } else {
    return 0;
  }
});
//----reduce()计算总和。
function getSum(total, num) {
  //total是上一次return的结果，num是数组元素
  console.info(">", total, num);
  return total + num;
}
console.warn(numbers.reduce(getSum));
```

- 注意：按引用类型操作的值，其后面操作改变了值，但前面值打印出来和改变后是一样的。

- **数组去重**：

```js
function unique(arr) {
  return Array.from(new Set(arr)); //使用集和。
}
unique([1, 1, "true", "true", true, true]);
//splice
var arr = [1, 2, 3, 4, 5, 6];
arr.splice(2); //删除2及之后的值。
arr.splice(0, 2); //表示删除0,1位置的值，第二个参数表示删除的个数。
//插入、第三个参数表示在当前索引后插入的数。
arr.splice(1, 0, 7); //[1,7,2,3,4,5,6] ！！
arr.splice(1, 1, 7); //[1,7,3,4,5,6]

arr.forEach(function (value, index, data) {});
```

### 四、map：

从对象中取出多个属性然后上传时的场景，如果用 obj.property 的方式取值，若缺少该值时程序可能会**不执行也不报错**。

```js
var obj = {a:1,b:3};
/*================
该方法创建的数据只是指针指向原型，添加时才会在自身数据上添加，不大建议使用！
==================*/
Object.create({a:1,b:2},{
    p: {
    value: 2,           // 属性值
    writable: true,     //  是否可以重写值
    enumerable: true,   //是否可枚举
    configurable: true  //是否可以修改以上几项配置
  }
});        //第二个参数配置属性控制。
/*=============================
           属性、原型操作
===============================*/
Object.getPrototypeOf(obj) == obj.prototype; //获取指定对象的原型（内部[[Prototype]]属性的值）
Object.getPrototypeOf(person1).name;         //"Nicholas",但不能通过此方法来更改。
Object.setPrototypeOf(vue,{v:2})             //设置一个指定的对象的原型
Object.getOwnPropertyDescriptors(obj);       //返回指定对象所有自身属性【原型属性不含有】
obj.hasOwnProperty('a');                     // 判断是否有指定属性
//getOwnPropertyNames()方法可以得到所有属性，包括对象的不可枚举属性。
Object.getOwnPropertyNames(Person.prototype);
//将对象的某个属性设置为是否可枚举。//----缺点：无法监听到增加和删除操作，无法监听到内部数组的改变。
Object.keys(obj).forEach((key) => {
        let value = obj[key];
        Object.defineProperty(obj, key, {
          get: function () {
            console.log("访问属性 name 触发");
            return value; // 定义访问该属性的返回值
          },
          set: function (newValue) {
            console.log("设置属性 name", newValue);
            value = newValue; // 修改该属性的值
          },
        });
      });
/*===============
    属性控制
=================*/
Object.is(obj1,obj2);              //可对比两个值是否相等
Object.freeze(obj);                //冻结该对象，不能对其做修改
Object.preventExtensions(obj);     //对象不能再添加新的属性。可修改，删除现有属性，不能添加新属性。
Object.seal(obj);                  //将obj密封，不可扩展、删除、修改属性特性。但可修改值。
/*=============================
            键值对操作
===============================*/
Object.keys({a:1,b:2});//可枚举出对象的属性。
Object.values(dict);//value值做一个数组
// 键值对按数组返回
Object.entries({a:3,b:8});//[['a',3],['b',8]]
obj.isPrototypeOf(obj2)            //判断obj是否在obj2的原型链上。
// res是有更新部分的数据，obj1是最终数据。
var res = Object.assign(obj1, obj2,...);//将obj1后的对象中的属性赋给obj1，相同的键值会覆盖。
```

Object.defineProperty()方法可传有三个参数，第一个是要监听的对象，第二个是参数是该对象中已有的属性或未有的属性，第三个参数是对象的形式，里面可以写两个方法，set 方法在改变目标对象中指定属性(第二个参数)时触发的函数，可传入一个参数表示被修改的值，get 方法在目标对象指定属性值被获取时触发。set 方法和 get 方法都是在对应的操作前就先触发的，比如：obj.name = 'jieke',是先触发 set 方法再运行 obj.name='jieke'语句；第三个参数中也可以写访问器属性：

```js
Object.defineProperty(obj, "name", {
  configurable: true, //表示能否通过delete删除此属性,默认为true
  writable: true, //表示能否修改此属性值，默认true
  enumerable: false, //表示该属性能否被for in等方法枚举，默认true
  value: "wcs", //直接为该属性赋值
});
```

在第三个参数中写以上属性都不能与 get,set 一起使用。

```js
Object.defineProperties(obj, {
  //defineProperties()方法同时设置多个值
  name: {
    value: "张三",
    configurable: false,
    writable: true,
    enumerable: true,
  },
  age: { value: "李四" },
});
Object.getOwnPropertyDescriptor(obj, "name"); //获取目标对象指定属性的描述
```

- [Object 方法集学习地址](https://www.cnblogs.com/mopagunda/p/8328084.html)
- **列表，字典均属于 Object 类型**，即：`[1,2] instanceof Object`#为 true，但`{a:1,b:2} instanceof Array`#为 false。
  **undefined**：派生自 null，因此`null==undefined`#返回 true，使用全等符号才会返回 false。已声明，未赋值的变量依然是 undefined。但是没有声明的值使用，会直接报错。然而使用`typeof no(未声明值)`#得到的也是 undefined 类型，所以 undefined 不属于 Object。
  **null**：表示一个空对象指针，因此用 typeof 检测时返回 object（但`null instanceof Object`返回 false）。如果该变量之后用于赋值一个对象，那初始赋值可以置为 null。
  **布尔值**：`0，空字符串、null、undefined、false`都是当做 false。
  **Set**：es6 新增数据类型，集合属于数学的概念。Set 属于 Object。

```js
// set转数组
const items = new Set([1, 2, 3, 4, 5]);
const array = Array.from(items);
```

**symbol**：es6 新加的数据类型，用于做唯一性标识。

```js
let id = Symbol("id"); //typeof id = symbol;
let obj = {
  [id]: "symbol", //普通枚举获取不到。
};
```

### 五、隐式转换：

在进行变量比较时，js 内部会对数据进行相应变换如下：（全等条件下回进行类型的比较，所以这些在**全等下不成立**）

- [] == true; //false []转换为字符串'',然后转换为数字 0,true 转换为数字 1，所以为 false
- [1,2,3] == '1,2,3' // true [1,2,3]转化为'1,2,3'，然后和'1,2,3'， so 结果为 true;
- [1] == 1; // true `对象先转换为字符串再转换为数字，二者再比较 [1] => '1' => 1 所以结果为 true
- **~~符号的使用**：对变量进行隐式转换。

```js
~~true == 1;
~~false == 0;
~~"" == 0;
```

**数据类型检测**：`console.log(typeof val)`#有 string、number、undefined、boolean、function、object（字典和 null 都显示这个）。
<b c=r>非引用类型（字符串、数值、布尔等）推荐使用 typeof 检测。</b><b c=r>引用类型（数组、object、自带对象 Date 等）推荐使用 instanceof 检测。</b>

```js
const a = [];
let _typ;
if (typeof a === "object") {
  if (a instanceof Array) {
    _typ = "array";
  } else if (a === null) {
    _typ = "null";
  } else if (a instanceof Set) {
    _typ = "set";
  }
  {
    _typ = "map";
  }
} else {
  _typ = typeof a;
}
console.info(_typ);
```

## 2、编码相关：

```js
encodeURIComponent("<svg>")#不会对 ASCII 字母和数字,标点字特殊符等进行编码
encodeURI('汉字');//url传参汉字时可以先encodeURI()对中文编码,浏览器会自动解码
decodeURI();// 再用decodeURI()转码，对汉字解码则不变。

escape()与unescape()://将url地址作为参数传参时可用
document.write(escape("Visit W3School!"))// Visit%20W3School%21
// escape()方法对输入内容进行编码转为机械码能让所有机型识别
document.write(unescape("?!=()#%&"))// %3F%21%3D%28%29%23%25%26
//unescape()方法对机械码进行转码，转为可识别码
//btoa()和atob(),这是属于base64的编解码。
var str = "javascript";
console.log(window.btoa(str))//amF2YXNjcmlwdA==
console.log(atob("amF2YXNjcmlwdA=="))// 'javascript'
```

**进制转换**：

```js
(10)
  .toString(16)(
    // =>"a"。//10进制转为16进制10进制转为16进制
    012
  )
  .toString(16)(
    // =>"a"。//8进制转为16进制//8进制转为16进制
    0x16
  )
  .toString(10)(
    // =>"22"。//16进制转为10进制
    0x16
  )
  .toString(8); // =>"26"。//16进制转为8进制
```

## 3、其它：

### a、SSE 与 WebSocket:

SSE(Server-Sent Eevents，服务器发送事件)用于创建到服务器的单向连接。

```js
// EventSource接受的参数必须同源。
// 使用message事件监听从服务器收到的消息，并存储在event.data对象里。
var source = new EventSource("http://127.0.0.1:8080/event/query");
//只要和服务器连接，就会触发open事件
source.addEventListener("open", function () {
  console.log("和服务器建立连接");
});

//处理服务器响应报文中的load事件
source.addEventListener("load", function (e) {
  console.log("服务器发送给客户端的数据为:" + e.data);
});

//如果服务器响应报文中没有指明事件，默认触发message事件
source.addEventListener("message", function (e) {
  console.log("服务器发送给客户端的数据为:" + e.data);
});

//发生错误，则会触发error事件
source.addEventListener("error", function (e) {
  console.log("服务器发送给客户端的数据为:" + e.data);
});
```

WebSocket 是一种在单个 TCP 连接上进行**全双工通讯的协议**，它允许服务端主动向客户端推送数据，浏览器和服务器只用完成一次握手两者之间即可创建持久性的连接，并进行双向数据传输。需要先安装 pywebsocket 支持 websocket 服务。

```js
if(window.WebSocket){
    // 继承webscoket类，传入url,可选子协议,wss为加密后的协议。
    var ws = new WebSocket("ws://url",[protocol]);
    ws.onopen = function(){// 连接建立时触发
        ws.send(data);//发送数据
    }
    ws.onmessage = function(res){alert(res);}// 接受到数据时触发
    ws.onclose = function(){//关闭时触发函数}
}
else{alert("连接错误")}
```

### b、H5 web Workers:

workers 是让一个 js 文件在后台执行不影响页面执行速度的一种技术,对一些需要处理大型的数据是一个不错的优化选择，且主流浏览器都支持(除了 IE）。可以用在 canvas 绘制大量图形时，将计算结果返回到主线程然后渲染。<b c=r>worker 是一个线程而不是微任务，宏任务的概念</b>

```js
var i = 0; //postMessage()方法将传入其中的值返回给调用它的worker
function start() {
  postMessage(i);
  i += 1;
  setTimeout(start, 1000);
}
// 另一个js文件中
(function () {
  if (typeof window.Worker != "undefined") {
    // 浏览器支持Worker
    var w = new Worker("js/a.js");
    //res为postMessage()返回的对象，res.data获取其中数据
    w.onmessage = function (res) {
      console.log(res.data);
    };
    w.terminate(); //终止worker
  }
})();
```

- **一键复制功能**:

```html
<button onclick="get()">点击复制</button>
<script>
  function get() {
    var int = document.createElement("input");
    int.value = "这是复制内容";
    document.body.appendChild(int); //添加到DOM中才能选择(使用select())
    int.select(); //选择input中的内容
    document.execCommand("Copy"); // 执行复制语句
    int.style.display = "none"; // 复制完后才能隐藏
  }
</script>
```

- **三元运算符**：三元运算符与 if 语句同样的作用，例：if(x>10 && x<50){alert("hello");}替为 `x>10 && x<50?alert("hello"):alert("flase")`。(两者等价问号前为判断条件，问号后为执行语句，冒号后为 else 时的语句)。
  三元运算符用于赋值：val = val>20 ? 20 : 10;//表示如果 val 大于 20val 值就为 20，否则为 10；
  三元运算符中写多条语句：a == 20 ? (a=15,alert(a)) : (a = 21,alert(a));

### c、 js 的异步原理：

浏览器每开一个窗口就是启动一个进程，js 代码的运行只使用了一个线程，所以 js 异步并不是真正的启动线程的异步。js 中的任务分为宏任务和微任务，<b c=r>js 会先运行主栈中的任务，然后取事件队列先运行微任务，然后运行宏任务</b>。<b c=b>DOM 的渲染本身是同步的操作</b>。渲染引擎是另一个线程在执行，为了 js 线程能控制渲染引擎的动作，<b c=v>每次 js 微任务执行完后会去检查一下是否需要渲染，所以每帧的渲染间 js 的计算不要太多</b>，不然会掉帧。

- [参考学习地址。](https://www.cnblogs.com/liangye/p/13461924.html)
  > **宏任务**：setTimeout，setInterval，Ajax，DOM 事件。**DOM 渲染后触发**。
  > **微任务**：async/await，then,catch,finally。**DOM 渲染前触发**。

```js
//promise中的代码则是一个主线程的执行。
let cc = new Promise((rs, rj) => {
  console.info("a");
  rs();
  console.info("b");
});
console.info("c");
setTimeout(() => {
  console.info("d");
}, 0);
cc.then(() => {
  console.info("e");
});
console.log("f");
//输出顺序：a,b,c,f,e,d
```

### c2、页面间传值：

1、url 传参。(域名或路径后将参数用?或#号分割,参数间用&分割)
2、cookie 缓存。(格式建议与 url 传参写成一样的)
3、Storage 缓存。(页面间调用 storage 中的值,将一个数组存入后会变为逗号分割)
4、window.open()+window.opener

```js
// 页面a：
var a = 55; // 页面a的对象
el.onclick = function () {
  window.open("b.html");
}; //打开一个新窗口
// 页面b:
console.log(window.opener.a); //window.opener会将前一个页面的所有对象封装为
//一个对象的形式，b页面可以使用，但对用户体验不好。
```

### d1、formData 的使用：

```js
const el = document.getElementById("form");
let fd = new FormData(el);    # 不传入元素时是一个空的表单。
formData.append("k1", "v2");
formData.delete("k1");
formData.has("k1"); // true
formData.set("k1", "1"); // 修改
formData.get("name"); // 获取key为name的第一个值
```

### e、时间：

```js
var dat = new Date();
dat.getFullYear(); // 获取年份
dat.getMonth() + 1; // 获取月份,从0开始所以需要加1
dat.getDate(); // 获取号数
dat.getHours(); // 获取小时
dat.getMinutes();// 分钟
dat.getTime(); //获取从1970/01/01至今过去的毫秒数。
dat.toUTCString(); // 将日期转换为字符串
dat.getDay(); // 获取星期
/*****获取指定时间左右的时间*******/
var dt1 = new Date();
var dt2 = new Date(dt1); // 将dt1当参数传入
dt2.setDate(dt1.getDate() + 5); //将今天的号数设置为5天之后的号数
// 或者（获取10分钟之前的时间）
var dy = 10*60*1000;
let dt3 = new Date(Date.parse(new Date())-dy);
// 与当日差距的天数时间
function dateScope(fromDate) {
  const _fromDate = fromDate || 0;
  const d1 = new Date();
  const d2 = new Date();

  d2.setDate(d1.getDate() + Number(_fromDate));

  const y1 = d2.getFullYear();
  const m1 = d2.getMonth() + 1;
  const date = d2.getDate();

  return `${y1}-${m1}-${date}`;
}
```

### f1、call()和 apply()的使用：

apply 和 call 的作用是回调，es6 之前很多回调都是使用它们；**Function.apply(obj,args)方法能接收两个参数**obj：这个对象将代替 Function 类里 this 对象。args：这个是数组，它将作为参数传给 Function（args-->arguments。call:和 apply 的意思一样,只不过是参数列表不一样。

```js
/*定义一个Person类*/
function Person(name, age) {
  this.name = name;
  this.age = age;
}
/*定义一个学生类*/
function Student(name, age, grade) {
  //Person.apply(this,arguments);//特点：this指代student对象，只接收2个参数，arguments为隐式类数组对象，用来接收传入的参数；
  Person.call(this, name, age); //特点：this指代student对象，可以接收任意多个参数
  this.grade = grade;
}
var student = new Student("zhangsan", 22, "二年级"); //方法Student()也是object的一个实例
//测试，相当于是借用apply()或call()方法来实现一个简单的继承。
alert(
  "name:" +
    student.name +
    "\n" +
    "age:" +
    student.age +
    "\n" +
    "grade:" +
    student.grade
);
```

//学生类里面我没有给 name 和 age 属性赋值啊,为什么又存在这两个属性的值呢,这个就是 apply 的神奇之处.

### f2、console：

console 模块不只 log()一个函数，全部如下：

- `console.log("%d年%d月%d日", 2017, 1, 8)`#打印，%是占位符。console.info()#信息。
- `console.warn()`#警告。
- `console.group("第一组信息");console.log("第一组第一条：我是张三");...console.groupEnd();`#作为一组展示出来。
- `console.error()`#打印错误。
- `console.dir()`可以显示一个对象所有的属性和方法。
- `console.dirxml()`用来显示网页的某个节点（node）所包含的 html/xml 代码。
- `console.assert(a===2)`用来判断一个表达式或变量是否为真。若为否会抛出异常。
- `console.table([[1,2,3],[4,5,6],[7,8,9]])`#打印表格
- console.time()和 console.timeEnd()，用来显示代码的运行时间。
- `console.profile("性能分析器");...中间代码;console.profileEnd("性能分析器");`

### f3、动画函数：

```js
function play() {
  console.log(a);
  window.requestAnimationFrame(play);
}
window.requestAnimationFrame(play); //开始第一帧
cancelAnimationFrame(); //方法取消动画。
```

### g、js 垃圾回收机制：

多数编程语言都带有垃圾回收机制。现在各大浏览器通常用采用的垃圾回收有两种方法：标记清除、引用计数。
减少 JavaScript 中的垃圾回收：
new 关键字就意味着一次内存分配，例如 new Foo()。最好的处理方法是：在初始化的时候新建对象，然后在后续过程中尽量多的重用这些创建好的对象。
为了最大限度的实现对象的重用，应该像避使用 new 语句一样避免使用{}来新建对象。
使用 delete x;手动删除一个变量。

### h、节流和防抖动：

所谓的节流就是指用户频繁操作同一个事件，但都是相同的请求，如重复提交表单中的数据，重复下拉刷新请求数据，这会频繁的消耗用户的流量但是无意义的，遇到这种情况做法：写一个定时器，规定时间内只允许操作一次。
而防抖动是指类似搜索框中要监听用户的输入实时获取将值传给后台获取相应的匹配项，但返回的候选项个数不一样会导致下拉展示条频繁变化抖动。解决：监听到用户输入后设定一个定义器，时间过后执行操作，如果期间接收到监听变化就取消前一个定是器，再重新创建一个，相当与只取最后一次操作，因为此时是最有效的操作。
这两种思想都类似，不过一个取第一次操作，一个取最后一次操作。[参考地址。](https://www.jianshu.com/p/11b206794dca)

## 4、循环和分支：

:::alert-primary
for in 循环会遍历原型上的属性，耗时更长，尽量避免使用。for 循环时，多数会读取数组 length 值，**用一个局部变量缓存它**，速度更快。
**基于函数**的循环迭代（map(),some(),...等）性能**比 for 循环要稍差**，尽量减少这一类的使用！
:::

**循环**：（for, while, do -while, for-in, for-of, map(),..）

```js
var a = 5;
switch (a) {
  case 1:
    a = 9;
    break; // 每个case完使用break;
  case 2: //匹配多个条件时写法。case相当于===，所以case 2 || 5这样的写法只等于2。
  case 5:
    alert("hello");
    break;
  default:
    // 没有匹配到时会运行default，使用switch时一定加上这个。
    alert("结束");
}
/*******for循环多条件*******/
// 多条件用逗号隔开时表示“或”，满足任1条件都会执行
for(let i=1,k=20;i<10,k>10;i++,k--){}
// 要求同时满足，用&&即可
for(let i=1,k=20;i<10 && k>10;i++,k--){}
```

- **for in 与 for of**：<i c=r>for 循环时，多数会读取数组 length 值，**用一个局部变量缓存它**，速度更快</i>

```js
// 在原型上绑定一些自定义属性。
Object.prototype.selProto = function (v) {
  console.info(v);
};
Array.prototype.ap = "hello ap";

var m = Object.create({ a: 5, b: 3 });
var n = [2, 4, 7];
//---for in（es5语法）会将上面自定义在原型上的属性也遍历出来。Array属于Object，所以ap依然在其中。
for (var i in n) {
  //---getOwnPropertyNames()获取只属于该对象的属性，包含length。
  //for in遍历时利用它来筛选。
  if (Object.getOwnPropertyNames(n).indexOf(i) !== -1) {
    console.info("in----", i);
  }
}
//---for of(es6语法)则输出值，且不会遍历原型上的自定义属性。
for (var j of n) {
  console.info("of----", j);
}
```

- 交换变量：`[x,y]=[y,x]`。
- 双非运算符：`const f=~~15.57;//15`#与 floor 效果一样，不过在值大于 2147483647 时会失效。
- 字符串转数字：`let a = +"13.456";//13.456`#与 parseInt，parseFloat 效果一致。
- 数字分隔符：`const H = 109_234_711;//109234711`#这种较大的数值时用分隔符并于查看。
- 感叹号：`!!"123"`#true，相当于 Boolean()方法对值变换。
- bind 的使用：

```js
function mskPhone(val) {
  console.info("this===", this);
  let _s = val.substr(0, 3);
  return _s + "*".repeat(3) + val.substr(7, 11);
}
var cc = mskPhone.bind({ a: 112 }); //bind的第一个参数是函数mskPhone的this，其它参数按序传入。
console.info("cc===", cc("18313746328")); //这里调用，参数接着上面的
```

**for 循环中使用定时器问题**：

```js
//由于var作用域为当前函数，而非当前代码块。
for (var i = 0; i < 5; i++) {
  setTimeout(function () {
    console.log(i); //5,5,5,5,5
  }, 200 * i);
}
//-----可以放到一个函数内使用。或者将var改为let。
for (var i = 0; i < 5; i++) {
  //这种匿名函数就相当于一个块及作用域。
  (function (index) {
    setTimeout(function () {
      console.log(index); //0,1,2,3,4
    }, 200 * index);
  })(i);
}
```

**分支**：（if-else, switch()）

- 条件情况较多时，`多使用switch()`，比 if-else 更易读，且**速度更快**。
- 将较**常出现的情况放在前面**判断，也能提升性能！
- 条件多时，嵌套的 if-else 比不嵌套的**速度更快**！（注意别嵌套太深）。
- 条件特别多时，可以使用查找表（数组/map 存储）；

```js
if (a < 10) {
  if (a > 5) {
  }
} else if (a >= 10) {
  if (a < 18) {
  }
}
```

## 6、BOM：

### [1]事件：

**事件流**：事件流描述的是从页面中接收事件的顺序。事件发生时会在元素节点与根节点之间按照特定的顺序传播，路径所经过的所有节点都会收到该事件，这个传播过程即 DOM 事件流。事件传播的顺序对应浏览器的两种事件流模型：捕获型事件流和冒泡型事件流。
冒泡型事件流：事件的传播是从最特定的事件目标到最不特定的事件目标。即从 DOM 树的叶子到根、到 window 对象。
捕获型事件流：事件的传播是从最不特定的事件目标到最特定的事件目标。即从 DOM 树的根到叶子。
**事件绑定**：

```js
<p onclick="start()"></p>; // 原生的事件绑定。
function start() {}
// js动态绑定事件
document.getElementById("myBtn").addEventListener("click", function (e) {
  // 第一个参数是事件类型，第二个参数是一个函数，会为其传入一个参数为事件对象，可以用e.target
  document.getElementById("demo").innerHTML = "Hello World";
});
/******文档加载完成事件*******/
window.addEventListener("load",function(){});
```

**事件冒泡与事件捕获**：由于老版本的浏览器不支持，因此很少有人使用事件捕获。我们也建议读者放心地使用事件冒泡，在有特殊需要时再使用事件捕获。
![paopao](\_v_images/20200424091838620_274839134.png =270x)
**DOM 事件流**：**先发生事件捕获再发生事件冒泡**，父元素捕获事件流（捕获阶段不会接收到事件），具体绑定事件的元素接收到事件后再发生事件冒泡。
在不同浏览器中，冒泡的程度不同：IE 6.0:div -> body -> html -> document。其他浏览器:div -> body -> html -> document -> window。
并不是所有的事件都能冒泡，以下事件不冒泡：blur、focus、load、unload。解决办法：

```js
if (event && event.stopPropagation) {
  // w3c标准
  //event.preventDefault():阻止默认行为；
  event.stopPropagation(); //阻止冒泡1.
} else {
  // IE系列 IE 678
  event.cancelBubble = true;
}
```

**鼠标事件**：

```js
var el = document.getElementById("el");
el.onmouseenter = function(e){}          //鼠标在进入时触发
el.onmousedown = function(e){}            //鼠标在元素上按下时触发
el.onmousemove = function(e){}            //鼠标在元素上移动时触发
el.onmouseup = function(e){}              //鼠标在元素上松开时触发
el.onmouseover = function(e){}            //鼠标指针移出某个元素到另一个元素上时发生
el.mouseout = function(e){}               //鼠标指针位于某个元素上且将要移出元素的边界时发
el.onmouseleave = function(e){}           //鼠标指针位移出元素时发生
doc.onmousewheel = function (event) {
    event = event || window.event;
    console.dir(event);
};
// 全局监听鼠标右键
document.oncontextmenu = function(e){
    //preventDefault会阻止浏览器弹出默认菜单
    e.preventDefault();
    // 或者使用
    e.returnValue = false;
};
<!--oncontextmenu：在元素上绑定右键事件-->
<div oncontextmenu="alert('aa')"></div>
// 或者获取
document.getElementById("test").onmousedown = function(e){
    if(e.button ==2){
       alert("你点了右键");
    }else if(e.button ==0){
       alert("你点了左键");
    }else if(e.button ==1){
       alert("你点了滚轮");
    }
}
```

**鼠标事件获取位置**：

```js
el.addEventListener("click", function (e) {
  e.clientX;
  e.clientY; //以浏览器窗口左上角为原点计算
  e.offsetX;
  e.offsetY; //以当前事件元素左上角为原点计算
  e.pageX;
  e.pageY; //以document对象左上角为原点计算
  e.screenX;
  e.screenY; //以计算机屏幕左上角为原点计算
  e.layerX;
  e.layerY; //以最近的绝对定位元素左上角计算
});
```

**事件委托/代理**：利用事件冒泡，我们想让用户点击一个块的每个子元素都触发一个事件，可以将该事件绑定再这些子元素的父元素上就可以不用每个子元素都去绑定了。
**获取鼠标事件目标的属性**：

```js
//e.target：触发事件元素的父级元素。
event.target.nodeName//获取事件触发的标签名
event.target.className//获取事件触发的元素的类名
event.target.id//获取事件所触发的元素的id名
event.target.innerHTML//获取事件触发的元内容
//指的是真正触发事件的那个元素;（不过它是个实时值）异步使用或输出都会为“null”
e.currentTarget;
document.getElementById("a").addEventListener('click',function(e){
    e.currentTarget.style.color = "red"; // 生效
    console.info(e.currentTarget); // null
    setTimeout(()=>{e.currentTarget.style.color = "red";// 报错},0);
})
```

**移动端手指事件**:
需要使用事件绑定函数：addEventListener()或 on()；
touchstart:手指触摸屏幕;addEventListener('touchstart',function(){})
touchmove:手指在屏幕上移动
touchend:手指离开屏幕

```js
event.touches[0].pageX, event.touches[0].pageY; //手指坐标，touchend事件中不能用
event.changedTouches[0].pageX, event.changedTouches[0].pageY; //都可用支持多指触摸事件？？？
```

**自定义事件**：

```js
// 一个元素设置监听事件名可随意。
document.body.addEventListener("文章勿盗", (event) => {
  console.dir(event.detail);
});
// 为该自定义事件设置，要传参必须制定使用detail。
var k = new CustomEvent("文章勿盗", {
  detail: 55,
});
// 触发该事件。
document.body.dispatchEvent(k);
```

事假兼容写入如下：

```js
(function () {
  if (typeof window.CustomEvent === "function") {
    // 如果不是IE
    return false;
  }

  var CustomEvent = function (event, params) {
    params = params || {
      bubbles: false,
      cancelable: false,
      detail: undefined,
    };
    var evt = document.createEvent("CustomEvent");
    evt.initCustomEvent(
      event,
      params.bubbles,
      params.cancelable,
      params.detail
    );
    return evt;
  };

  CustomEvent.prototype = window.Event.prototype;

  window.CustomEvent = CustomEvent;
})();
```

**onselectStart 事件**：`<p onselectStart="return false">积分抵啊放假</p>`
**监听浏览器刷新&退出**：

```js
window.onbeforeunload = onclose; //刷新和关闭操作都会触发onbeforeunload事件。
function onclose() {
  // 该判断，关闭时才触发。
  if (
    (event.clientX > document.body.clientWidth && event.clientY < 0) ||
    event.altKey
  ) {
    return "您要离开吗？";
  }
}
/*===========
浏览器获得焦点与，失去焦点事件
============*/
window.addEventListener("focus", function () {
  document.title = "获得焦点";
}); // 刚打开页面不会触发。
window.addEventListener("blur", function () {
  document.title = "去哪了，快回来！";
}); // 切到其它网站页面时触发。
```

**判断三方资源加载**:
凡带加载性质的元素均有 onreadyStateChange 事件，不过不同浏览器的支持不同，一些浏览器可能会失效。
img.onload 事件(最好用的判断加载的方法)：

```html
<img id="img" src="img/a.jpg" />
<h2 id="h2"></h2>
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

### [2]打印功能：

```js
// 打印print_content元素内容
function printExample() {
  let nt = document.getElementById("print_content");
  // 克隆该节点
  let clone = nt.cloneNode(true);
  clone.style.width = "1000px";

  const newWin = window.open(""); // 新打开一个空窗口

  var styleTag = document.createElement("style");
  styleTag.innerHTML = `div{box-sizing:border-box;}.table{width:100%;}.table td{padding:5px;}.right{
    text-align:right;}.right-border{border-right:1px solid black;}.product{border:2px solid black;
  border-top:none;}.row div{padding:8px 5px;}`;
  newWin.document.title = "报关单打印";

  newWin.document.head.appendChild(styleTag);
  newWin.document.body.appendChild(clone);

  newWin.document.close(); //关闭文档输入流（window.close()和document.close()的区别）
  newWin.focus();
  setTimeout(() => {
    //定时器等待，JS单线程，异步执行此行代码
    newWin.print();
    newWin.close(); //打印完成或取消，关闭新窗口
  }, 300);
}
```

- [参考学习地址](https://www.cnblogs.com/weiyu11/p/7574726.html)

### [3]运行环境检测

```js
var browser = {
  versions: (function () {
    var u = navigator.userAgent,
      app = navigator.appVersion;
    return {
      //移动终端浏览器版本信息
      trident: u.indexOf("Trident") > -1, //IE内核
      presto: u.indexOf("Presto") > -1, //opera内核
      webKit: u.indexOf("AppleWebKit") > -1, //苹果、谷歌内核
      gecko: u.indexOf("Gecko") > -1 && u.indexOf("KHTML") === -1, //火狐内核
      mobile: !!u.match(/AppleWebKit.*Mobile.*/), //是否为移动终端
      ios: !!u.match(/\(i[^;]+;( U;)? CPU.+Mac OS X/), //ios终端
      android: u.indexOf("Android") > -1 || u.indexOf("Linux") > -1, //android终端或uc浏览器
      iPhone: u.indexOf("iPhone") > -1, //是否为iPhone或者QQHD浏览器
      iPad: u.indexOf("iPad") > -1, //是否iPad
      webApp: u.indexOf("Safari") === -1, //是否web应该程序，没有头部与底部
    };
  })(),
  language: (navigator.browserLanguage || navigator.language).toLowerCase(),
};
console.info(browser);

if (browser.versions.mobile) {
  //判断是否是移动设备打开。browser代码在下面
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

### 路由控制

**hash 模式**：hash 模式 url 中会带有#号，不会导致刷新，不过依然可以添加浏览器历史记录

```js
window.onhashchange = function (event) {
  console.log(event.oldURL, event.newURL);
  // location.hash可读可写
  location.hash = "#freedom";
  let hash = location.hash.slice(1);
  document.body.style.color = hash;
};
```

**history 使用**：

```js
// 页面回退
history.back();
// 页面前进或后退
history.go(2);
// 添加1个history记录
/*
@data: 可传的数据，map型；
@title: 页面标题；
@url: 页面地址
*/
history.pushState(data, title, url);
// 替换掉当前页
history.replaceState(data, title, url);
```

**跳转监听**：

```js
// 拦截history模式的回退
// 添加popstate事件监听变化
window.addEventListener("popstate", function () {
  // 发生了跳转
  history.pushState(null, null, document.URL); // 用pushState阻止回退
});
// 拦截hash模式的回退
function c() {
  var url = window.location.href;
} //获取到的是变化后的地址。用正则表达式来监听是否是回退到了上一个页面。
window.onhashchange = c; //onhashchange可以今天hash模式的变化，触发函数c。
```

### 拖拽文件

```html
<p id="box" class="box" style="width:100px;height:100px;"></p>
<script>
  box.addEventListener("dragover", function (event) {
    event.preventDefault();
    // 检测是否需要新窗口打开链接
    if (event.dataTransfer.dropEffect != "link") {
      isOpenLink = true;
    }
    event.dataTransfer.dropEffect = "link";
  });

  box.addEventListener("drop", function (event) {
    event.preventDefault();
    // 遍历文件信息
    var files = event.dataTransfer.files || [];
    // files是一个File对象列表。
    var length = files.length;
    if (length == 0) {
      this.innerHTML = "<p>没有文件</p>";
      return;
    }
    var html = "";
    for (var index = 0; index <script length; index++) {
      html += "<p>类型：" + files[index].type + "</p>";
    }
    this.innerHTML = html;
  });
</script>
```

## 7、DOM：

:::alert-primary
js 执行 dom 操作后，其任务会被放到**ui 任务队列**，按顺序交给**ui 线程**执行；不过，其余**同步 js 执行完毕后**才会将任务加入到队列。
js 由 javascipt 引擎执行，dom 渲染时由单独的 webCore 来实现，渲染和 js 的执行（dom 操作结束后的代码）是**异步**的！
js 的执行和 dom 的渲染是两个引擎执行的，所以每次交互时，其之间的触发就会较慢。
:::

### [1]DOM 操作：
1
1. **获取元素尺寸相关**

```js
el.offsetHeight; // 包括边框+内边距+内容尺寸
el.offsetTop; // 距父元素左边距含margin值
el.clientHeight; // 内边距+内容尺寸
el.clientTop; // 到上边框距离
el.scrollTop; // 元素当前内部滚动的距离
el.scrollHeight; // 元素内部可滚动的距离，一般比clientHeight大。
ele.style.left = ""; // 来重新写入该元素的位置，否则返回的永远都只是该元素的初始位置
ele.getBoundingRect().left; // 使用可实时获取元素位置。
```

2. **元素节点操作**

```js
p = document.createElement("p"); //创建一个节点
document.createTextNode("text"); //创建文本节点
el.appendChild(p); //添加孩子节点：末尾添加
p.setAttribute("style", "width:10px;height:20px"); //在添加完节点后可以用方法来动态改变该元素属性，直接用style则无效。</i>
fa.insertBefore(el, fa.lastChild); //插入节点：fa中插入节点el,在最后一个节点前插入。
el.parentNode; //父节点,选中el的父节点。
el.previousSibling; //选取上一个节点
el.nextSibling; //选取下一个节点
a.contains(b) / a.compareDocumentPosition(b); //判断一个元素是否包含另一个元素
el.removeChild(ak); // 删除元素节点//只能用父元素删除子元素的方式
el.cloneNode(true); // 复制元素,true是会连其子元素一齐复制
el.childNodes; // 返回元素的所有子元素(两种不同情况返回的长度)、
el.childNodes[0].nodeName; //节点名,为间隙或文字则为#text为元素则为。大写的标签名,nodeValue;//节点中的文本内容(非html结构)
```

```html
<p><b>1</b><b>2</b><b>3</b></p>
//p.childNodes.length>>3
<p>
  <b>1</b>
  <b>2</b>
</p>
//p.childNodes.length>>4
```

3. **获取属性**：`ele.style.property`和`window.getComputedStyle('元素','伪类').getPropertyValue('属性')`//这两个方法都是只读属性。
4. **写入样式**：

- `ele.style["color"] = "red";`可以使用这两种方法来改变其元素的 css 样式(但是会显示在内嵌样式中)：
- `ele.style.cssText=”width:150px;height:200px;”`;//内嵌样式全部重写。
- `ele.style.setProperty(‘样式名’,’样式值’);`//更新的方式写入，不会去除不相关样式。
- **为元素添加类名或 id 名**：setATTribute(“class”,“new”)，element.className=””;setATTribute(“id”,”id”),element.id=””;
- 使用 removeATTribute(“class”.”id”)（也可用来移除 id 名）或.classList.remove(“id”)来移除元素类名。

5. **获取伪类元素**：

```js
var myIdElement = document.getElementById("myId");
// 添加多个类名时使用
myIdElement.classList.add("name");
var beforeStyle = window.getComputedStyle(myIdElement, ":before");
```
6. 动态添加style标签

```js
var style = document.createElement("style");
style.type = "text/css";

try{
　　style.appendChild(document.createTextNode("body{background-color:red}"));

}catch(ex){
　　style.styleSheet.cssText = "body{background-color:red}";//针对IE
}
var head = document.getElementsByTagName("head")[0];
head.appendChild(style);
```
### [2]性能探究：

- 尽量避免 DOM 修改次数；
- innerHtml 稍慢于 createElement()；
- createElement()稍慢于克隆节点；
- 将元素集合放到数组中，然后操作，比直接操作这个元素集合更快；
- 使用 offsetLeft、scrollWidth、clientTop 等属性时会导致，“刷新渲染队列”（避免在布局改变时使用它们）
- 利用`el.style.cssText="width:90px;top:15px;";`来一次写入全部属性，**这样就只会出现一次重排**；
- 或者使用`el.className="new";`的方式来修改；
- 脱离文档流减少重排：同一元素内多个 dom 操作时，为只使用一次重排来达到效果，**可使其先脱离文档流**，在上面操作完成后再恢复其文档流。

```js
/*================
    隐藏-脱离文档流-恢复
==================*/
var ul = document.getElementById("ul");
ul.style.display = "none";
ulAppend(ul); // 对ul一系列dom操作
ul.style.display = "block";
/*================
    文档片段方式-脱离文档流
==================*/
var fragment = document.createElementFragment();
ulAppend(fragment); // 对文档片段一系列dom操作
ul.appendChild(fragment);
/*================
    克隆替换方式
==================*/
var cn = ul.cloneNode(true);
ulAppend(cn); // 对文cn一系列dom操作
ul.parentNode.replaceChild(cn, ul); //替换
```

- 同个操作中，js 执行完前，其创建的 ui 任务都不会加入到任务队列，<b c=b>使用微任务或宏任务放置这些 ui 操作</b>，特别是较多 js 代码时。

```js
function click() {
  // 定时器，或放到promise。
  setTimeout(() => {
    // dom操作代码
  }, 250);
  // ...一堆op
}
```

## 8、音视频：

**调用摄像头**：[参考学习地址](https://developer.mozilla.org/zh-CN/docs/Web/API/MediaDevices/getUserMedia)

- [video 所有属性及 js 方法](https://www.cnblogs.com/TF12138/p/4448108.html)

```html
<video
  id="vd"
  poster=""
  loop
  autoplay
  controls
  width="200"
  height="300"
></video>
<!--
poster：视频封面，没有播放时显示的图片
preload：预加载
autoplay：自动播放
loop：循环播放
controls：浏览器自带的控制条
-->
<video id="video">调用摄像头</video>
<canvas id="canvas"></canvas>
<button onclick="get()">打开摄像头</button>
<button onclick="show()">拍照</button>
<button onclick="deviceClose()">关闭所有设备</button>
<script>
  var width = window.innerWidth;
  var height = window.innerHeight;
  var video = document.getElementById("video");
  var stream = null;
  /*==============
    video常用方法
  ===============
*/
  video.currentTime = 1; //设置开始播放位置
  video.controls = "controls"; // 显示控制条。
  video.play();
  video.pause(); // 播放，暂停。
  video.load(); //重新加载src指定的资源
  video.volume = value; //音量
  video.muted = value; //静音

  // 点击调用摄像头
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
    /*    
        ==============================
                兼容性处理
        ==============================
        注意：这些情况才能调用：地址为localhost:// 访问时、地址为https:// 时、为文件访问file:///
        http访问时，navigator.mediaDevices为undefined。
    */
    let photo =
      navigator.mediaDevices.getUserMedia(obj) ||
      navigator.webkitGetUserMedia(obj) ||
      navigator.mozGetUserMedia(obj) ||
      navigator.msGetUserMedia(obj);
    // 会先获取权限(用户控制)，调用成功的话则运行then()方法
    photo.then(function (MediaStream) {
      // srcObject属性，兼容性处理。
      stream = MediaStream;
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
    devices.map((v) => {
      v.stop();
    });
  }
</script>
```

**webrtc**：运输层使用的 UDP 传输。web 端视频电话支持技术，里面处理了媒体流数据编码、杂音、画面去噪等功能。

- <b c=r>web 端直播推流使用此方法（这里只有大致的思路）</b>
- [参考学习地址](https://www.dazhuanlan.com/2019/12/24/5e0191c6d8816/)，[腾讯的一套 webrtc 直播 sdk](https://github.com/tencentyun/tweblive)
- **HLS**：的工作原理是把整个流分成一个个小的基于 HTTP 的文件来下载，每次只下载一些。当媒体流正在播放时，客户端可以选择从许多不同的备用源中以不同的速率下载同样的资源，允许流媒体会话适应不同的数据速率。[hts 与 m3u8](https://www.jianshu.com/p/e97f6555a070)
- **m3u8**：该文件实质是一个播放列表（playlist），其可能是一个媒体播放列表（Media Playlist），或者是一个主列表（Master Playlist）。但无论是哪种播放列表，其内部文字使用的都是 utf-8 编码。

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

**flv.js**：解析 flv 文件的拉流实现。flv.js 这个项目解决了 HTML5 支持 flash 协议的问题，这就是 flv.js 应运而生短期爆红的历史背景。flv.js 中的 demux 就是一套 FLV 媒体数据格式的解析器，

> [原理讲解地址](https://www.cnblogs.com/saysmy/p/10209581.html)

**rtmp 推拉流**：

- 推流协议使用 rtmp，之前的借助 flash 插件实现 rtmp 推流，但 flash 插件各浏览器几乎已不支持。
- 这个协议建立在 TCP 协议或者轮询 HTTP 协议之上。所以理论上可以用 js 实现 rtmp 协议，似乎也有人这么做，但没找到相关的解析 rtmp 协议的 js 库。
- [git 地址](https://github.com/chxj1992/rtmp-streamer)
- [流媒体服务框架](https://github.com/ZLMediaKit/ZLMediaKit)、[EasyMedia 浏览器 rtmp 播放](https://gitee.com/52jian/EasyMedia#https://download.csdn.net/download/Janix520/15785632)

## 10、文件&图片：

input 中的 file 属性提供了一个从本地图库选择图片文件的功能,以下代码将选中的图
片显示在页面上：

```html
<img id="img" />
<input type="file" onchange="get(this)" multiple="multiple" />
<!--multiple允许一次选择多张图片-->
<canvas id="can" width="500" height="300"></canvas>
<form id="form"></form>
```

### a、选择图片并压缩

```js
function get(self) {
  // self是input元素
  var img = document.getElementById("img");
  var ctx = document.getElementById("can").getContext("2d");
  var cImg, w, h;
  //self.files.length;获取图片张数
  var fil = self.files[0];
  var read = new FileReader();
  read.readAsDataURL(fil);
  read.onload = function () {
    img.src = read.result;
    cImg = new Image();
    cImg.src = read.result;
    // 可直接将read.result直接传给后台
    cImg.onload = function () {
      // 获取原始图片大小
      w = cImg.width;
      h = cImg.height;
      //可以根据w,h的比列缩小画在canvas上再获取相应区域的像素数据传送
      ctx.drawImage(cImg, 0, 0); //不填入宽高值时是原始打下显示。
    };
  };
}
```

### b、选择视频并显示

```html
<script>
  function get(self) {
    // self是input元素
    var img = document.getElementById("img");
    var vd = document.getElementById("video");

    var cImg, w, h;
    //self.files.length;获取图片张数
    var fil = self.files[0];
    var read = new FileReader();

    read.readAsDataURL(fil);
    read.onload = function () {
      //vd.src = fil;
      vd.src = window.URL.createObjectURL(fil);
      vd.load();
      vd.onloadedmetadata = function (e) {
        // 设置当前播放位置，
        vd.currentTime = 1;
        vd.controls = "controls";
        vd.play(); // 不设置播放的话，显示有问题。离开页面后视频显示也会出现同样的问题。
      };
    };
  }
</script>
```

### c、获取图片 base64 法 1

使用 canvas 绘制图片，再使用 toDataURL 或 getImgData 方法获取 base64 数据即可；但多有跨域问题。

### d、获取图片 base64 法 2

```js
var xhr = new XMLHttpRequest();
xhr.open("get", "http://localhost:80/download/xiuxin.png");
// 注意返回设置为blob类型
xhr.responseType = "blob";
xhr.withCredentials = true;
xhr.onreadystatechange = function () {
  if (xhr.readyState == 4 && xhr.status == 200) {
    var blob = xhr.response;
    read2base64(blob);
  }
};
xhr.send();
// 使用FileReader将blob转base64
function read2base64(blob) {
  var reader = new FileReader();
  reader.readAsDataURL(blob);
  reader.onload = function (eve) {
    var txt = event.target.result;
    console.log(txt);
  };
}
```

### e、base64 转 file

```js
function base642file(base64, filename) {
  var arr = base64.split(",");
  var mime = arr[0].match(/:(.*?);/)[1];
  var bstr = atob(arr[1]),
    n = bstr.length,
    u8arr = new Uint8Array(n);
  while (n--) {
    u8arr[n] = bstr.charCodeAt(n);
  }
  return new File([u8arr], filename, { type: mime });
}
```

### f、base64 转 blob

```js
function base642blob(base64Data) {
  var byteString;
  var segments = base64Data.split(",");
  if (segments[0].indexOf("base64") >= 0) {
    byteString = atob(segments[1]);
  } else {
    byteString = unescape(segments[1]);
  }
  var mimeString = segments[0].split(":")[1].split(";")[0];
  var ia = new Uint8Array(byteString.length);
  for (var i = 0; i < byteString.length; i++) {
    ia[i] = byteString.charCodeAt(i);
  }
  var blob = new Blob([ia], { type: mimeString });
  return blob;
}
```

### h、文件转 base64

```js
function file2base64() {
  // 该函数绑定文件选择点击事件
  var file = this.files[0];
  var reader = new FileReader();
  reader.readAsDataURL(file);
  reader.onload = function (e) {
    var txt = e.target.result;
    console.log(txt);
  };
}
```

## 15、兼容性问题：

事件的兼容性处理：

```js
el.onclick = function (event) {
  //ie中可直接用window.event/event读取事件，firfox中通过传参传入事件
  var eve = event || window.event;
};
```

**元素选择**：
document.idName/document.getElementById("");//IE
document.getElementById();//其它,统一使用此法
el.parentElement/el.parentNode;//IE,统一使用 parentNode

**元素中写入内容**：
el.innerText = "";//多数支持
el.textContent="";//低版本的 firefox 使用，建议全部用 innerHTML 代替。
ajax 兼容问题：

```js
if (window.XMLHttpRequest) {
  var xml = new XMLHttpRequest(); //IE7以上支持
} else {
  var xml = new ActiveXObject("Microsoft.XMLHTTP");
}
contains与compareDocumentPosition;
ela.contains(elb); //elb是否在ela中，是则返回true,IE
ela.compareDocumentPosition(elb); //是则返回20，否为10,低版本的firefox
```

https://www.jb51.net/article/81704.htm
https://www.jb51.net/article/84596.htm

## 16、网络相关：

### 1、ajax:

- **原生 ajax 的写法**：

```js
var xhr = new XMLHttpRequest();
//username和password为url所需要的授权提供认证资格一般不填
xhr.open('post','url',true，username,password);
/********设置回应类型，blob时对应用xhr.response获取**********/
xhr.responseType = 'blob';
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

```

- **两种数据类型**：向服务端发送的数据有 Form Data 和 Request Payload 两种，这两种数据类型可以由请求头的 Content-Type 控制。
  > Form Data 类型：`Content-Type:"application/x-www-form-urlencoded"`#默认使用的类型，使用 POST，但数据不是 json 格式而是：`rpc.post(url,"key=234&v=9fdf0")`#的类型，在浏览器/netWork/Headers/最下方可以看到。
  > Request Payload：`Content-Type:"application/json"`#现在几乎使用这种数据类型，发送一个字典的话会默认将每个键值队拼在 url 后请求。使用 JSON.stringify()将数据转为 json 在发送是常用的形式。
  > Raw：将 json 格式数据用字符串表示，如：`'{"name":"www","age":"15"}'`#注意，里面的引号是需要的。

### 2、ajax 上传文件

使用 jquery 封装的 ajax 和 axios 的 ajax 先用 formdata 封装文件再上传时发现浏览器的 xhr/head 项中没有显示 FormData 项数据，在请求头中修改 Content-Type:'multipart/form-data'后发现 head 项出现 FormData 数据了，但是有报跨域问题，这可能跟 axios 源码中检测数据类型，做的特别处理有关。

```html
<form id="a"><input type="file" name="file" /></form>
<script>
  var form = document.getElementById("file-form");
  var _form = new FormData(form);
  var xhr = new XMLHttpRequest();
  xhr.open("post", _url, true);
  // 不用设置请求头数据类型，反而直接成功。
  xhr.send(_form);
  xhr.onreadystatechange = () => {
    if (xhr.readyState == 4 && xhr.status == 200) {
      var res = xhr.responseText;
      res = eval("(" + res + ")");
      console.log(res);
    }
  };
</script>
```

- **404 问题**：404 不完全是接口路径的原因，如果后台有请求日志情况的 404，可能是传输的数据类型与后台接收类型不一致。<b c=r>若后台没有请求日志，则是前端路径、接口、代理等问题。</b>
- **ajax 注入分页**：使用 document.write(data)的方法要求分页里只有元素结构（没有 meta,html,body 等在主页中重复的标签）,可是这样仍会把主页<head></head>标签中的外链样式覆盖为无,我们可以再写一个分页专门用于装效 head 标签及其里面的外联样式（link,script 等）;可是外联的 js 语句只执行一次就 无效了!!（弃）;若注入分页的 js
  代码用引入的方式则`<script async='async' src=''></script>`或在注入的 ajax 代码中将 async 改为 false 或 ajax 代码后加一个延时器延时绑定事件。(一些坑爹的后台框架会劫持所有 ajax 请求导致报错所以使用需谨慎,本地打开带有使用 ajax 的文件会产生跨域问题);
  **ajax 中地址为空情况**：ajax 中如果 url 地址为空在提交时会变成提交到当前页 url 路径。jquery 的 ajax 中不填写 dataType 值时 jquery 会自动判断返回值的类型(所填写的 data 中的格式不能是 json 格式)。
  <i class="label2">ajax 中添加加载动画</i>使用 jquery 的 Ajax 是在 beforeSend:function(){}中添加动画，在 complete:function(){}中取消加载动画。在原生 js 的 ajax 中也可以自行在 onreadystatechange = function(){}前后添加两个函数也可实现。但 beforeSend 函数只在第一次请求时触发,所以显示加载动画最好是在调用 ajax 之前,complete 中隐藏加载动画可以加一个延时取消这样交互效果更好。
  <i class="label1">ajax 接口的处理</i>做项目中在使用到 ajax 或其它方式对接数据时对接的接口需要用"http://"+获取的本地域名+接口来充当请求数据的接口，这样更换域名后也不会出错。(也可直接写域名后的接口名，在运行时会被自动添加上当前域名)。
- GET 与 POST 的区别：规范中 GET 是将参数放在 url 中，POST 是将数据放在请求体中，当然也可以反过来。
- **跨域问题**：解决方法如下
  > jsonp：使用`<script src="http://a.com?id=15">`标签能跨域的特性，发起 get 请求让后台返回想要的数据，甚至在里面写上触发前端函数的方法。
  > cros：后台直接配置 cros 即可。**浏览器将 CORS 请求分成两类**：简单请求（simple request，请求方式受限，字段受限）和非简单请求（not-so-simple request）。
  > webscoket 和 workers 的 postMessage 可以跨域。

不借助input的文件选择：
```js
// 打开文件
window.showOpenFilePicker();
// 打开文件夹
window.showDirectoryPicker();
```
### 3、文件下载：

```js
export function download(url, params, filename) {
  //"Content-Type": "application/x-www-form-urlencoded",
  return request
    .post(url, params, {
      headers: {
        "Content-Type": "application/json",
        "Accept-Encoding": "gzip,deflate,br",
        Accept: "*/*",
      },
      responseType: "blob",
    })
    .then((data) => {
      const content = data;
      // 将文件转为数据对象。
      const blob = new Blob([content]);
      if ("download" in document.createElement("a")) {
        // 创建a标签，主动触发其点击，然后下载（当前页面下载），用户点击的a标签下载似乎会打开新页面。
        const elink = document.createElement("a");
        elink.download = filename;
        elink.style.display = "none";
        elink.href = URL.createObjectURL(blob);
        document.body.appendChild(elink);
        elink.click();

        URL.revokeObjectURL(elink.href);
        document.body.removeChild(elink);
      } else {
        navigator.msSaveBlob(blob, filename);
      }
    })
    .catch((r) => {
      console.error("er--", r);
    });
}

import axios from "axios";
/**
 * @desc blob文件下载
 * @version version=1.0.0
 * @author yd_yuliping
 * @param {object} config 请求配置信息
 * @param {string} fileName 下载文件名
 */

export function downloadFileByBlob(config, fileName) {
  return new Promise((resolve, reject) => {
    axios({
      ...config,
      responseType: "blob",
    }).then((res) => {
      let reader = new FileReader();
      reader.readAsText(res.data);
      reader.onload = function () {
        try {
          const result = JSON.parse(reader.result);
          reject(result);
        } catch {
          const blob = new Blob([res.data], {
            type: "application/octet-stream",
          });
          if ("msSaveOrOpenBlob" in navigator) {
            window.navigator.msSaveOrOpenBlob(blob, fileName);
            return;
          }
          const href = window.URL.createObjectURL(blob);
          downloadFile(href, fileName);
          resolve(res);
        }
      };
    });
  });
}
```

[Blob 的使用](https://www.cnblogs.com/cheng825/p/11694348.html)

## 23、es6 语法：

因为是在 2015 发布的，所以又用 ES2015+来代替。

```js
let a = 10;//###块级作用域let定义变量,只在定义的块或附近的块有用，如for循环中
let a = () => 1;
alert(a);// 报错 a已被清除。
const a = 20;//const定义常量，第一次赋值后不能被改变。但如果是用来定义一个对象的话是可以改变其值的。
/*###箭头函数，this*/
let foo = () => 1;//建立一个名为foo的函数返回值1，传参数时就等号后就写括号，
// var f = (1,2) =>{};多个参数时的写法，单个参数可不写括号，箭头指向执行语句
()=>{};// 将无名函数作为一个参数时的写法
v => {this.a = 20};// 将一个有名函数作为参数传入时的写法。箭头函数中的this
//不是指向他的上一级而是指向它本身
/**************类**************/
class animal{// 父类
    // static修饰的变量或方法不能被继承，但可用父类直接调用(animal.AS)
    static AS = '55';
    construct(dat){this.x=20;}
    run(){alert('here run');}
    //不能直接animal.run()调取父类中的方法。
}
// 子类,extends继承父类; 无法继承 父类中使用this添加的变量
class dog extends animal{
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
//###模块的使用
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

/*==============
     promise
================*/
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
/*=================
    async与await的使用，await一定要放在async内部，相当于是promise的两种使用方式。
===================*/

async function funAsy() {
     const a = 1;
     // 使用await可以直接拿到resolve()或reject()的结果赋值给b，否则b就只能是一个promise对象。
     const b = await new Promise((resolve, reject) => {
           setTimeout(function() {
               resolve('time');//如果resolve()在定时器外使用的话，会先与定时器执行。
           }, 3000)
     })
     // 直接输出b的话得到：time
     console.log(b,a);//定时器中的resolve()运行后才会执行这里。
     return b;
}
// 而将b返回使用的话则是一个promise对象。
funAsy().then(res => {console.log(res)});//3s后才会输出。
//！！！    async无法配合使用回调的函数使用，如下：
function a(arr){await c = new Promise...}
async a.call([1,2,3]); //不会报错，但并不会变成同步。所以forEach,map()方法中使用也是无效的。

//---等待所有结果返回：
new Promise.all([pr1,pr2]).then().catch();//任何一个出行catch时触发catch

//-----------------代理proxgy。与就的object方法集一样的作用，都用于监听对象的变化。
//还有其它方法，能监听到一些Object.defineProperty监听不到的东西。
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
/*===================
       迭代器与生成器
=====================*/
var a = {
  x: 10,
  y: 20,
};
var iter = Iterator(a);//迭代器
console.log(iter.next()); //使用next()获取下一个值，
function* f() {
 for (let i=0; i<5; i++){
  yield i // 返回并记录函数状态
 }
}
var f = f();//使用yield提供的一个生成器。f.next()调用。
/*=================
    模块化
===================*/
//js文件中用export分别导出，可以是任意数据类型。
export const av = {
    a: 1,
    b: 2
};
export const ab = function() {
    return 'hello';
};
import {av} from 'utils/tool.js';//这样另一个文件中import时就能使用解构的写法。
//都放在default导出的话，另一边import是无法用解构的。
export default {
    av:{},
    ab:function(){}
}
// *****未使用export的文件，也可以使用import导入***********
import * as allModule from "./jquery.js";
const moules = allModule.default; //从defalut中获取使用
```

## 27、原型：

- **js 中无类的概念**：类意味着复制，传统的类被实例化时，它的行为会被复制到实例中。类被继承时，行为也会被复制到子类中。而 js 并不会像类那样自动创建对象的副本。
- **封装**：将一些 js 语句写到一个方法里面，只留下一些特定的借口供外部访问。
- **继承**：每个函数中都有一个 prototype 属性，而这个 prototype 属性被称为函数 的原型，原型中的所有方法都是可以被外部继承的，而函数方法内（原型外 部）的对象是该函数的私有对象，不能被继承。继承的方法可以使用 new 关 键字继承，继承的那个变量就变成了一个对象（是对象而不是函数），继承 之后我们可以使用 el[‘name’]=’pro’的方法向其中添加新的属性名属 性值，在原型方法中也可以继承自己的父函数中的原型，这样就可以实现重 复循环的自调用了；也 可以使用 call(),applay()方法来继承。
- **多态**：传入不同的参数或者配合不同的函数使用可以得到不同的结果。

- 网页端 js 开发在相当一段时间 bai，由于浏览器的 js 解释引擎性能并不高，而且网络带宽也比较小，因此绝大多数站点的代码规模并不大，主要针对页面一些简单交互逻辑，在此前提下，浏览器厂商以及工业界都没有强大的动力去实现面向对象版本的 js。<b c=gy>考虑到到网页环境的特殊性，使用原型继承而不是类继承的方式，更节约内存空间，而且解释器的实现更为简单。</b>
- **工厂模式**：没有解决对象识别的问题（即怎样知道一个对象的类型）。

```js
function createPerson(name, age, job) {
  var o = new Object();
  o.name = name;
  o.age = age;
  o.job = job;
  o.sayName = function () {
    alert(this.name);
  };
  return o;
}
var person1 = createPerson("Nicholas", 29, "Software Engineer");
var person2 = createPerson("Greg", 27, "Doctor");
```

- **构造函数方式**：没有显式地创建对象、直接将属性和方法赋给了 this 对象、没有 return 语句。使用 new 继承后会有一个 construct 属性指向，以此知道他们的类型。
  构造函数的主要问题：就是每个方法都要在每个实例上重新创建一遍。

```js
//如果不用new来继承函数的原型而是直接运行函数，那么构造函数中用this添加的变量就会添加到window对象下成全局变量，解决如下：
function person(name, age) {
  if (this instanceof person) {
    // 使用this添加的属性在new之后是直接在实例中，而不在__proto__中。
    this.name = name;
    this.age = age;
  } else {
    return new person(name, age);
  }
}
```

- **原型模式**：使用原型对象的好处是可以让所有对象实例共享它所包含的属性和方法。换句话说，不必在构造函数中定义对象实例的信息，而是可以将这些信息直接添加到原型对象中。在默认情况下，所有原型对象都会自动获得一个 constructor（构造函数）属性，这个属性包含一个指向 prototype 属性所在函数的指针。
  <b c=r>创建了自定义的构造函数之后，其原型对象默认只会取得 constructor 属性</b>；
  <b c=gn>至于其他方法，则都是从 Object 继承而来的</b>。
  <b c=r>Object 的原型指向是 null，不过对于访问不到的属性返回则是 undefined。</b>

```js
function Person() {}

Person.prototype.name = "Nicholas";
Person.prototype.age = 29;
Person.prototype.job = "Software Engineer";
Person.prototype.sayName = function () {
  alert(this.name);
};
var person1 = new Person();
person1.sayName(); //"Nicholas"
alert(Object.getPrototypeOf(person1) == Person.prototype); //true
alert(Object.getPrototypeOf(person1).name); //"Nicholas",但不能通过此方法来更改。

//-----直接在原型中写属性相当于重新构造了原型，所以construct会指向Object。
function Person() {}
Person.prototype = {
  //让其constructor重指向Person。不过会让该属性变为可枚举。
  constructor: Person,
  name: "Nicholas",
  age: 29,
  job: "Software Engineer",
  sayName: function () {
    alert(this.name);
  },
};
//也可以在js自带的String、Array等方法的原型上添加属性。
```

- **原型链**：Array、Object、函数都会有一个**proto**属性，这个属性是该子类继承父类之后，显示的继承的对象内容（比如[1,2,3].**proto**就是 Object），当使用该对象的某个属性时，若没有就会在它的**ptoto**属性查找，再从 Object 中查找。
- **new 的实现原理**：将一个空对象（{}）的**proto**指向对应函数的原型的，然后**ptoto**.constructor 指向该构造函数。示例如下：

```js
//原型的弊端：原型是共享的，如果属性是数组这种引用型数据时，在new之后的实例上去改变它，那么直接会改变原型的值。
function Parent(age, name) {
  this.age = age;
  this.name = name;
  this.sayAge = function () {
    console.log("this.age :", this.age);
  };
}
Parent.prototype.sayName = function () {
  console.log("this.name :", this.name);
};

function New(Fn) {
  let obj = {};
  //选择后两个参数。
  let arg = Array.prototype.slice.call(arguments, 1);

  obj.__proto__ = Fn.prototype;
  obj.__proto__.constructor = Fn;
  Fn.apply(obj, arg);
  return obj;
}
let newSon = New(Parent, 18, "lining");
console.warn(">>", newSon.name);
```

- 构造函数模式与原型模式组合：原型中写可以共用的方法和变量，构造函数中写经常会涉及改动的、各场景使用值不同的情况。还能让函数接收传参，及决定是否在原型上添加某个方法（这叫动态原型）。
- **稳妥创建**：构造函数内部不使用 this，继承不使用 new。在要求环境安全时可以这么写。

```js
function Person(name, age, job) {
  //创建要返回的对象
  var o = new Object();
  o.name = name;
  o.age = age;
  o.job = job;
  o.sayName = function () {
    console.info(name);
  };
  return o;
}
const cc = Person("w", 23, "web");
```

- **继承父类私有属性**：

```js
function SuperType() {
  this.colors = ["red", "blue", "green"]; //私有，直接使用new是无法继承的。
}
function SubType() {
  //继承了 SuperType
  SuperType.call(this); //使用call()将父类属性添加进来。
}
var instance1 = new SubType();
instance1.colors.push("black");
alert(instance1.colors); //"red,blue,green,black"
var instance2 = new SubType();
alert(instance2.colors); //"red,blue,green"
```

## 28、函数：

:::alert-info
每个函数会在内存中为其创建一个空间，存储其所用变量（下图所示，顺序和链式存储结合）。**全局变量（window,document）等会被注入到该空间中**。
:::

- map，Array 等较深的结构按链式方法查找，<b c=r>使用的数据结构越深，速度越慢！</b>
- 局部变量存储顺序靠前，其查找使用起来速度最快。
- 全局变量存储到最后，查找使用起来较慢，_因此性能最差，尽量避免使用！_
- 执行完毕后执行环境被销毁。
- 动态作用域：使用了 with、catch(){}子句、eval()函数的可以看做时动态作用域情况
- **性能优化方法**：
  （1）将对应全局变量赋值给一个局部变量，这样在查找时就只是查找该局部变量（按标识符查找的）。
  （2）避免使用 with 语句。<i c=gn>with 创建的作用域会被推到函数作用域首位，局部变量位置反而落于其后</i>
  （3）适当使用`try{}catch(e){}`：执行 catch 时，对象 e 会被推到作用域首位！一般在 catch 中专门将 e 交给一个函数来处理最好。
- **闭包**：一般来讲，当函数执行完毕后，局部活动对象就会被销毁，内存中仅保存全局作用域。
  在另一个函数内部定义的函数会将包含函数（即外部函数）的活动对象添加到它的作用域链中。<i c=gn>也教耗性能</i>

```js
var a = 15;
function cc() {
  console.info("a>>", a);
}
(function () {
  var a = 20;
  cc(); //得到15，cc的创建并不在当前函数中，所以cc的输出还是全局变量a。
})();
// 改变作用域情况
var obj = { a: 1, b: 2 };
with (obj) {
  //为obj创建一个作用域，内部的变量都是从obj中查找。
  a = 1;
  b = 2;
}
```

![](\_v_images/20210303192355713_21879.png =607x)

# B、vuejs：

:::alert-info
**核心实现**：每个组件实例会有一个渲染 watcher，用于收集页面上的绑定的属性。计算属性和监听属性建立后都会各有一个 watcher 用于手机相应的依赖，并同时向 Dep 中发布订阅，添加到 Dep.subs 中，然后各 watcher 收集到的响应式对象会交给 Observe，其使用 Object 方法集为这些响应式对象添加 getter，setter 属性，当发生改动时会触发 setter，然后 setter 内根据其绑定的相关 watcher 通知 Dep，触发 Dep 的 notify()函数，去遍历 Dep.subs 中的订阅者，触发相关 watcher 的 update 方法重新计算、渲染。
:::

![v2-b94d747fd273ec8224e6349f701430fd_720w](\_v_images/20210305103536586_26904.jpg =510x)![vue](\_v_images/20210305201824661_21824.png =790x)

## a1、原理:

**初始化阶段**(这个阶段主要是把普通对象转化为响应式对象)、**编译阶段**(编译阶段会把 options.template 编译成 render 函数，解析 template 中的数据，事件绑定等)、**挂载阶段**(这个阶段会执行 render 函数以获取 vnode。然后模板引擎根据 vnode 去生成真实 DOM)、**监听阶段**(挂载阶段之后，模板引擎已经渲染好网页，这时就进入了监听阶段。patch 函数还会对比新旧 vnode，并计算出更新 DOM 需要的操作。最后由框架更新到网页上)、**注销阶段**(注销过程会先触发 beforeDestroy，然后注销掉 watchers、child components、event listeners 等，之后是 destroyed 钩子函数)。
**vue 生命周期**：生命周期函数运行顺序如下：注意各阶段对应的钩子函数。

- **beforeCreate**：new 一个 vue 实例后，只有一些默认的生命周期钩子和默认事件，其他的东西都还没创建。<i class="gray">data 和 methods 中的数据都还没有初始化。因此不能在此调用 methods 的方法和 data 的数据。</i>
- created：data 和 methods 都已经被初始化好了。
- beforeMount：在内存中已经编译好了模板了，但是还没有挂载到页面中。
- mounted：Vue 实例已经初始化完成了。进入运行阶段，页面渲染完成，可在此进行操作 dom。
- beforeUpdate：页面中的显示的数据还是旧的，data 中的数据是更新后的， 页面还没有和最新的数据保持同步。
- updated：页面显示的数据和 data 中的数据已经保持同步了，都是最新的。
- beforeDestory：进入到了销毁阶段，这个时候上所有的 data 和 methods ， 指令， 过滤器 ……都是处于可用状态。还没有真正被销毁。
- destroyed(组件已经被销毁)。
- **单个组件中为什么 data 是一个函数**：由于组件可以复用，而对象又是引用型的，如果改成 map，会造成互相污染，函数则是返回一个全新的。
- **vue 怎么监听数组的**：通过在 Array 重写数组方法，在其中添加监听，监听到有使用这些方法时则直接出发 Dep 的 notify 来更新。
- **虚拟 DOM**：vue 中的虚拟 DOM 是根据对编译后的模板，生成一个用 js 对象描述节点内容，属性的抽象。
- **nextTick**：vue 用异步队列的方式来控制 DOM 更新和 nextTick 回调先后执行，nexTick 中的操作是放于微任务队列，若浏览器不支持则会使用 setTimeout(fn,0)来处理。
-
- **diff 算法**：用于新老虚拟 DOM 之间找到最小更新部分，然后进行更新。（1）比较新旧节点是否为同一节点（使用 key 或选择器）若不是同一节点则以旧节点为基准插入这个新节点，然后删除旧节点。（2）若是同一节点且文本属性等都相同则不作处理，若只有文本差异则替换文本即可。（3）若新节点有子节点，则清空老节点，将新节点的子节点插入老节点中即可。

**vue-cli**：
:::alert-info
**vue-cli**：是一个构建项目的工具，一个平台，也是一个 npm 包。它提供一套初始的项目模板，内部规定好哪些文件夹的功能。打包时使用的 webpack，webpack 的配置，vue-cli 中也写了一些初始的配置，webpack 做为项目的一个依赖而安装。其它安装的一些依赖都放在 node_modules 下，一些 less-loader,file-loader 的东西是在编译打包时运行的，其配置也作为 webpack 的 plugin。这些工程化项目的过程中 node 只是作为一个让其独立运行的环境，当然这当中也使用 node 一些自带的功能。所以不使用 vue-cli,自己定义一个目录，编写配置也是可以的，也由此有很多 cli 工具。**vue-cli 中使用的服务时 webpack 的服务**。
:::

- 安装：`npm install vue-cli -g`#全局安装 vue-cli 工具，安装后可以使用 vue 命令初始化项目。
- 初始化：`vue init webpack test `#配置更开发，适合中大型。`vue create project`#配置较简单。
- **vue-cli-service**：该 service 相当于是使用 node 语言书写的一个本地服务，包括默认从 vue.config.js 读取配置（所以与 webpack-service 使用时的配置有些差异），运行 webpack 这些操作。所以也可以根据这些逻辑自己写一个恶脚手架。
- **可视化管理**：cmd/输入：vue ui 打开 vue 的开始化管理界面，导入项目，然后进去查看详细。

相关资源：

- [package.json 文件各种属性解释](https://zhuanlan.zhihu.com/p/33928507)。[v3 直达](https://v3.cn.vuejs.org/guide/migration/introduction.html#%E5%BF%AB%E9%80%9F%E5%BC%80%E5%A7%8B)、[使用 ts 的创建。](https://zhuanlan.zhihu.com/p/99343202)
- [vite.config.js 配置](https://vitejs.dev/config/#server-port)、[vuejs 官网。](https://cn.vuejs.org/v2/guide/)、[vue 深入原理参考学习地址](https://zhuanlan.zhihu.com/p/101330697)、[生命周期解释](https://www.cnblogs.com/wzndkj/p/9612647.html)、[具体介绍学习地址。](https://blog.csdn.net/weixin_34023863/article/details/87945630)

**问题集**：

- linux 上：安装 vue-cli 后会在所的 nodejs/bin 下看到 vue。(npm config list#可以查看这个文件的位置)。为这个 vue 建立一个软链接将其放到/usr/local/bin 下，`sudo ln -s /home/wcs/software/nodejs/bin/vue /usr/local/bin/vue`
- windows 上：将`C:\Users\wcs\AppData\Roaming\npm`#vue 被下载到该文件，添加到环境变量即可。

## a2、基本使用：

**$attrs 与\$listeners**：

```html
<!--子组件-->
<label>输入框：</label><input v-bind="$Allattrs" v-on="$listenserAll" />
<script>
  export default {
    name: "pop",
    computed: {
      $Allattrs() {
        return this.$attrs; //this.$attrs表示绑定在该组件上的所有属性。
      },
      $listenserAll() {
        //this.$listeners也是表示从父组件接收到的所有绑定事件。
        return Object.assign({}, this.$listeners, {
          input: (event) => this.$emit("input", event.target.value),
        });
      },
    },
  };
</script>
<!--父组件,native修饰符的事件不会出现在$listeners中-->
<pop
  placeholder="$attrs支持不使用bind写法传值"
  @focus="focus"
  @input="inp"
  @change.native="change"
/>
```

- **循环**：

```html
<li v-for="i in is">
  <h5>{{ i }}</h5>
  <div v-if="i == 0" v-html="a">这是i</div>
  <div v-else-if="i == 1" v-html="b">这是else</div>
  <div v-else v-html="c"></div>
</li>
// 常用情况,key尽量使用一个唯一的值，不使用索引。
<p v-for="(val,idx) in phones" :key="idx">{{ val.text }}</p>
```

**注**：由于 vue2.x 使用 Object.defineProperty 监听对象，数组数据无法监听到改变，尽量使用 Array 自带方法：splice/push 等操作数组，或$forceUpdate 强制刷新。

- **method**：

```js
var v = new Vue({
  el: "#view",
  data: { name: "error" },
  method: {
    alter: function () {
      this.name = "vue";
    },
  }, // 这里的this指向的是method
  //所以data中的数据已被逐一放置到method中
  component: { template: "<h3>dkl</h3>" },
});
v.alter(); //直接运行函数
```

调用方法集中的函数：v.alter()直接调用，或原始中`<p v-on:click="alter()"></p>`，v-on 绑定的事件是动态绑定的所以使用 v-for 循环出来也能使用。

- **样式绑定**：

```html
<div v-bind:class="{a:isa,b:isb}"></div>
<!--isa为true时将类名a绑定-->
<p v-bind:class="[a,b]"></p>
// 绑定多个类名
<a v-bind:style="styObj"></a>//styObj是js中定义好的变量，内嵌样式
<b v-bind:style="{ width: w + 'px',color: col }"> </b>
```

- **计算属性与监听属性**：与 methods 是一个函数集对象，不过 computed 中的函数可以直接放到模板中<b class="violet">computed 一般用于页面渲染的数据，watch 一般监听一个值改变影响较大情况。</b>：

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
    },
    "obj.name"(){
        //也可以这样来监听一个对象的属性。
    }
}
```

- **事件绑定中传入 event 参数**：

```js
<p v-on:click="get($event)"></p>;
function get(e) {
  // 使用此法来获取当前元素。*********注意！就算get中不传入$event对象，也会默认传入。
  e.target.style.color = "red"; //若绑定事件的元素中有多个子元素请用
  //currentTarget,因为可能点Z中的是子元素，触发事件的却是因为事件冒泡
}
```

**插件**：

```js
//plugin.js放置 插件格式,一个对象。
export plugin = {
    install(vue,params){//第一个会被传入vue对象。
        vue.prototype.plugin = function(){}
    }
}
//main.js
import {plugin} from "./plugin.js";
vue.use(plugin,"hello");//use方法会调用plugin的install()函数
```

## a3、组件：

第三方的组件一般安装后可直接单个页面按需引入，对应的插件安装后也可以单页面直接引入使用。子组件使用的数据最好是在父组件 mounted 之前就生成。

```js
<script>
// 全局注册，写在main.js文件中
Vue.component("wcs",{
    template:'<h1>{{ info }}</h1>',
    props:['info'],
    data:{},
    props:[],
    methods:{}
});// 页面中直接<wcs></wcs>即
</script>
/*======================
    父组件值改变，子组件不刷新问题
========================*/
<child :key="dateStream" :forms="useForm"/>
<script>
alter(){
    this.ajaxRequest();
    this.dialogOpen = true;                        //会先打开子组件，但数据还没拿到。
},
ajaxRequest(){
    ajax({..}).then(r=>{
        this.useForm = {...};
        this.dataStream = new Date().getTime();    //更改子组件key值，此时会再次刷新子组件。
    })
}
</script>
```

**局部注册**：

```html
<!--av是子组件test中的props中定义的值，当是一个对象时可以直接v-bind。:av="nm"(mpvue中的简写)。
.async表示组件内修改值也改变组件外的值，两者同步。
-->
<test v-bind:av="nm" v-bind="post" :varray.async="datas"></test>
import test from '../component/test' ... components:{test}
```

<i class="label2">prop 验证</i>在父组件向子组件中的 props 传递值时，props 的值可以预先写定一个类型数据来做验证，若传来的值不满足验证则会有 warn 提示。

```js
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

**keep-alive 的使用**：用于缓存组件，具体如下：

- **原理**：根据组件 ID 和 tag 生成缓存 Key,并在缓存对象中查找是否已缓存过该组件实例。如果存在,直接取出缓存值并更新该 key 在 this.keys 中的位置。在 this.cache 对象中存储该组件实例并保存 key 值,之后检查缓存的实例数量是否超过 max 的设置值,超过则根据 LRU 置换策略删除最近最久未使用的实例。

```html
<!--include和exclude用于匹配组件的name，满足匹配项的才会缓存或不缓存，也可以是一个列表-->
<keep-alive :include="[/login/,'/acc/']" :exclude="/acc/">
  <login />
</keep-alive>
```

- **两个额外的钩子函数**：由于组件被缓存起来，再次使用到该组件时不会触发它的一系列生命周期函数，可用如下钩子判断是否处于使用中。

```js
export default {
  activated() {
    //活跃状态，在使用时触发,即使第一次进入页面也会触发。
  },
  deactivated() {
    //不使用时触发
  },
};
```

**组件中使用插槽**：有时候我们定义一个组件不能完全应付所有场景，比如一个底部弹出框，有的有选择项，有的是展示商品内容，如果靠传值来控制显示，会导致子组件内东西非常多。而分为多个组件来写，它们之间又有一些共用的东西，所以产生了插槽。

```html
// 第一个子组件的内容
<template v-slot:head
  >// v-slot的值对应第三个子组件中slot的name属性。具名插槽可以缩写为#head
  <div>第一个子组件内容{{ name }}</div>
</template>
// 第二个子组件的内容
<template v-slot:[slotType]
  >//
  只能用在template标签上。用[]时就是使用动态插槽名，改变slotType值可以改变要插入的插槽。
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
    <hello>
      //这里的hello是子组件3
      <c1></c1> //这是子组件1，也可以这这个标签中写v-slot:head属性。
    </hello>
  </div>
</template>
```

**插槽作用域**：用于子组件中的数据想提供给父组件任意展示。[学习地址。](https://blog.csdn.net/lzl980111/article/details/104783252/)

```html
<!--子组件中-->
<template>
  <div><slot :data="dts"></slot></div>
  <!--绑定一个数据上去-->
</template>
<script>
  export default {
    name: "child",
    data() {
      return { dts: [1, 2, 3] };
    },
  };
</script>

<!--父组件中-->
<template>
  <div>
    <child slot-scope="slot"
      ><!--数据都在slot下-->
      <span>{{ slot.dts.join('-') }}</span>
    </child>
  </div>
</template>
```

**动态组件和异步组件**：使用 component 标签和 v-bind:is 属性来切换组件。

```html
<keep-alive>// 外面套上keep-alive标签后，加载过的组件会被缓存下来，再切回去的时候不会重新渲染。
  <component v-bind:is="name"></component> //component是vue内部自带的已注册的标签名，修改name值(对应组件名称)来在这个位置切换组件。
</keep-alive>
data:{
    name:'test'
},
components:{
    test,
    vv:()=>import("../components/vv"),//该组件会被单独打包成代码块，使用时才会被以<script>的形式引入页面。
    cc:() => ({    //定义异步组件加载时的一些其它行为。
      // 需要加载的组件 (应该是一个 `Promise` 对象)
      component: import('./MyComponent.vue'),// 异步组件加载时使用的组件
      loading: LoadingComponent,// 加载时使用的组件
      error: ErrorComponent,// 失败时使用的组件。
      delay: 200,// 如果提供了超时时间且组件加载也超时了，
      // 则使用加载失败时使用的组件。默认值是：`Infinity`
      timeout: 3000 //超过该时间不再加载。毫秒
    }),
   // 直接使用渲染函数
   abc: {
      render(cre) {
        return cre(
          "h1",
          {style: { color: "red" }},
          "content-ccc"
        );
      },
    }
}
```

**异步组件原理**：内部调用 createComponent()方法创建组件，异步的写法是一个函数，判断到组件是一个函数的情况会将组件内容赋值给 asyncFactory(一个 promise)，然后传给 resolveAsyncComponent()，其内部会执行 asyncFactory 创建一个空的虚拟节点，加载完之后会调 factory 函数传入 resolve 和 reject 两个参数，执行后返回一个成功的回调和失败的回调，promise 成功了就会调 resolve，resolve 中就会调取 forceRender 方法强制更新视图重新渲染。<b c=gn>异步组件被打包成单独的 bundle，如 v-if 使用组件时，才会从服务器下载相应的 js 文件。</b>[参考学习地址](https://blog.csdn.net/qq_42072086/article/details/109642272)。
**边界情况**：官网中将以下子组件访问父组件，父组件访问子组件数据等称为边界情况。
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
**元素选择器**：`<p ref="aa"></p>` ref 标记元素，`this.$refs.aa选中元素，如果绑定的是一个组件还可以继续this.$refs.aa.get()`调起组件内的方法。
<i class="label3">依赖注入</i>类似访问父组件实例的情况，不过依赖注入可以在后代组件中都访问到，而且不用暴露所有父组件实例。

```js
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

依赖注入还是有负面影响的。它将你应用程序中的组件与它们当前的组织方式耦合起来，使重构变得更加困难。同时所提供的属性是非响应式的。这是出于设计的考虑，因为使用它们来创建一个中心化规模化的数据跟使用 $root 做这件事都是不够好的。
**组件上使用 v-model 与 sync 修饰符**:

```html
<!--父组件-->
<pop
  v-model="stateContent"
  :cs.sync="[1,2,3]"
/><!--sync修饰的数据其子组件内可以直接更改，且父组件也会跟着变化-->
<!--子组件-->
<template>
  <div class="pop">
    <!--注意，绑定value，而不是v-model-->
    <div>
      <input :value="state" v-on:input="alt($event)" placeholder="请输入" />
    </div>
  </div>
</template>
<script>
  export default {
    props: {
      state: { default: "" },
      cs: Array,
    },
    model: {
      // model中需要指定改变的props中的值和使用哪个事件改变。
      prop: "state",
      event: "change",
    },
    methods: {
      alt(e) {
        let c = e.target.value;
        this.cs.push("h");
        this.$emit("change", c); // 子组件中使用触发事件更改父组件的值，即props中的值。
      },
    },
  };
</script>
```

<i class="label3">第三方组件库安装</i>多数组件库都支持全局注册和按需使用，两者方式稍有区别。
全局引入：较为简单，安装后直接入口文件引入，Vue.use()使用插件，然后倒入相关样式文件，各组件内直接按语法使用即可。
按需引入：如果支持 babel 中配置的可以在 babel-loader 的配置项中写入（入口 js 文件中也要导入样式文件）：

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

## a4、vuex 的使用：

一个全局变量管理控件。[vuex 使用学习地址。](https://segmentfault.com/a/1190000015782272)[vuex 官网。](https://vuex.vuejs.org/zh/guide/)
安装：`npm install vuex --save`#然后在 src 文件夹下新建一个 store 文件夹，store 内再建一个 Index.js 文件，文件内容如下：

```js
import Vue from "vue";
import Vuex from "vuex";
Vue.use(Vuex);

const state = {
  //要设置的全局访问的state对象
  showFooter: true,
  changableNum: 0,
  //要设置的初始属性值
};

/**-----当state中数据量，结构比较复杂时，要获取state中一些较深结构的值会比较麻烦
而且从设计原则上考虑也应该用一些函数来单独获取值。
*/
const getters = {
  //实时监听state值的变化(最新状态)
  isShow(state) {
    //承载变化的showFooter的值
    return state.showFooter;
  },
  getChangedNum(state) {
    //承载变化的changebleNum的值
    return state.changableNum;
  },
};
const mutations = {
  show(state) {
    //自定义改变state初始值的方法，这里面的参数除了state之外还可以再传额外的参数(变量或对象);
    state.showFooter = true;
  },
  hide(state) {
    //同上
    state.showFooter = false;
  },
  newNum(state, sum) {
    //同上，这里面的参数除了state之外还传了需要增加的值sum
    state.changableNum += sum;
  },
};
const actions = {
  //异步运行
  hideFooter(context) {
    //自定义触发mutations里函数的方法，context与store 实例具有相同方法和属性
    context.commit("hide");
  },
  showFooter(context) {
    //同上注释
    context.commit("show");
    context.commit("user/login"); //使用斜杆方法调用其它模块的方法
  },
  getNewNum(context, num) {
    //同上注释，num为要变化的形参
    context.commit("newNum", num);
  },
};
const store = new Vuex.Store({
  state,
  getters,
  mutations,
  actions,
});
export default store;

// main.js文件中。
import store from "./store"; //引入store

new Vue({
  el: "#app",
  router,
  store, //使用store
  template: "<App/>",
  components: { App },
});
// 使用
this.store.state.changebleNum; //可直接获取到值。
this.store.commit("newNum", 6); //运行mutation中定义的函数。
this.$store.dispatch("hideFooter"); //运行actions中定义的函数。
// 有多模块情况使用：
this.$store.dispatch("user/getInfo");
```

大多数的项目中，我们对于全局状态的管理并不仅仅一种情况的需求，有时有多方面的需求，比如写一个商城项目，你所用到的全局 state 可能是关于购物车这一块儿的也有可能是关于商品价格这一块儿的；像这样的情况我们就要考虑使用 vuex 中的 modules 模块化了。在 store 文件夹下面新建一个 modules 文件夹，然后在 modules 文件里面建立需要管理状态的 js 文件

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

## a5、路由：

```js
import Vue from 'vue';
import Router from 'vue-router';
Vue.use(Router); //全局注册路由，这样<router-view/>才会生效

const router = new Router({...});
new Vue({
    el: '#home',
    router,//放到vue中，之后可使用路由函数。
    ...
});
```

在 router 文件夹下的 index.js 文件中为每个页面添加路由。路由还提供一些钩子函数供控制跳转页面使用：

```js
{// 这是Index.js文件中配置路由时的一个页面。单个路由里的钩子函数：
    path:'/',
    name:'aa',
    //使用import实现路由的懒加载，webpack中会以import做分割点将单独路由分割成块快，访问该页面时才会请求该js文件，渲染路由。
    component:import('../pages/av.vue'),
    beforeEnter:(to,from,next)=>{    //钩子函数。准备进入路由时触发
        console.log(from,to);//from，to分别是当前页，要跳转的目标页，的信息。可以获取其中信息做一些限制。
        next(false);//传入false的话则不能跳转。
    },
    alias:'/b' //别名，跳转到该页时使用的路径名
}

//组件路由：和上面的钩子函数类似，不过这个是写在每个页面的组件里的：
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

**全局路由钩子**：在 main.js 页面添加。

```js
// main.js添加
router.beforeEach((to, from, next) => {
  //每个页面跳转时都会调用。改变标题
  window.document.title = to.meta.title;
  router.addRoutes(newRoutes); //可以添加一些新的路由
  next(); //next({path:"/"}),还可以传路径来重定向路由，传false则禁止跳转。
});
//离开页面后触发，可在此关闭加载动画。
router.afterEach((to, from) => {
  loading = false;
});
```

<i class="label1">router 的两种模式：</i>hash 模式背后的原理是 onhashchange。因为 hash 发生变化的 url 都会被浏览器记录下来，从而你会发现浏览器的前进后退都可以用了，同时点击后退时，页面字体颜色也会发生变化。这样一来，尽管浏览器没有请求服务器，但是页面状态和 url 一一关联起来，后来人们给它起了一个霸气的名字叫前端路由，成为了单页应用标配。[学习地址。](https://www.cnblogs.com/imgss/p/7492333.html)

**模式切换**：<b c=v>history 模式是配合服务端渲染使用。一般服务端将所有路径都重定向到首页，路由交给前端处理。</b>

```js
export default new Router({
  mode: "history", // 默认是hash
  base: "/base", //hash和history模式使用的基础路径。打包放到部署时，包名与此一致。
  routes: [
    {
      path: "/",
      name: "HelloWorld",
      component: HelloWorld,
      // 重定向也可以使用函数，做假跳转。！！！如果对应的重定向路径也是一级路由，那么会直接跳转该页。
      direct: "/child", //访问该页面时路径变为/index（得在children配置），但router-view显示的是component的。
      children: [{ path: "/index", name: "index" }],
    },
  ],
});
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
    //path:"/hello/:nav(.*)"
    name:"book",
    component:()=>import('../book')
}
this.$router.push({name:"book",params:{id:110}}); //页面地址变为/book/110。注意这些页面使用的是同一个页面。
```

**子路由/二级路由**：在单页面上再加一个`<router-view/>`，示例如下：

```vue
<router-view />
<!--App.vue页面使用一个路由标签-->
//---路由中将二级路由配置在children中 { path:"home", children:[{ path:"er" }] }
```

home 页面再使用路由标签，**对路由使用 keep-alive**:

```html
<template>
  <router-link to="/er">到er页面</router-link>
  <router-view /><!--二级路由页面显示在这里。-->
</template>
<transition name="fade" mode="in-out">
  <keep-alive
    ><!--这是个更好的使用方法，返回页面时滚动条位置不变-->
    <router-view v-if="$route.meta.keepAlive" />
  </keep-alive>
</transition>
<transition name="fade" mode="in-out">
  <router-view v-if="!$route.meta.keepAlive" />
</transition>
```

**动态添加路由**：

```js
import Router from 'vue-router';
router = new Router({mode:"",base:"",routes:[..]});
// 动态添加路由配置：
router.addRoutes([{path:"/",component:require('@cmp/eye.vue'),name:""}]);
```

## b1、混入：

混入 (mixin) 提供了一种非常灵活的方式，来分发 Vue 组件中的可复用功能。[学习地址。](https://www.jianshu.com/p/1bfd582da93e)

```js
// 局部混入。mixin中的像建立一个vue实例时那样创建created,mounted等属性，这些会被合并到vue实例中，发生冲突时与组件中定义的为准。
var mixin = {
  created: function () {
    console.log("混入对象的钩子被调用");
  },
};

new Vue({
  mixins: [mixin],
  data: {},
});
// 全局混入
Vue.mixin({
  created: function () {
    var myOption = this.$options.myOption;
    if (myOption) {
      console.log(myOption);
    }
  },
});
```

**使用场景**：可复用的功能，或那种因为解耦将同一页面分为两个，这两个页面组件一样但逻辑有差异，那么它们相同的功能部分就可以单独定义出来，然后使用 mixins 组合。

```js
const mixin1 = {
  data() {
    return { name: "www", age: 20 };
  },
  methods: {
    hello() {
      console.info(this.name);
    },
  },
  created() {
    console.warn("mixin result", this.name);
  },
};
const mixin2 = {
  data() {
    return { job: "ai", addr: "ttk" };
  },
  methods: {
    hello() {
      console.info(this.job);
    },
  },
  mounted() {
    console.info("mixin2 res");
    this.skip();
  },
};
export default {
  mixins: [mixin1, mixin2], //使用混入，按照这个顺序覆盖前面的data，methods中相同的部分（初始化阶段完成），然后执行它们的周期函数。
  data() {
    return { name: "last" };
  },
  created() {
    console.info("最后执行");
  },
};
```

## b2、自定义指令：

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

**钩子函数**：

- **bind**：只调用一次，指令第一次绑定到元素时调用。在这里可以进行一次性的初始化设置。
- **inserted**：被绑定元素插入父节点时调用 (仅保证父节点存在，但不一定已被插入文档中)。
- **update**：所在组件的 VNode 更新时调用，但是可能发生在其子 VNode 更新之前。指令的值可能发生了改变，但是你可以通过比较更新前后的值来忽略不必要的模板更新 (详细的钩子函数参数见下)。
- **componentUpdated**：指令所在组件的 VNode 及其子 VNode 全部更新后调用。
- **unbind**：只调用一次，指令与元素解绑时调用。

**钩子函数参数**：指令钩子函数会被传入以下参数

- el：指令所绑定的元素，可以用来直接操作 DOM。
- binding：一个对象，包含以下属性：
- name：指令名，不包括 v- 前缀。
- value：指令的绑定值，例如：v-my-directive="1 + 1" 中，绑定值为 2。
- oldValue：指令绑定的前一个值，仅在 update 和 componentUpdated 钩子中可用。无论值是否改变都可用。
- expression：字符串形式的指令表达式。例如 v-my-directive="1 + 1" 中，表达式为 "1 + 1"。
- arg：传给指令的参数，可选。例如 v-my-directive:foo 中，参数为 "foo"。
- modifiers：一个包含修饰符的对象。例如：v-my-directive.foo.bar 中，修饰符对象为 { foo: true, bar: true }。
- vnode：Vue 编译生成的虚拟节点。移步 VNode API 来了解更多详情。
- oldVnode：上一个虚拟节点，仅在 update 和 componentUpdated 钩子中可用。

## b3、渲染函数&jsx：

Vue 推荐在绝大多数情况下使用模板来创建你的 HTML。然而在一些场景中，你真的需要 JavaScript 的完全编程的能力。这时你可以用渲染函数，它比模板更接近编译器。

```js
Vue.component("anchored-heading", {
  data() {},
  functional: true, //为true时，render函数的第二个参数可以使用，来获取同级的data，props参数等；
  render: function (createElement, context) {
    // render渲染函数，在生命周期函数中也是使用该函数来解析组建的。
    return createElement(
      "h1", // 标签名称
      {
        //这个对象内部定义一些模板的事件、指令、插槽类的东西。
        class: { foo: true, bar: false },
        // 与 `v-bind:style` 的 API 相同，// 接受一个字符串、对象，或对象组成的数组
        style: { color: "red", fontSize: "14px" },
        // 普通的 HTML attribute
        attrs: { id: "foo" },
        // 组件 prop
        props: { myProp: "bar" },
        // DOM 属性
        domProps: { innerHTML: "baz" },
        // 事件监听器在 `on` 属性内，// 但不再支持如 `v-on:keyup.enter` 这样的修饰器。// 需要在处理函数中手动检查 keyCode。
        on: { click: this.clickHandler },
        // 仅用于组件，用于监听原生事件，而不是组件内部使用/ `vm.$emit` 触发的事件。
        nativeOn: { click: this.nativeClickHandler },
        // 自定义指令。注意，你无法对 `binding` 中的 `oldValue`// 赋值，因为 Vue 已经自动为你进行了同步。
        directives: [
          {
            name: "my-custom-directive",
            value: "2",
            expression: "1 + 1",
            arg: "foo",
            modifiers: { bar: true },
          },
        ],
        // 作用域插槽的格式为// { name: props => VNode | Array<VNode> }
        scopedSlots: { default: (props) => createElement("span", props.text) },
        // 如果组件是其它组件的子组件，需为插槽指定名称
        slot: "name-of-slot",
        // 其它特殊顶层属性
        key: "myKey",
        ref: "myRef",
        // 如果你在渲染函数中给多个元素都应用了相同的 ref 名，// 那么 `$refs.myRef` 会变成一个数组。
        refInFor: true,
      },
      [
        "先写一些文字", // 这是h1标签的一个文本节点。
        createElement("h1", "一则头条"),
        createElement(MyComponent, {
          // 相当于创建一个组件的子组件。
          props: {
            someProp: "foobar",
          },
        }),
      ]
    );
  },
});
```

## b4、插件：

vuejs 的插件是与 vue 实例分开的，使用时与 vue 原型绑定在一起。

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

## b6、过渡，动画：

vuejs 有提供元素在插入，移除时做动画封装，使用起来还算方便。

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

## c1、vue.config.js

```js
module.exports = {
  devServer: {},
  publicPath: "./",
  //如果是一个对象(这里写成函数形式)，则config中配置的属性会合并到最终配置上。
  configureWebpack: (config) => {
    config.outputDie = "dist";
  },
  chainWebpack: (config) => {
    // 配置title
    config.plugin("html").tap((args) => {
      args[0].title = "进销存系统";
      return args;
    });
    //这里配置loader
    config.module
      .rule("vue")
      .use("vue-loader")
      .loader("vue-loader")
      .tap((options) => {
        return options;
      })
      .end();
    //这样配置plugin。
    config
      .plugin("define")
      .tag((arg) => {
        arg[0]["process.env"] = "dev";
        return arg;
      })
      .end();
  },
  css: {
    extract: true, //组件内css抽取到一个单独css文件
    sourceMap: true, //开启css的sourceMap
    loaderOptions: {
      //css相关的loader部分配置。
      css: {}, //这个配置传递给css-loader
      postcss: {}, //这个配置会传递给postcss-loader
    },
  },
};
```

**添加环境**：package.json/scripts 中添加：`"vue-cil server --mode mock"`，根目录中可添加`.env.mock`来写一些要用的全局变量。默认有 development 和 production。

- `process.env.NODE_ENV`的值默认也会变为`--mode`后面的环境值。

```py
# 可在此处再次更改其值。
NODE_ENV = "production"
# 在vue.config.js均可使用
MODE = "dev"
# 要在vue项目中使用，必须前缀是VUE_APP。
VUE_APP_BASE_API = '/base-api'

VUE_APP_BG_API = '/bg-api'
```

- [vue.config.js 官方配置文档](https://cli.vuejs.org/zh/config/#outputdir)

## c2、常用修饰符：

```html
<child-component
  :data.sync="tables"
/><!--sync让子组件可以修改该prop的值，且同步到父组件-->
<div @click.once="hh"></div>
<!--once：事件只能用一次-->
<div @click.prevent="hh"></div>
<!--prevent：阻止默认行为-->
<div @click.self="hh"></div>
<!--self:只有元素本身触发时才触发方法，-->
<div @click.stop="hh"></div>
<!--stop：阻止事件冒泡-->

<input
  v-model.lazy="val"
/><!--lazy:这个修饰符会在光标离开input框才会更新数据-->
<input v-model.trim="val" /><!--trim:输入框过滤首尾的空格-->
<input
  v-model.number="val"
/><!--number:先输入数字就会限制输入只能是数字，先字符串就相当于没有加numbe-->
```

## c3、extend()使用：

```js
import locp from "@/components/loading/loading.vue";
import Vue from "vue";
//https://blog.csdn.net/qq_39024012/article/details/108152290
const loade = Vue.extend(locp); //解析组件生成一个实列

const control = new loade();
control.$mount(document.body); //将组件挂载到页面元素上
// 控制
const loading = {
  show() {
    control.show = true; //show是组件locp,data中的数据
  },
  cancel() {
    control.show = false;
  },
};

export default loading; //导出后可在ajax拦截器，等全局使用。
```
