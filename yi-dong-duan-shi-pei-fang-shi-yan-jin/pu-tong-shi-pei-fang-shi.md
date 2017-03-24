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

