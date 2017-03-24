#### 移动端是如何做到适应屏幕的呢？

首先得了解清楚viewport的概念，前面已经介绍了，这里就不多说。

#### 第一种

在没有rem的年代，要适配手机主要是通过写固定宽度来实现的，比如给device-width设置固定宽度，然后通过媒体查询，依据屏幕宽度来判断是iPhone4，5还是6，6p，最开始是以640px的宽度来设计的，因此参照的是4s

```css
@media screen and (min-width:320px) and (max-width:375px)  //前提是设置了meta标签的viewport
```

#### 刀耕火种的年代

那个时候我们的宽度都是写死的，比如

```html
<meta name="viewport" content="width=640">
```

```css
.wrapper { width 640px; margin: 0 auto; overflow: hidden;}
```

为什么用640呢？那个时候是依据iPhone4s为准去适配的。

#### 铁犁牛耕的年代

这个时候已经有了css3，那么就好办了，我们可以结合css3的媒体查询来做，通过media query属性来进行适配，思路就是依据屏幕的高度来进行设置对应的css，为什么是高度呢，因为在我们看来，iPhone4，4s，5，5s，6，6s宽度都是相同的。

#### 现代文明

来到现代文明，我们能用的更多了，我们可以使用rem了，可以使用flex了，通过flex布局，然后rem与媒体查询或者一些js结合就可以做到适配屏幕了。

我们再来回顾一下rem的概念

> **rem**
>
> 代表相对于根元素的font-size大小（html）。当用在根元素font-size上面时，他代表了它的初始值（默认初始值是html的默认的font-size大小，比如当未在根元素上面设置font-size大小的时候，此时1rem == 1em，当设置font-szie=2rem的时候，就使得页面中1rem的大小相当于html的根字体默认大小的2倍）

##### 有了这个思路就好办了，只要我们动态的设置根节点字体的大小就可以做到适配屏幕了，于是就出现一些衍生的辅助适配的工具

比如lib

#### 近地未来



