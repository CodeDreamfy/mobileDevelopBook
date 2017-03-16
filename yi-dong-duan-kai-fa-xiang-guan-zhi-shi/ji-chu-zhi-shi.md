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

##### 判断屏幕是否旋转

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

##### 判断是否是微信浏览器

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

#### webkit CSS

主要

#### 页面描述



