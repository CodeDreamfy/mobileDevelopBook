##### lib.flexible

我们说一说这个库的基本思路，其实和我们刚才提到的思路是一致的

这个东西的原理是通过动态的改变html根节点的fontSize和动态的设置meta标签

```js
var metaEl = doc.createElement('meta');
var scale = isRetina ? 0.5:1;
metaEl.setAttribute('name', 'viewport');
metaEl.setAttribute('content', 'initial-scale=' + scale + ', maximum-scale=' + scale + ', minimum-scale=' + scale + ', user-scalable=no');
if (docEl.firstElementChild) {
    document.documentElement.firstElementChild.appendChild(metaEl);
} else {
    var wrap = doc.createElement('div');
    wrap.appendChild(metaEl);
    documen.write(wrap.innerHTML);
}
```

```js
if (!dpr && !scale) {
    var isAndroid = win.navigator.appVersion.match(/android/gi);
    var isIPhone = win.navigator.appVersion.match(/iphone/gi);
    var devicePixelRatio = win.devicePixelRatio;
    if (isIPhone) {
        // iOS下，对于2和3的屏，用2倍的方案，其余的用1倍方案
        if (devicePixelRatio >= 3 && (!dpr || dpr >= 3)) {                
            dpr = 3;
        } else if (devicePixelRatio >= 2 && (!dpr || dpr >= 2)){
            dpr = 2;
        } else {
            dpr = 1;
        }
    } else {
        // 其他设备下，仍旧使用1倍的方案
        dpr = 1;
    }
    scale = 1 / dpr;
}
```

flexible会将视觉稿分成100份（主要为了以后更好的兼容vw与vh），而每一份被称为单位a，同时约定10a = 1rem，即：

> 1a = 7.5px;
>
> 1rem = 10a = 75px;

只需要对视觉稿的px值除以rem基准值即可。

#### 怎么样快速计算呢？

postcss -&gt; px2rem

less，sass 函数话处理

```less
@function px2rem($px){
    $rem: 37.5px;
    @return ($px/$rem)+ rem;
}
```

对于字体处理不建议使用rem，我们可以通过依据dpr去做判断



其实H5适配的方案有很多种，网上有关于这方面的教程也非常的多。不管哪种方法，都有其自己的优势和劣势

