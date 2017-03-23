### 前言

```html
<meta name="viewport" content="width=device-width, initial-scale=1, minimum-scale=1, maximum-scale=1, user-scalable=no">
```

上面这行代码我们在写移动端app的时候会经常用到，但是除了用到我们对这个属性一无所知。

#### 基本定义

`viewport`在字典里面意思是视口， 这个meta标签是由苹果发明的，后来慢慢被其他生产商接受，就开始流行起来了

> 以前移动端浏览器通常有一个比屏幕更宽的视口（窗口）去渲染页面，从而我们不需要去将所有的页面压缩到屏幕中，用户只需要通过平移和缩放来浏览不同区域就可以了。Mobile Safari引入了“viewport元标签”来让web开发者更好的控制视口的尺寸及比例。如今很多浏览器都支持这一标签，虽然它不属于任何标准.

viewport有几个属性需要了解

> width: 控制viewport的大小，可以指定一个值，比如375，或者给他一个特殊的值，如：device-width，device-width为设备的宽度，屏幕宽度（单位为缩放为100%时css的像素）
>
> height：与width相对应，指定viewport高度
>
> initial-scale：初始缩放比例，页面第一次load的缩放比例
>
> maximum-scale：允许用户缩放的最大比例
>
> minimum-scale：允许用户缩放到的最小比例
>
> user-scalable；是否允许用户缩放

meta的viewport的几种写法：

```html
<meta name="viewport" content="width=device-width, initial-scale=1, minimum-scale=1, maximum-scale=1, user-scalable=yes">
```

```html
<meta name="viewport" content="width=device-width, initial-scale=1, user-scalable=no">
```

既然已经禁止用户进行缩放了，那么就不存在设置范围了。

