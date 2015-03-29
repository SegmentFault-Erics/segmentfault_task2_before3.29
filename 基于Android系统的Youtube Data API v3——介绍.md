### 基于Android系统的Youtube Data API v3——介绍 ###

本文将一步步讲解如何在Android应用程序和其它平台上使用YouTube Data API V3接收YouTube视频信息。基于Android系统的YouTube Data API V3的帖子——在Isaac RF Blog（http://isaacrf.com）中第一次介绍。

### 首先第一件事情... ###

如果你之前开发过app，并且需要从YouTube获取视频信息，你可能会发现使用[YouTube Data API V3](https://developers.google.com/youtube/v3/?hl=en)并非如此简单。

为了能方便使用这个API，我将撰写一系列的基础文章，这样就可以理解如何使用并且马上可以制作自己的app，从这个简单介绍的帖子开始吧。

### 什么是Youtube Data API v3? ###

![](http://isaacrf.com/wp-content/uploads/2015/03/youtube.png)

YouTube提供了一个公共URL（[https://www.googleapis.com/youtube/v3](https://www.googleapis.com/youtube/v3)），称为Data API，因此可以从YouTube上读取应用程序、网站等公开信息（也可以读/写私人信息，首先登入[OAuth System](http://en.wikipedia.org/wiki/OAuth)），同时，API是基于Android系统（或者其它操作系统），可以使你毫不费力的在你app上生成视频、预览图像、布局组件等。

分析早期版本的Data API，为了恢复所需的特定信息，而不是所有的频道/视频数据，v3已经完成重组，这样避免了YouTube资源的大量损耗和时间浪费来，等待所有数据恢复。

与YouTube Data API v3交流的基本方法是公共URL上的[HTTP查询](http://en.wikipedia.org/wiki/Hypertext_Transfer_Protocol)。谷歌还提供一个Youtube API浏览器，你可以测试查询Data API上你想要接收的信息：[https://developers.google.com/apis-explorer/#p/youtube/v3 /](https://developers.google.com/apis-explorer/#p/youtube/v3/)

![](http://isaacrf.com/wp-content/uploads/2015/03/HTTP-Request.png)

在这里我们面临问题是Android API不会试图去恢复信息，而且也不公开直接访问Data API的方法，所以我们通过发送不同的GET参数手动执行URL的HTTP查询（参见维基百科上查询字符串的文章理解URL参数），这取决于我们想要获取的信息，这个过程并不简单，需要我们对我们所用的平台/语言有一定的了解。。

### 结束之前，给一个简单的例子 ###

我也不再多过多介绍，让我们来看看一个来自谷歌的小例子，它是用Google的API浏览器

如果我们访问下面URL，点击执行按钮，我们可以从[Murata Shinya's YouTube channel](https://www.youtube.com/user/MurataShinya)获得基本数据，请花点时间看看我是如何填写表中的参数，数据恢复将非常有用，因此我们可以得到，例如，该通道的视频列表：

[https://developers.google.com/apis-explorer/#p/youtube/v3/youtube.channels.list?part=contentDetails&forUsername=muratashinya&_h=2&](https://developers.google.com/apis-explorer/#p/youtube/v3/youtube.channels.list?part=contentDetails&forUsername=muratashinya&_h=2&)

你用手动HTTP查询来获取信息的实际URL是这样的:

[https://www.googleapis.com/youtube/v3/channels?part=contentDetails&forUsername=muratashinya&key={YOUR_API_KEY}](https://www.googleapis.com/youtube/v3/channels?part=contentDetails&forUsername=muratashinya&key={YOUR_API_KEY})

让我们来简单分析一下上面URL中使用的参数：

**“part=contentDetails”**：我们要检索的指定“piece”信息，“contentDetails”是参数的详细信息，我们用其它选项如“id”（通道ID），snippet（标题和描述），以及其它“statistics”，“topicDetails”，或“invideoPromotion”来填补部分参数。

**“forUsername=muratashinya”**：用户/信道的名称，我们即将接收的部分参数信息。如果我们有信道ID而不是用户名称，应该在id参数中指定而不是在用户名称中。

**“key={YOUR_API_KEY}”**：填写来自谷歌API控制台的参数API的密钥，（我们将在接下来的文章中介绍这一点），这样我们就可以不受限制的查询Data API URL。如果不指定此参数，则可能将无法查询URL，而且你会得到一个“Forbidden”的错误。

查询这些参数将返回以下信息[JSON格式](http://en.wikipedia.org/wiki/JSON)，请注意一下以下标亮的部分：

![](http://a4.qpic.cn/psb?/V108KV171LGmJd/i3KS5UieY44Ee.vxjZdIPs6o92ZeELyhzH5lgD9XZ0g!/c/dA8AAAAAAAAA&ek=1&kp=1&pt=0&bo=uwJeAbsCXgEDCC0!&sce=0-12-12&rf=0-18)

### 原文链接 ###

[http://www.codeproject.com/Articles/888694/Youtube-Data-API-v-on-Android-Introduction](http://www.codeproject.com/Articles/888694/Youtube-Data-API-v-on-Android-Introduction)