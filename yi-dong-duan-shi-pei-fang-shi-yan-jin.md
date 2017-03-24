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
<head>
    <meta name="viewport" content="width=640">
</head>
```

```css
.wrapper { width 640px; margin: 0 auto; overflow: hidden;}
```

为什么用640呢？那个时候是依据iPhone4s为准去适配的。

#### 铁犁牛耕的年代



#### 现代文明



#### 近地未来











