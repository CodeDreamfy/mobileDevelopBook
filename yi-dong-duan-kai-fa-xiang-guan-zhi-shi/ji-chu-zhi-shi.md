#### meta标签

meta标签在开发APP时起到非常重要的作用

```html
<meta content="width=device-width; initial-scale=1.0; maximum-scale=1.0; user-scalable=0" name="viewport" />
<meta content="yes" name="apple-mobile-web-app-capable" />
<meta content="black" name="apple-mobile-web-app-status-bar-style" />
<meta content="telephone=no" name="format-detection" />
```

第一个meta标签表示：强制让文档的宽度与设备的宽度保持1:1，并且文档最大的宽度比例是1.0，且不允许用户点击屏幕放大浏览； 尤其要注意的是content里多个属性的设置一定要用分号+空格来隔开，如果不规范将不会起作用。

第二个meta标签是iphone设备中的safari私有meta标签，它表示：允许全屏模式浏览； 第三个meta标签也是iphone的私有标签，它指定的iphone中safari顶端的状态条的样式； 第四个meta标签表示：告诉设备忽略将页面中的数字识别为电话号码

在设置了initial-scale=1 之后，我们终于可以以1:1 的比例进行页面设计了。 关于viewport，还有一个很重要的概念是：iphone 的safari 浏览器完全没有滚动条，而且不是简单的“隐藏滚动条”， 是根本没有这个功能。iphone 的safari 浏览器实际上从一开始就完整显示了这个网页，然后用viewport 查看其中的一部分。 当你用手指拖动时，其实拖的不是页面，而是viewport。浏览器行为的改变不止是滚动条，交互事件也跟普通桌面不一样。

#### 移动端开发事件

##### 手势事件

* touchstart //当手指接触屏幕时触发
* touchmove //当手指已经接触屏幕并开始移动后触发
* touchend //当手指离开屏幕时触发
* touchcancel

##### 触摸事件

* gesturestart //当两个手指接触屏幕时触发
* gesturechange //当两个手指接触屏幕后开始移动时触发
* gestureend

##### 屏幕旋转事件

* oneorientationchange

##### 检测触摸屏幕的手指何时改变方向

* orientationchange

##### touch事件支持的相关属性

* touches
* targetTouches
* changedTouches
* clientX　　　　// X coordinate of touch relative to the viewport \(excludes scroll offset\)
* clientY　　　　// Y coordinate of touch relative to the viewport \(excludes scroll offset\)
* screenX　　　 // Relative to the screen
* screenY 　　 // Relative to the screen
* pageX　　 　　// Relative to the full page \(includes scrolling\)
* pageY　　　　 // Relative to the full page \(includes scrolling\)
* target　　　　 // Node the touch event originated from
* identifier　　 // An identifying number, unique to each touch event
* 屏幕旋转事件：onorientationchange



#### 页面描述

> 以下属性仅适用于iOS

```html
<link rel="apple-touch-icon-precomposed" href="http://www.xxx.com/App_icon_114.png" />
<link rel="apple-touch-icon-precomposed" sizes="72x72" href="http://www.xxx.com/App_icon_72.png" />
<link rel="apple-touch-icon-precomposed" sizes="114x114" href="http://www.xxx.com/App_icon_114.png" />
```

这个属性是当用户把连接保存到手机桌面时使用的图标，如果不设置，则会用网页的截图。有了这，就可以让你的网页像APP一样存在手机里了

```html
<link rel="apple-touch-startup-image" href="/img/startup.png" />
```

设置启动时界面显示的图片。如果不设置，启动画面就是白屏，图片像素就是手机全屏的像素

> 该路径需要注意的就是放到将网站的文档根目录下但不是服务器的文档的根目录。
>
> 官方规定启动界面的尺寸必须为320\*640（px），原本以为Retina屏幕可以支持双倍，但是不支持，图片显示不出来。

```html
<meta name="apple-mobile-web-app-status-bar-style" content="black-translucent" /
```

这个描述是表示打开的web app的最上面的时间、信号栏是黑色的，当然也可以设置其它参数

```html
<meta name="apple-mobile-web-app-capabl" content ="yes" />
<meta name="apple-mobile-web-app-status-bar-style" content="black" />
```

如果`content`设置为`yes`，Web应用程序以全屏模式运行;否则，它不会。默认行为是使用Safari显示Web内容。

可以使用`window.navigator.standalone`只读布尔JavaScript属性来确定网页是否以全屏模式显示。

`apple-mobile-web-app-status-bar-style`的`content`默认值为default\(白色\)，可以定为black\(黑色\)和black-translucent\(灰色半透明\)。

注意： 若值为”black-translucent”将会占据页面px位置，浮在页面上方\(会覆盖页面20px高度iphone4和itouch4的Retina屏幕为40px\)

```html
<meta name="apple-touch-fullscreen" content="yes" /> /* 全屏显示 */
```

以上iOS的meta属性可以参考\([https://developer.apple.com/library/content/documentation/AppleApplications/Reference/SafariHTMLRef/Articles/MetaTags.html\](https://developer.apple.com/library/content/documentation/AppleApplications/Reference/SafariHTMLRef/Articles/MetaTags.html%29\)

