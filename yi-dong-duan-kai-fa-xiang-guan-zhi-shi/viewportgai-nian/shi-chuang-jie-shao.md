viewport虽然只是一个单词，但是包涵了两个视口，分为：视觉窗口、布局窗口

几个属性概念

> `screen.width`：返回屏幕的宽度
>
> `window.innerWidth`：浏览器视口（viewport）（像素）vw单位基于适口的大小来确定的
>
> `window.outerWidth`：获取浏览器窗口外部的宽度。表示整个浏览器窗口的宽度
>
> `HTMLElement.offsetWidth`：返回一个元素的布局宽度
>
> `Element.clientWidth`：返回元素内部宽度

#### 视觉窗口

**就是设备的屏幕区域，换句话说就是用户通过屏幕所看到的页面内容**。但是对应的并不是指屏幕的物理像素，而是css像素。并且他所包含的css像素的数量随着用户缩放或者旋转屏幕而有所改变

> 可以通过`window.innerWidth`来获取视窗在缩放不同情况下的对应的宽和高

![](/assets/未标题-1.jpg)

#### 布局窗口

**布局视窗指的不是屏幕区域，而是为了解决pc端网站在移动端显示不佳的一个解决方案**。布局视窗通常比设备屏幕宽的多，一般为980px。在safari上面布局宽度为980，Opera中布局视窗宽为850px等

> 可以通过`document.documentElement.clientWidth`来获取布局视窗的宽度

![](/assets/未标题-2.jpg)

!注意：布局视窗的宽高值是在页面没有添加viewport时所获得的值。如果给页面添加了viewport，并且设置了width=device-width时，通过上面代码获得的值就不是布局视窗的默认值了。

