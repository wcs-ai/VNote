# 一、离线web应用
**html部分离线定义**：
```html
<!DOCTYPE HTML>
<!--cache.appcache放在与该html文件同目录下；文件中指定缓存相关的控制信息-->
<html manifest="cache.appcache"></html>
```
cache.appcache内容如下：
- 开头为默认区域；CACHE后面定义要缓存的文件；
- FALLBACK定义未被离线缓存的资源，使用的默认；支持匹配；
- NETWORK：定义不缓存的文件；
```
CACHE MANIFEST

index.html
abc.png

CACHE:
hello.png

FALLBACK:
*.png default.png
* offline.html    #点击的目标链接未被缓存时，使用的默认页面

NETWORK:
acc.jpg
```
**接口的离线处理**：
```js
/******状态判断******/
if(window.navigator.onLine){
    alert("在线状态");
}else{
    alert("离线状态");
}
/*使用离线，返回的属性如下：
update()        更新缓存
swapCache()    交换当前缓存与较新缓存
status        缓存的状态
*/
var cs = window.applicationCache;

/******离线时使用代理处理接口********/
// index.js
if (navigator.serviceWorker) {
  navigator.serviceWorker
    .register('sw.js')
    .then(function(registration) {
      console.log('service worker 注册成功')
    })
    .catch(function(err) {
      console.log('servcie worker 注册失败')
    })
}
// ---------sw.js
// 监听 `install` 事件，回调中缓存所需文件
self.addEventListener('install', e => {
  e.waitUntil(
    caches.open('my-cache').then(function(cache) {
      return cache.addAll(['./index.html', './index.js'])
    })
  )
})

// 拦截所有请求事件
// 如果缓存中已经有请求的数据就直接用缓存，否则去请求数据
self.addEventListener('fetch', e => {
  e.respondWith(
    caches.match(e.request).then(function(response) {
      if (response) {
        return response
      }
      console.log('fetch source')
    })
  )
})
```


# 二、vuejs：

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

# 三、vue性能优化

## 1、函数式组件

**介绍**：该类型组件不支持响应式，不能通过this关键字引用，一般用于定义没有响应数据，只接收props参数，显示组件内容情况；

函数式组件和普通的对象类型的组件不同，它不会被看作成一个真正的组件，我们知道在 `patch` 过程中，如果遇到一个节点是组件 `vnode`，会递归执行子组件的初始化过程；而函数式组件的 `render` 生成的是普通的 `vnode`，不会有递归子组件的过程，因此渲染开销会低很多；

```html
<!--functional声明其为函数式组件-->
<template functional>
  <div class="cell">
    <div v-if="props.value" class="on"></div>
    <section v-else class="off"></section>
  </div>
</template>
```

## 2、无需实时的任务放到子组件

若父组件刷新频率可能较高，那些不用实时跟随变动的操作可以放与子组件中，且里面不设响应式数据，这样父组件刷新时子组件并不会刷新；

## 3、尽量少的响应式变量

每次使用this获取响应式变量时都会触发getter的一系列执行，将其保存为局部变量使用，或部分使用全局变量；

## 4、组件延时渲染

子组件过多时，异步组件也同样可能卡顿，可用延时来渲染部分组件


# 四、React
## d1、安装
- create-react-app安装：`npm install create-react-app -g`（使用node 14.0以上版本）
- 创建react-app：`create-react-app react-demo`
## d2、jsx示例
JSX 语法被 @babel/preset-react 插件编译为 createElement() 方法
```jsx
import React,{useRef,useState} from 'react';
import Child from "./Child";

// demo类
class Demo extends React.Component{
  constructor(props){
    // props是使用该组件时传递来的参数map
    super(props);
    this.state = {
      name:'wcs',
      age:'unknown',
      val:3,
      dom:this.yieldAchieveList(),
    };
    this.ffc = 11;
    // 类组件的ref使用
    this.childRefs = React.createRef();
    this.inpRef = React.createRef();
    // ******如此绑定的事件，handleBtn()才能访问到本类实例
    // 或者绑定时：<button onClick={(e) => this.handleClick(e)}>
    this.handleBtn = this.handleBtn.bind(this);
    //*******供子组件调用的方法也绑定this
    this.parentFun = this.parentFun.bind(this);
  }
  componentWillMount(){console.log('[生命周期-组件挂载之前执行]');}
  componentDidMount() {console.log('[生命周期-创建dom后触发]');}
  componentWillReceiveProps(nextProps,nextContext){console.log('[传入的props有改变后触发（初次渲染不会执行）]');}
  componentWillUnmount() {console.log('[生命周期-卸载组件后触发]')}
  shouldComponentUpdate(nextProps,nextState){
    console.log('[钩子函数-反回false时不会渲染组件]')
    return true;
  }
  yieldAchieveList(){
    // ******jsx中的样式写法和列表
    let arr = [];
    ['web','java','python','c++'].map((v,ix)=>{
      arr.push(<span style={{margin:'0 10px'}} key={v}>{v}</span>);
    });
    return arr;
  }
  //*****事件：e是组合的事件 */
  handleBtn(e){
    /********设置状态：
    setState()只在合成事件和钩子函数中是“异步”的(模拟的异步)，在原生事件和 setTimeout 中都是同步的。
    */
    this.setState({age:'86'});
    /*******current下面才是子组件实例*/
    var x = this.childRefs.current.getCount();
  }
  // *********input框必须绑定change事件 或readOnly
  inputChange(event){
    this.setState({
      val: event.target.value
    });
  }
  parentFun(v){
    console.info('[子组件来信]',this.state);
  }
  //******渲染视图使用（每次渲染都会运行该函数，这里尽量避免与视图无关的logic）
  render(){
    const batchProp = {page:1,size:10,useTable:false};
    return(
      <div className="user-info">
        {/*普通内容渲染*/}
        <p>用户名：{this.state.name}；年龄：{this.state.age}
        {/****普通元素也可以用ref选择*/}
        <input ref={this.inpRef} value={this.state.val} onChange={(e)=>this.inputChange(e)}/> 
        <button onClick={this.handleBtn}>生成列表</button>
        </p>
        <p>{this.state.dom}</p>
        {/******向子组件传递方法，供子组件触发向父组件通信
          后面是多个prop是一次性批量传入
        ***/}
        <Child ref={this.childRefs} name='aa' pfn={this.parentFun} {...batchProp}/>
      </div>
    );
  }
}

export default Demo;
```
**组件插槽**（父组件渲染时子组件也会跟着渲染）
```jsx
import React, { Component } from 'react'

class Child extends Component {
    //********钩子函数，用来控制是否渲染
    shouldComponentUpdate(nextProps,nextState){
      // true时表示进行渲染，false则不会
      return true;
    }
    render() {
        return (
            <div>
                传入的所有插槽在children中
                {this.props.children[0]}
                {this.props.children[1]}
                {this.props.children[2]}
            </div>
        )
    }
}
export default class Children extends Component {
  render() {
    return (
      <div><Child><div>11111</div><div>22222</div><div>33333</div></Child></div>
    )
  }
}
```
[父子组件交互](https://blog.csdn.net/qq_44472790/article/details/124994164)
## d3、react-route

```js
import {NavLink,useNavigate,useParams,useSearchParams} from 'react-router-dom';
<NavLink to="/home/help" />
// 编程式跳转
const navigate = useNavigate();
navigate('/login',{replace:true});//replace 指定是否是替换
navigate(-1);// 回退
//*****传参方式1
navigate.push('/single-blog/123');
const parmas = useParams();
// 传参方式2
navigate.push('/single-blog?hello=rrr');
const search = useSearchParams();
```

[参考学习地址](https://blog.csdn.net/ZHANGYANG_1109/article/details/126022959)

## d4、redux全局状态管理
- 有actions，和reducer构成；[官方文档](https://www.redux.org.cn/docs/basics/UsageWithReact.html)
- actions 只是描述了有事情发生了这一事实，并没有描述应用如何更新 state。
- reducer 就是一个纯函数，接收旧的 state 和 action，返回新的 state。
- 永远**不要**在 reducer 里做这些操作：
（1）修改传入参数；
（2）执行有副作用的操作，如 API 请求和路由跳转；
（3）调用非纯函数，如 Date.now() 或 Math.random()

- actions.js示例
```js
/*action 类型*/
export const ADD_TODO = 'ADD_TODO';
export const TOGGLE_TODO = 'TOGGLE_TODO'
export const SET_VISIBILITY_FILTER = 'SET_VISIBILITY_FILTER'
/*其它的常量*/
export const VisibilityFilters = {
  SHOW_ALL: 'SHOW_ALL',
  SHOW_COMPLETED: 'SHOW_COMPLETED',
  SHOW_ACTIVE: 'SHOW_ACTIVE'
}
/*action 创建函数（type是必须的）*/
export function addTodo(text) {
  return { type: ADD_TODO, text }
}
export function toggleTodo(index) {
  return { type: TOGGLE_TODO, index }
}
export function setVisibilityFilter(filter) {
  return { type: SET_VISIBILITY_FILTER, filter }
}
```
- reducer.js示例
```js
//所做的只是生成一个函数，这个函数来调用你的一系列 reducer，每个 reducer 根据它们的 key 来筛选出 state 中的一部分数据并处理
import { combineReducers } from 'redux'
import {ADD_TODO,TOGGLE_TODO,SET_VISIBILITY_FILTER,VisibilityFilters} from './actions'
const { SHOW_ALL } = VisibilityFilters
// 每个reducer函数都是，匹配对应的state时做对应的事
function visibilityFilter(state = SHOW_ALL, action) {
  switch (action.type) {
    case SET_VISIBILITY_FILTER:
      return action.filter
    default:
      return state
  }
}
function todos(state = [], action) {
  switch (action.type) {
    case ADD_TODO:
      return [
        ...state,
        {
          text: action.text,
          completed: false
        }
      ]
    case TOGGLE_TODO:
      return state.map((todo, index) => {
        if (index === action.index) {
          return Object.assign({}, todo, {
            completed: !todo.completed
          })
        }
        return todo
      })
    default:
      return state
  }
}
const todoApp = combineReducers({
  visibilityFilter,
  todos
})
export default todoApp;
```
- 创建和发起action
```js
import { createStore } from 'redux'
import todoApp from './reducers'
let store = createStore(todoApp);
import {addTodo,toggleTodo,setVisibilityFilter,VisibilityFilters} from './actions';
// 打印初始状态
console.log(store.getState())
// 每次 state 更新时，打印日志
// 注意 subscribe() 返回一个函数用来注销监听器
const unsubscribe = store.subscribe(() =>
  console.log(store.getState())
)
// 发起一系列 action
store.dispatch(addTodo('Learn about actions'))
store.dispatch(toggleTodo(0))
// 停止监听 state 更新
unsubscribe();
import App from './App';
import { Provider } from "react-redux";
/*****Provider作为整个App的容器，传入Store，
 * 作为props，和放入整个应用的context中（为其创建contextType后，其它组件可引入使用）
*/
ReactDOM.render(
    <Provider store={store}>
      <App />
    </Provider>
  document.getElementById("root")
);
```
## d5、react-redux/connect
React-Redux 将所有组件分成两大类：UI 组件和容器组件。
- UI 组件：只负责 UI 的呈现，不带有任何业务逻辑，没有状态state值的使用，所以的参数是通过this.props获取。
- 容器组件：负责管理数据和业务逻辑，不负责 UI 的呈现
- connect作用：用于从 UI 组件生成容器组件
- [参考地址](https://blog.csdn.net/yoonerloop/article/details/112058929)

```js
import { connect } from 'react-redux';
import React from 'react';
class AppUI extends React.component{
  constructor(props){super(props);console.log(props.a)}
}
//******mapStateToProps：更新props作为输入源。返回一个对象，value为state处理的结果;
const mapStateToProps = (state) => {
    // 会订阅redux中的state数据；此对象将被添加到ui组件的props中
    return {value: state.count}
}
//*****mapDispatchToProps用于对state做修改的操作
const mapDispatchToProps = (dispatch, ownProps) => {
    return {
        onIncreaseClick: () => dispatch({type: 'increase'}),
        onReduceClick: () => dispatch({type: 'reduce'})
    }
//可以省略mapStateToProps参数：那样的话，UI 组件就不会订阅Store
export default connect(mapStateToProps, mapDispatchToProps)(AppUI);
```
## d6、context使用
创建context类型
```js
// 自定义Context  ThemeContext.js
import React from 'react';
const ThemeContext = React.createContext('light'); //初始化值为‘light’
export default ThemeContext;
```
修改及使用
```js
import ThemeContext from './context/ThemeContext.js';
import ThemedButton from './ThemedButton.js';

function App() {
  return (
    //使用了自定义Context的Provider，传入value覆盖了默认值，之后子组件读到的ThemeContext的值就是'dark'
    <ThemeContext.Provider value='dark'>
      <div className="App">
        <header className="App-header">
          <ThemedButton />
        </header>
      </div>
    </ThemeContext.Provider>
  );
}
// 子组件使用类似
class ThemedButton extends Component {
	static contextType = ThemeContext;
	render() {
		return <button>{this.context}</button>;
	}
}
```

# 五、经验集

| 描述               | 原因                                                                  | 解决                                                 |
| :----------------- | :-------------------------------------------------------------------- | :--------------------------------------------------- |
| 键盘弹起时影响布局 | 弹起时视窗,body等高度被压缩（非固定高时）fixed/absolute定位元素受影响 | 对应父元素写固定px高，或监听视窗高变化时隐藏对应元素 |
| 移动端尺寸处理     |                                                                       |                                                      |