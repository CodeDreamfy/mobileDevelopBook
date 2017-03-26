#### 移动端是如何做到适应屏幕的呢？

在讲rem屏幕适配之前，先说一下一般做移动端适配的方法，一般可以分为：

**1** 简单一点的页面，一般高度直接设置成固定值，宽度一般撑满整个屏幕。

**2** 稍复杂一些的是利用百分比设置元素的大小来进行适配，或者利用flex等css去设置一些需要定制的宽度。

**3** 再复杂一些的响应式页面，需要利用css3的media query属性来进行适配，大致思路是根据屏幕不同大小，来设置对应的css样式。

我们知道rem是以根节点字体来计算的，在没有赋值情况下，也就是默认情况下1rem是等于1em的；

那么当我们改变根节点默认值的时候，这个时候rem换算出来的值也就不一样了。

那么当我们把rem当度量单位用的时候呢？

lib.flexible.js

```js
!function(doc, win){
    var timer,docEle = doc.docuementElement,
    evt = "onorientationchange" in window ? "orientationchange" : "resize";
    setFontSize = function(){
        var width = docEle.innerWidth;
        var base = 750 / 10;
        width && (docEle.style.fontSize = (width/750) * base +'px')
        win.fontSize = (width/750) * base;
    },
    win.addEventListener(evt, function(){
        clearTimer(timer);
        timer = setInterval(setFontSize,200)
    } , false)
    doc.addEventListent('DOMContentLoaded', setFontSize, false);
    setFontSize()
    
}(document,window)
```



