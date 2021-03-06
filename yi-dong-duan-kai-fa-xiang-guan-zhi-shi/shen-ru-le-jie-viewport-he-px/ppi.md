#### PPI，每英寸像素 / 像素密度

表示打印图像或者显示器单位面积的像素数量的指数。一般用来衡量屏幕的精细程度。通常情况下，每英寸像素值越高，屏幕能显示的图像也就越精细。

研究表明，人肉眼能够分辨的最高像素点密度是300PPI，苹果公司在2010年推出iPhone4手机的时候提出超过300ppi的屏幕被称为Retina显示屏。

电脑和手机屏幕每英寸像素值取决于尺寸和分辨率，通常指的就是每英寸上的像素点。

同一台显示器如果分辨率设置的不同，像素点也不同。分辨率越高，每英寸的像素值也越大。

这个就类似于我们的电脑显示器，同一个电脑显示器，当分辨率设置1920×1080的时候，图标文字什么的看起来小一些，但是如果设置成1366×768的时候就看起来很大了。这一点可以侧面证明分辨率越低，每英寸的像素值也越小。

![](/assets/200px-Square_200x200.svg.png)

> 上图是200×200像素的图片，如果浏览器的显示比例为100%，显示的图像越小，代表显示器的每英寸像素值越高（即ppi越高）

一台显示器的像素密度是由显示单元之间的点决定的。

ppi的计算方式是： dp / di

dp屏幕对角线分辨率 = 勾股定理得到（屏幕横向分辨率 × 屏幕纵向分辨率）

di是屏幕对角线的长度（英寸）

计算像素密度公式：

![](/assets/1441638622_1436653066_8976_imageAddr.jpg)

勾股定理算出对角线的分辨率：√\(1920²+1080²\)≈2203px

对角线分辨率除以屏幕尺寸：2203/5≈440dpi

##### 基于每英寸像素值的屏幕分级

根据屏幕每英寸像素值不同，Android开发者将平板电脑和手机分成五类：

| 名称 | 显示等级 | 每英寸像素值 |
| :---: | :---: | :---: |
| LDPI | 低等像素密度 | 每英寸120像素 |
| MDPI | 中等像素密度 | 每英寸160像素 |
| HDPI | 高等像素密度 | 每英寸180像素 |
| XHDPI | 极高像素密度 | 每英寸320像素 |
| XXHDPI | 超高像素密度 | 每英寸480像素 |

最后XHDPI指具有类似于苹果Retina显示屏效果的屏幕，下图为iPhone 3GS与iPhone 4显示效果比：

![](/assets/400px-Non-Retina_Display.jpg)![](/assets/400px-Retina_Display.jpg)

左图为iPhone 3GS（160每英寸，MDPI）                                      右图为iPhone 4（326每英寸像素，XDPI）

