# web性能篇
## a、离线web应用
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