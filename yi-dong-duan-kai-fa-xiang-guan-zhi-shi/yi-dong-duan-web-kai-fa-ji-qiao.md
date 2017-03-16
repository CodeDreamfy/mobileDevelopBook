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

```css
body {
    -webkit-overflow-scrolling: touch;
}
```

用iphone或ipad浏览很长的网页滚动时的滑动效果很不错吧？不过如果是一个div，然后设置`height:200px;overflow:auto;`的话，可以滚动但是完全没有那滑动效果，很郁闷吧？

我看到很多网站为了实现这一效果，用了第三方类库，最常用的是iscroll（包括新浪手机页，百度等） 我一开始也使用，不过自从用了`-webkit-overflow-scrolling: touch;`样式后，就完全可以抛弃第三方类库了，把它加在body{}区域，所有的overflow需要滚动的都可以生效了。



