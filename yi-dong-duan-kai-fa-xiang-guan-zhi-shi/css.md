#### css3

手机浏览器对于CSS3的支持，总体上支持的比较好，不过由于Android的碎片化，手机碎片化以及IOS的各种版本，在很多地方需要谨慎操作。

如果说起手机Web的CSS，就需要说起-webkit-的前缀的CSS的属性。这些前缀是专门为了webkit核心的浏览器设置的属性，可能很多-webkit-的属性，已经成功通用的属性了，不需要再加前缀。不过为了兼容低版本的浏览器，在设置的时候，还是需要加上-webkit-前缀

CSS3有很多类型，大致可以分为以下类型，布局类型、渲染类型、选择器类型、动画类型

目前解决办法是使用插件，比如说autoprefix、但是发展到现在大部分的动画都支持了，如果不确定我们可以去网站上查相关属性看支持程度：www.caniuse.com

#### css Reset

在讲以上布局之前，需要说一下关于CSS的reset的问题。关于这个问题，需要追溯到HTML4的时代，在那个时候，由于PC有各种游览器、各种标准、造成对于HTML的各个标签所带的默认样式的不同，结果造成要在各个平台统一一个样式会非常难。因此出现了reset，所谓reset的意思是把所有HTML的标签的默认样式进行重置，这样方便在所有平台进行页面制作开发。跨入无线Web的时代之后，reset是否还要存在，业界有着非常多的讨论。主要分为两派：reset派和normalize派。reset派认为就算是到了移动时代，还是有各种碎片化的问题，需要reset，而normalize的一派认为，到了无线Web，很多规范已经收到了很多厂商的支持，最出名的要属Google和苹果，因此不需要进行reset，只需要将那些标签进行统一化，即可。

因此，在市面上做移动开发，有两种CSS模式，reset模式和normalize的模式。个人认为，两者没有绝对的好与坏。主要看这个项目的特性。

* reset模式 适用于严格要求所有的平台必须完全按照统一的一个形态的进行开发的项目，一般而言，对于webapp的类型的项目，可能使用reset更加适合。reset模式也适合UI控件的编写，因为UI控件有着严格的标准，使用reset，可以更加好的进行精确控制。
* normalize模式 此模式适用于Web特性的网站，所谓Web特性的网站，是指那种适合各种平台，并且在不同的平台需要体验各平台自己特性的网站，不需要强制要求所有平台进行统一。

不过就大多数项目而言，一般产品经理和交互都会要求在各个平台需要有个统一的产品表现，因此在实际项目里，reset可能用的会更多一点。

#### flex

布局目前推荐使用flex进行布局。
