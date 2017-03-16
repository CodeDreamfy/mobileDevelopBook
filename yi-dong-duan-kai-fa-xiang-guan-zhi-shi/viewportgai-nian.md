### meta中的viewport

> 首先声明viewport标签直到现在也不属于任何标准

#### 背景

以前移动端浏览器通常有一个比屏幕更宽的视口（窗口）去渲染页面，从而我们不需要去将所有的页面压缩到屏幕中，用户只需要通过平移和缩放来浏览不同区域就可以了。

Mobile Safari引入了“viewport元标签”来让web开发者更好的控制视口的尺寸及比例。如今很多浏览器都支持这一标签，虽然它不属于任何标准。

一个典型的meta标签如下：

```html
<meta name="viewport" content="width=device-width, initial-scale=1, maximum-scale=1">
```

width控制视口的宽度。可以像`width=600`这样设为确切的像素值， 或者设为`device-width` 这一特殊值来指代比例为100%时屏幕宽度的css像素值\(相应的有`height`及`device-height`属性，可能包涵基于视口高度调整大小及位置元素的页面有用\)

`initial-scale`属性控制页面最初加载时的缩放等级。`maximun-scale`、`minimun-scale`及`user-scalabale`属性控制允许用户以什么样的方式放大或缩小页面。

