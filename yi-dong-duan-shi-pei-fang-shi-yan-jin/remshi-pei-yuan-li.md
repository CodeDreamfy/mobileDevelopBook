我们再来回顾一下rem的概念

> **rem**
>
> 代表相对于根元素的font-size大小（html）。当用在根元素font-size上面时，他代表了它的初始值（默认初始值是html的默认的font-size大小，比如当未在根元素上面设置font-size大小的时候，此时1rem == 1em，当设置font-szie=2rem的时候，就使得页面中1rem的大小相当于html的根字体默认大小的2倍）

##### 我们将rem作为css的度量单位来使用。

依照某特定宽度设定 rem 值（即 html 的_font-size_），页面任何需要弹性适配的元素，尺寸均换算为 rem 进行布局；当页面渲染时，根据页面有效宽度进行计算，调整 rem 的大小，动态缩放以达到适配的效果。利用该方案，还可以根据_devicePixelRatio_设定_initial-scale_来放大 viewport，使页面按照物理像素渲染，提升清晰度。

##### 优点：

* 清晰度高，能到到物理像素的清晰度
* 能解决dpr引起的1px问题
* 向后兼容较好，即使屏幕分辨率增加，ppi增加该方案依然可以适用

缺点：

* 适配js需要尽早的引进来，减少（避免）viewport重绘
* 需要预编译库进行单位转换

webkit现在默认字体大小是16px

当我们直接给div设置宽高的时候

```css
.box { 
    width: 10rem;
    height: 10rem;
}
```

这个时候其实最后的计算结果是

```css
.box {
    width: 160px;
    height: 160px;
}
```

如果将html根元素的默认值font-size修改一下的话，那么这里div的宽高也会改变。

#### rem数值计算

如果利用rem来设置css的值的时候，需要通过一层计算才能得到，比如需要设置一个长宽为100px的div，那么就需要计算出100px对应的rem值是100/16=6.25rem了；在写的时候频繁的计算就比较繁琐了。

所以，为了方便起见，对于没有使用工程化的项目：

直接将根节点字体设置为100px，这样在写单位的时候，直接将数值除以100加上rem的单位就可以了，然后再配合上媒体查询。

对于使用了工程化的项目：

第一种方式是利用less，sass的函数来解决：

```sass
@function px2rem($px){
    $rem: 37.5px;
    @return ($px/$rem)+ rem;
}

//使用方式：width: px2rem(90px);
```

##### rem基准值计算

关于rem基准值，也就是37.5其实是根据我们拿到的视觉稿来决定的。主要有以下原因：

1. 由于我们写出的页面要求在不同屏幕设备上运行
2. 写样式的时候必须先以一个确定的屏幕来进行参考，这个就是我们的视觉稿来定
3. 假如我们拿到的视觉稿是以iPhone6的屏幕为基准设计的
4. iPhone6的屏幕大小css像素是375px

> rem = window.innerWidth / 10

这里为什么要除以10，这个值只是为了方便计算，主要是不想要rem的font-size太大，当然可以选择不除。

iPhone 3gs： 320px / 10 = 32px；

iPhone 4/4s/5/5s：320 / 10 = 32px；

iPhone 6/6s/7： 375 / 10 = 37.5px；

iPhone 6p/6sp/7p： 414 / 10 = 41.4px；

然后动态的设置html的font-size就可以了，

如何动态的设置呢？

1 利用css的media query来设置

```css
@media (min-device-width : 375px) and (max-device-width : 667px) and (-webkit-min-device-pixel-ratio : 2){
      html{font-size: 37.5px;}
}
```

2 利用js动态的设置，根据我们之前算出的基准值，可以动态的算出当前屏幕所适配的font-size

```js
document.getElementsByTagName('html')[0].style.fontSize = window.innerWidth / 10 + 'px';
```

##### rem适配进阶

我们知道，一般我们获取到的视觉稿大部分是iphone6的，所以我们看到的尺寸一般是双倍大小的，在使用rem之前，我们一般会自觉的将标注/2，其实这也并无道理，但是当我们配合rem使用时，完全可以按照视觉稿上的尺寸来设置。

1. 设计给的稿子双倍的原因是iphone6这种屏幕属于高清屏，所以显示的像素较为清晰，不用重复提供多倍图的图片了。
2. 以前手机的dpr是1，现在智能手机越来越高级，大部分都是1080以上分辨率，我们可以通过window.devicePixelRatio获取当前设备的dpr，然后算出设备的分辨率
3. 拿到dpr后，我们可以动态的设置viewport meta头部里面的缩放了

```
var e = window.innerWidth;
// $('html').css({
//     fontSize: e/10
// })
// console.log(e)
var dpr = window.devicePixelRatio;
var vpMeta = document.createElement("meta");
vpMeta.setAttribute("name", "viewport");
// var meta = document.getElementsByTagName('meta')[0];
vpMeta.setAttribute('content', 'initial-scale=' + 1/dpr + ', maximum-scale=' + 1/dpr + ', minimum-scale=' + 1/dpr + ', user-scalable=no');
document.documentElement.firstElementChild.appendChild(vpMeta)
```

使用缩放的这种方式解决了一些问题：

1. 图片高清问题
2. border 1px问题



