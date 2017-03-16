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

#### webkit CSS

#### 页面描述



