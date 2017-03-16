##### 就目前而言，大多数移动设备使用两个主要操作系统之一：Google开发的Android（62.4%）与苹果开发的iOS（37%）

随着智能手机的兴起，显然我们喜欢的应用程序基本都基于Android与iOS，这个基本不会改变，因此要在两个操作系统上面开发目前主要有几种种方式：

* Native App
* web app
* Hybrid
* React Native / Weex
* PWA

### Native App（原生应用）

我们常用的微信，支付宝，Uber，网易云音乐等等都是原生app实现的，不管是android还是iOS两个操作系统都提供了供开发者使用的开发工具，界面元素与标准化的SDK，对于专业人员来说相对更容易开发本机应用程序。

用这种方式开发有很多好处：

* 为用户提供了最快、最可靠和最好的体验
* 可以利用更广泛的功能，包括：相机、麦克风、指南针、加速度计和滑动手势等
* 随时推送通知，在每次发布更新后或需要提示用户注意时提醒用户。这是一种主要的参与方式，有机会不断给用户带来更多
* 提供了更好的离线体验等

总的来说本地程序为用户带来了愉悦的应用程序体验。

但其缺点也很明显：

* 不同设备得分别开发，意味着开发了iOS的程序无法在Android下运行。有几个平台就得需要对应的开发人员开发维护。
* 不同平台开发意味着需要的人力成本与资金更多
* 必须符合不同系统APP上架的要求与标准（近期Apple警告开发者关于JSPATH相关js调用问题的事件）

当然，如果你的预算充足，那么原生应用程序是最理想的选择，他提供了最好的用户体验。

### Web App（网页应用）

从最早的WAP方式与GPRS2.0开始上网我们就已经接触到了web app了，通俗说就是移动端的网页版，比如腾讯新闻网页版，百度贴吧，类似UC的头条等等。主要生存在浏览器中，宿主是浏览器不是操作系统。

这种方式开发因为简单优势和不足很明显：

* 只需要一处开发，只需要适配好不同的手机屏幕，基本没问题
* 成本低，易于宣传推广活动应用
* 过于简单，导致功能方面有限，无法调用到系统的一些特性，比如上面提到的摄像头，相机等，
* 相对原生app来说体验很差，尤其是在离线情况下无法使用

### Hybrid App（混合应用）

通过介绍上面两种开发方式后，就有了目前这种基于原生APP内部内嵌页面的新思路，这种开发在一定程度上降低了开发成本，在混合应用里面有两个玩家：Phonegap/Cordova和Appcelerator Titanium。使用这两种工具，可以将本地创建的HTML/CSS/Javascript本地文件，通过Cordova将他们包装到移动应用中。

这种方式的基本思路是伪造一个浏览器的apk原生程序，把地址写死，然后里面运行一个webapp，里面是UI WebView，而不是（safari或chrome）体验度比webapp好一些。

* 对多平台使用一套基础代码
* 只需要一处开发，依据平台推送不同端的APP客户端
* 减少开发时间和成本
* 高级的离线特性
* 可以调用系统底层的的照相机、传感器、通讯录等
* 开发人员可以使用现有的网页技术

缺点：

* 某些特定的app性能问题（依赖于复杂的原生功能或繁重的果冻动画的app，比如3d游戏）
* 为模拟native app的ui和感官增加了时间和精力
* 如果app体验不够原生化，有被苹果拒绝的风险
* PhoneGap程序的加载和UI接口的反应都比本地的程序慢

> ##### PhoneGap
>
> PhoneGap是一款开发源代码的移动设备开发框架，旨在让开发者使用[H](https://zh.wikipedia.org/wiki/HTML)TML、CSS、Javascript等Web APIs开发跨平台的移动设备应用程序。
>
> PhoneGap是一个行动设备的[API](https://zh.wikipedia.org/wiki/API)接口集，利用JavaScript访问这些接口可以调用诸如摄影机、罗盘等硬件系统资源。配合上一些基于[HTML5](https://zh.wikipedia.org/wiki/HTML5)、[CSS3](https://zh.wikipedia.org/wiki/CSS3)技术的[UI](https://zh.wikipedia.org/wiki/UI)框架，如jQuery Mobile、Dojo Mobile或Sencha Touch，开发者得以快速地开发跨平台App而不需要编写任何的原生代码。[\[11\]](https://zh.wikipedia.org/wiki/Adobe_PhoneGap#cite_note-11)
>
> 注意到因为PhoneGap本身仍是一个原生程序，为App打包时依然需要用到这些系统平台的SDK。
>
> ##### Apache Cordova
>
> 2011年10月4日PhoneGap代码贡献给了Apache软件基金会，但保留了PhoneGap的商标版权，并命名为Apache Callback，后来改名为Apache Cordova。
>
> Cordova提供了一组设备相关的API，通过这组API，移动应用能够以JavaScript访问原生的设备功能，如摄像头、麦克风等。
>
> Cordova还提供了一组统一的JavaScript类库，以及为这些类库所用的设备相关的原生后台代码。 Cordova支持如下移动操作系统：iOS, Android,ubuntu phone os, Blackberry, Windows Phone, Palm WebOS, Bada 和 Symbian
>
> ##### Phonegap Build
>
> Phonegap Build是一个在线打包工具，使用cordova写好的项目给Phonegap Build，Phonegap Build就会在线打包成App，目前大家所说的Phonegap，其实指的都是cordova。Phonegap Build，（[iPhone, Android SDK service](https://link.zhihu.com/?target=http%3A//html.adobe.com/edge/phonegap-build/)）和cordova（[Apache Cordova](https://link.zhihu.com/?target=http%3A//cordova.apache.org/)）的合体

##### 



