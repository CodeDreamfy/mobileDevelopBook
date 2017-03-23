#### 点

最初，所有的图像的坐标都是用点确定的。点是绝对单位，他们只在数学的坐标空间有意义。最初的iPhone上，点和实际屏幕的像素是完全一致的，但是后面不再是这样了。

#### 渲染像素

以点为基础的图像渲染成为像素，这个过程就是光栅化（rasterization）

点坐标乘以一定比例系数，得到相应的像素坐标。更高的比例系数可以得到更好的细节呈现。

典型的比例系数有1x、2x和3x

#### 物理像素

iPhone 6 Plus的屏幕像素分辨率比之前步骤渲染的图像分辨率低。

在图像显示在屏幕之前，图像必须重新调整大小到更低的像素分辨率。

#### 物理设备

最后一步是将计算的像素显示在物理屏幕上，每一个屏幕都有一个每英寸像素（PPI）的特性。这个数字告诉你一英寸显示多少像素，也就是一像素在真实世界里显示的大小。

#### 一根线的渲染

为了说明多种设备的不同渲染情况，我们比较一个一像素宽的线是怎么样渲染的：

* 最初的iPhone - 没有高清屏，比例系数是1
* iPhone 5 - 有高清屏幕，比例系数是2
* iPhone 6 Plus - 超高清屏，比例系数是3，并且图像会先渲染为2208×1242像素然后缩小为1920×1080像素

缩小的比例是1920/2208 = 1080/1242 = 20/23。意味着最初渲染的每23像素会分布到20物理像素中，图像会缩小为原尺寸的87%。


