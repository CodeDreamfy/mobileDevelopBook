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



