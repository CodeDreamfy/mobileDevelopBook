> 刀耕火种的年代

#### 固定高度，宽度自适应

viewport meta 设置成 width=device-width，垂直方向的高度和间距使用定值，水平方向混合使用定值和百分百或利用弹性布局，最终达到“当手机屏幕变化时，横向拉伸或者填充空白的效果”，图片元素根据容器情况，使用定值或者background-size缩放

#### 要点：

* 以小宽度作为参照是因为如果布局满足了小宽度的摆放，当屏幕变宽时，简单的填充空白就可以了；而如果反过来就可能造成“挤坏了”，考虑 header 区域，左测 logo 右测横向 nav 的情况。
* 需要小宽度的布局，又需要大宽度的图像，这是一个矛盾点。
* 320px 过于窄小，不利于页面的设计；只能设计横向拉伸的元素布局，存在很多局限性。
* 兼容性较好。

实现比较简单，样式中的尺寸都按照视觉稿二分之一大小设置

#### 固定宽度，viewport缩放

##### 优点：

* **开发简单**
     缩放交给浏览器，完全按视觉稿切图。
* **还原精准**
     绝对等比例缩放，可以精准还原视觉稿（不考虑清晰度的情况下）。
* **测试方便**
     在PC端即可完成大部分测试，手机端只需酌情调整一些细节（比如图标、字体混合排列时，因为字体不同造成的对齐问题）。

##### 存在的问题：

* **像素丢失**

对于一些分辨率较低的手机，可能设备像素还未达到指定的 viewport 宽度，此时屏幕的渲染可能就不准确了。比较常见的是边框“消失”了，不过随着手机硬件的更新，这个问题会越来越少的。

* **缩放失效**

某些安卓机不能正常的根据 meta 标签中width的值来缩放 viewport，需要配合initial-scale。

* _**文本折行**_

存在于缩放失效的机型中，某些手机为了便于文本的阅读，在文本到达 viewport 边缘（非元素容器的边缘）时即进行折行，而当 viewport 宽度被修正后，浏览器并没有正确的重绘，所以就发现文本没有占满整行。一些常用的段落性文本标签会存在该问题。

缩放失效问题需通过 js 动态设定_initial-scale_。

