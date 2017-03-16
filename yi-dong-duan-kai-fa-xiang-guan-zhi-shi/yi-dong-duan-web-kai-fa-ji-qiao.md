#### 点击与click事件

对于a标记的点击导航，默认是在onclick事件中处理的。而移动客户端对onclick的响应相比PC浏览器有着明显的几百毫秒延迟。

在移动浏览器中对触摸事件的响应顺序应当是：

```bash
ontouchstart -> ontouchmove -> ontouchend -> onclick
```

因此，如果确实要加快对点击事件的响应，就应当绑定ontouchend事件。

#### 使用click会出现绑定点击区域闪一下的情况

解决：给该元素一个样式如下

```css
-webkit-tap-highlight-color: rgba(0,0,0,0);
```

如果不使用click，也不能简单的用touchstart或touchend替代，需要用touchstart的模拟一个click事件，并且不能发生touchmove事件，或者使用zepto中的tap（轻击）事件。

#### 滚动效果控制

```css
body {
    -webkit-overflow-scrolling: touch;//属性控制元素在移动设备上是否使用滚动回弹效果
}
//两个值
//auto： 使用普通滚动, 当手指从触摸屏上移开，滚动会立即停止
//touch：使用具有回弹效果的滚动, 当手指从触摸屏上移开，内容会继续保持一段时间的滚动效果。继续滚动的速度和持续的时间和滚动手势的强烈程度成正比。同时也会创建一个新的堆栈上下文。
```

用iphone或ipad浏览很长的网页滚动时的滑动效果很不错吧？不过如果是一个div，然后设置`height:200px;overflow:auto;`的话，可以滚动但是完全没有那滑动效果，很郁闷吧？

看到很多网站为了实现这一效果，用了第三方类库，最常用的是iscroll（包括新浪手机页，百度等） 我一开始也使用，不过自从用了`-webkit-overflow-scrolling: touch;`样式后，就完全可以抛弃第三方类库了，把它加在body{}区域，所有的overflow需要滚动的都可以生效了。

#### 锁定viewport

```js
ontouchmove="event.preventDefault()" //锁定viewport，任何屏幕操作不移动用户界面（弹出键盘除外）。
```

#### 利用media Query监听

```js
Window.matchMedia() //返回一个新的MediaQueryList 对象，表示指定的媒体查询字符串解析后的结果
//其中mediaQueryString参数是一个字符串，表示即将返回一个新MediaQueryList对象的媒体查询
```

设置一个查询列表用来判定设备屏幕处于横屏还是竖屏，那你可以像下面这样编码：

```js
var mql = window.matchMedia("(orientation: portrait)");
if (mql.matches) {
  /* The device is currently in portrait orientation */
} else {
  /* The device is currently in landscape orientation */
}
```

```js
if (window.matchMedia("(min-width: 400px)").matches) {
  /* the view port is at least 400 pixels wide */
} else {
  /* the view port is less than 400 pixels wide */
}
```

如果你需要持续观察查询结果值的变化情况，那么就很有必要来注册一个监听器，这比手动检查查询结果要有效很多.

```js
var mql = window.matchMedia("(orientation: portrait)");
mql.addListener(handleOrientationChange);
handleOrientationChange(mql);
```

上述代码创建了一个屏幕方向的测试查询列表mql，并且添加了事件监听。

需要注意的是，当我们添加监听后，我们其实直接调用了一次监听。这会让我们的监听器以目前设备方向来初始化判定代码。或者说如果我们代码设定设备处于竖屏模式，而实际上它启动时处于横屏模式，那么我们后面的判断就出现矛盾了。

我们可以在`handleOrientationChange()` 方法中来查看查询结果

```js
function handleOrientationChange(mql) {
  if (mql.matches) {
    /* The device is currently in portrait orientation */
  } else {
    /* The device is currently in landscape orientation */
  }
}
//终止查询通知
mql.removeListener(handleOrientationChange);
```

#### rem实践

rem是非常好用的一个属性，可以根据html来设定基准值，而且兼容性也很不错。

兼容 低端浏览器不出问题：

```css
html { font-size: 62.5%; }
body { font-size: 14px; font-size: 1.4rem; } /* =14px */
h1   { font-size: 24px; font-size: 2.4rem; } /* =24px */
```

#### 检查判断iPHone/iPod

```js
if((navigator.userAgent.match(/iPhone/i)) || (navigator.userAgent.match(/iPod/i))) {
　　if (document.cookie.indexOf("iphone_redirect=false") == -1) {
　　　　window.location = "http://m.example.com";
　　}
}
```

虽然Javascript是可以在水果设备上运行的，但是用户还是可以禁用。它也会造成客户端刷新和额外的数据传输，所以下面是服务器端侦测和转向：

```php
if(strstr($_SERVER['HTTP_USER_AGENT'],'iPhone') || strstr($_SERVER['HTTP_USER_AGENT'],'iPod')) {
　　header('Location: http://yoursite.com/iphone');
　　exit();
}
```

#### 阻止屏幕旋转时字体自动调整

```css
html, body, form, fieldset, p, div, h1, h2, h3, h4, h5, h6 {-webkit-text-size-adjust:none;}
```

#### 模拟:hover伪类

因为iPhone并没有鼠标指针，所以没有hover事件。那么CSS :hover伪类就没用了。但是iPhone有Touch事件，onTouchStart 类似 onMouseOver，onTouchEnd 类似 onMouseOut。所以我们可以用它来模拟hover。使用Javascript：

```js
var myLinks = document.getElementsByTagName('a');
for(var i = 0; i < myLinks.length; i++){
　　myLinks[i].addEventListener(’touchstart’, function(){this.className = “hover”;}, false);
　　myLinks[i].addEventListener(’touchend’, function(){this.className = “”;}, false);
}
```

然后用css增加hover效果：

```css
a:hover, a.hover { /* 你的hover效果 */ }
```

这样设计一个链接，感觉可以更像按钮。并且，这个模拟可以用在任何元素上。

##### 其他思路：

要让a链接的CSS active伪类生效，只需要给这个a链接的touch系列的任意事件touchstart/touchend绑定一个空的匿名方法即可hack成功

```HTML
<style>
a {
color: #000;
}
a:active {
color: #fff;
}
</style>
<a herf=”asdasd”>asdasd</a>
<script>
var a=document.getElementsByTagName(‘a’);
for(var i=0;i<a.length;i++){
a[i].addEventListener(‘touchstart’,function(){},false);
}
</script>
```

#### viewport宽度超过device-width宽度 后导致文字无故折行

[http://www.iunbug.com/archives/2013/04/23/798.html](http://www.iunbug.com/archives/2013/04/23/798.html)

#### 引导用户安装并打开APP

来自 [http://gallery.kissyui.com/redirectToNative/1.2/guide/index.html](http://gallery.kissyui.com/redirectToNative/1.2/guide/index.html)

kissy mobile 通过iframe src发送请求打开app自定义url scheme，如taobao://home（淘宝首页） 、etao://scan（一淘扫描）\); 如果安装了客户端则会直接唤起，直接唤起后，之前浏览器窗口（或者扫码工具的webview）推入后台； 如果在指定的时间内客户端没有被唤起，则js重定向到app下载地址。 大概实现代码如下

```js
goToNative:function(){

    if(!body) {
            setTimeout(function(){
                doc.body.appendChild(iframe);
            }, 0);
        } else {
            body.appendChild(iframe);
        }

setTimeout(function() {
            doc.body.removeChild(iframe);
            gotoDownload(startTime);//去下载，下载链接一般是itunes app store或者apk文件链接
            /**
             * 测试时间设置小于800ms时，在android下的UC浏览器会打开native app时并下载apk，
             * 测试android+UC下打开native的时间最好大于800ms;
             */
        }, 800);
}
```

需要注意的是 如果是android chrome 25版本以后，在iframe src不会发送请求， 原因如下：

[https://developers.google.com/chrome/mobile/docs/intents](https://developers.google.com/chrome/mobile/docs/intents)

通过location href使用intent机制拉起客户端可行并且当前页面不跳转。

```
window.location = 'intent://' + schemeUrl + '#Intent;scheme=' + scheme + ';package=' + self.package + ';end';
```

补充\[三清水\]\([http://js8.in/2013/12/16/ios使用schema协议调起app/\](http://js8.in/2013/12/16/ios使用schema协议调起app/%29\)

#### 消除transition闪屏

两个方法：使用css3动画的时尽量利用3D加速，从而使得动画变得流畅。动画过程中的动画闪白可以通过 backface-visibility 隐藏。

```css
-webkit-transform-style: preserve-3d;
/*设置内嵌的元素在 3D 空间如何呈现：保留 3D*/
-webkit-backface-visibility: hidden;
/*（设置进行转换的元素的背面在面对用户时是否可见：隐藏）*/
```

#### 测试是否支持svg图片

```js
document.implementation.hasFeature("http:// www.w3.org/TR/SVG11/feature#Image", "1.1")
```

#### 测试是否支持某CSS属性

`CSS.supports()`

The`CSS.supports()`static methods returns a[`Boolean`](https://developer.mozilla.org/en-US/docs/Web/API/Boolean)value indicating if the browser supports a given CSS feature, or not.

```js
boolValue = CSS.supports(propertyName, value);
boolValue = CSS.supports(supportCondition);
```

#### 常用webkit属性

##### -webkit-appearance:none

去除系统默认appearance的样式,常用于IOS下移除原生样式

##### -webkit-user-select: none;

禁止选中文本（如无文本选中需求，此为必选项）

##### -webkit-touch-callout: color;

当用户点击iOS的Safari浏览器中的链接或JavaScript的可点击的元素时，覆盖显示的高亮颜色。该属性可以只设置透明度。如果未设置透明度，iOS Safari使用默认的透明度。当透明度设为0，则会禁用此属性；当透明度设为1，元素在点击时不可见

##### -webkit-overflow-scrolling: touch;

属性控制元素在移动设备上是否使用滚动回弹效果.

##### -webkit-font-smoothing: antialiased; -moz-osx-font-smoothing: grayscale;

优化字体

##### -webkit-touch-callout: none !important;

当你触摸并按住触摸目标时候，禁止或显示系统默认菜单

##### -webkit-tap-highlight-color

点击出现背景色

#### 指定时间调用scroll/resize事件

由于绑定scroll事件或者resize会重复触发，导致浏览器崩溃，因为应该这样优化

正常的情况下类似这样

```js
$('div').on('scroll', function(){
//.….code
{});
```

而如果中间的code需要处理的东西多的话，fps就会下降影响程序顺滑度，而如果改成这样

```js
//可以分为两次，第一次调用是不存在scrollTimer的，所以会执行下面的；第二次的时候会先干掉第一次执行的；
$(window).on('scroll', function(){
    if($addMore.offset().top - $(window).scrollTop() < $(window).height()){ 
      if(scrollTimer){
        clearTimeout(scrollTimer)
      }
      scrollTimer = setTimeout(function(){
        $container.append($items).masonry('appended', $items, true);
      }, 400);
    }
  })
```

#### 强制GPU渲染

```css
a {-webkit-transform: translateZ(0); transform: translateZ(0);}
```

#### 文字过多自动省略

```css
.hiddenText {
    overflow: hidden;
    text-overflow: ellipsis;
    white-space: nowrap;
}
```

#### transitionend事件

`transitionend` 事件会在`css transition` 结束后触发. 当transition完成前移除transition时，比如移除css的`transition-property`属性，事件将不会被触发.如在`transition`完成前设置`display:none`，事件同样不会被触发

```js
/*
 * 在指定的元素上监听transitionend事件, 例如#slidingMenu
 * 然后指定一个函数, 例如 showMessage()
 */
function showMessage() {
    console.log('Transition 已完成');
}

var element = document.getElementById("slidingMenu");
element.addEventListener("transitionend", showMessage, false);
```

\[叶小钗 - transitionEnd小故事\]\([http://www.cnblogs.com/yexiaochai/p/3602303.html\](http://www.cnblogs.com/yexiaochai/p/3602303.html\)\)

#### 判断是否是微信打开1

```js
<script>
    function is_weixn(){  
      return true
      var ua = navigator.userAgent.toLowerCase();  
      if(ua.match(/MicroMessenger/i)=="micromessenger") {  
          return true;  
      } else {  
          return false;  
      }  
  }
  </script>
<script type="text/javascript" src="http://res.wx.qq.com/open/js/jweixin-1.0.0.js"></script>
<script>
    if(!is_weixn()){
      alert('请从微信打开连接');
    }else{
      $('body').show();
    }
  </script>
```

#### 判断是否是微信浏览器2

```js
function is_weixn(){
    var ua = navigator.userAgent.toLowerCase();
    if(ua.match(/MicroMessenger/i)=="micromessenger") {
        return true;
    } else {
        return false;
    }
}
```

#### 判断屏幕是否旋转

```js
function orientationChange() {
    switch(window.orientation) {
    　　case 0:
            alert("肖像模式 0,screen-width: " + screen.width + "; screen-height:" + screen.height);
            break;
    　　case -90:
            alert("左旋 -90,screen-width: " + screen.width + "; screen-height:" + screen.height);
            break;
    　　case 90:
            alert("右旋 90,screen-width: " + screen.width + "; screen-height:" + screen.height);
            break;
    　　case 180:
        　　alert("风景模式 180,screen-width: " + screen.width + "; screen-height:" + screen.height);
        　　break;
    };};
```

#### 页面视频小窗播放

在iOS上需要用到`webkit-playsinline playsinline`属性

```html
<video webkit-playsinline playsinline></video>
```



