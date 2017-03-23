当我们加上meta的viewport标签后，出现了神奇的一幕：

viewport加之前与加之后的对比

![](/assets/view1.jpg)![](/assets/view2.jpg)

可以发现，加上meta的viewport标签后window.innerWidth由980变成了375，在iPhone6/7上发现，即使viewport将视口变为了375，而我们设置的box的宽度是100，在加上标签后也看起来占据了差不多1/3的位置了。

棘手的问题

device-width与meta中的width=device-width标签都可以使用设备像素，而不是css像素，因为他声明了网页的上下文，而不是内部css的变化

