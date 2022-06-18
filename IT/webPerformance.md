# web性能篇
# a、离线web应用
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
**js部分离线处理**：
```js
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
```

# b、vue性能优化

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