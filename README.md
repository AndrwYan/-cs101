# -cs101
from cs101
1.搭建基础
网页如何运行？
网络爬虫是一个与网站进行交互的程序。网络爬虫用于创建搜索引擎索引和归档页面，但在我们的例子中用于探索维基百科。编写爬虫前，我们需要先了解网页的工作原理。特别是，需要了解一些 HTML。

如果你是一个热爱学习的网络开发人员，可能已经熟悉了 HTML。但如果不熟悉 HTML，也别担心！编写网络爬虫时，不需要了解太多 HTML。继续阅读要点概述。

HTML 或超文本标记语言是网页的源代码。HTML 文档是描述页面内容的文本文档。其包括文本内容、页面上图像和视频的 URL 以及关于内容排列和样式的信息。网页浏览器会收到原始 HTML，并相应提供格式整齐的多媒体网页。

我们来看一个简单页面的源码，了解一下如何构建 HTML，

<title>My Website</title>
<div id="introduction">
  <p>
    Welcome to my website!
  </p>
</div>    
<div id="image-gallery">
  <p>
    This is my cat!
    <img src="cat.jpg" alt="Meow!">
    <a href="https://en.wikipedia.org/wiki/Cat">Learn more about cats!</a>
  </p>
</div>
HTML 源代码由嵌套标签组成。第一个标签是标题标签，<title>和结束标签</title>之间的文本用作页面标题。"


样本页面，标题为 "我的网站"

HTML 源代码中的下一个标签是 <div id="introduction">。div 是 "division" 的缩写，id="introduction" 表示该页面的作者将这一部分标注为引言。

我们在该标签下面的几行中可看到 </div>。这是 div 的结束标签，表示该段落代码嵌套在 div 中:

<p>
  欢迎来到我的网站！
</p>
p 是 "段落" 的缩写。<p> 和其结束标签 </p> 之间的文本是提供 HTML 时，显示在屏幕上的内容。可以将该段落称为 div 标签（嵌套在其中）的 "子类"。同样，div 是段落的 "父类"。总而言之，这种父类标签和子类标签的排列创建了一个树结构。

词汇注释：术语 "标签" 和 "元素" 密切相关，有时可互换使用。标签是一个 HTML 源码，而元素是在浏览器呈现标签后用户可以看到的可视化组件。


由嵌套标签组成的 HTML 文档树结构。

HTML 文档中的第二个 div 更复杂。它还有一个作为子类的段落标签，该段落标签有自己的子类，img 和 a。这两个子类标签嵌套在 div 标签内，成为 div 的后代标签。但它们不是 div 的子类，而是 'p` 标签的子类。

识别父类标签与子类标签
请参阅上文 "我的网站" html 来回答该问题。 image-gallery div 里面有多少元素？

在这里输入你的回答。
识别父类标签与子类标签 II
这些标签中有多少是 image-gallery 的直接后代标签？

在这里输入你的回答。
识别父类标签与子类标签 III
一个标签有多少个父类标签？该数字对于每个 html 文档是一样的。

在这里输入你的回答。
锚标签
如需爬取网页，还需要了解一个标签类型，即锚标签。我们已经看到一个锚标签：

<a href="https://en.wikipedia.org/wiki/Cat">Learn more about cats!</a>
锚标签（用<a></a>表示，用于创建链接。此示例创建了这样一个链接：

了解关于猫的更多内容！

在 href 属性中指定链接的目的，开始和结束标签之间的文本即链接的文本。

使用开发工具探索 HTML

00:00 / 01:32
1x
CC


习题 4/6
自己试用开发人员工具。浏览任何维基百科的文章，并通过查看其 HTML 源码来回答该问题。

查找带有 `mw-content-text’ 的 div。该 div 的父类是什么类型的标签？









使用 Python 获取 HTML

00:00 / 02:41
1x
CC


尝试自己请求
现在该你尝试请求库。

首先去命令行安装具有 pip 的 requests

$ pip3 install requests
（根据 Python 安装，你可能需要使用 pip，而不是 pip3）

然后打开交互式 Python 解释器测试一些请求代码。这是此前视频的代码：

>>> response = requests.get('https://en.wikipedia.org/wiki/Dead_Parrot_sketch')
>>> print(response.text)
>>> print(type(response.text))
将示例中的 url 替换为你自己选择的页面，以便在交互式 Python 解释器中对其进行测试，然后查看html。

Beautiful Soup
我们现在已经掌握了如何制作网页请求和下载 html，接下来我们了解一下如何解析 HTML。由于 HTML 只是文本，我们可以使用已经了解的工具对其进行解析；循环和字符串方法。这将极具挑战性，HTML 是一种非常灵活的语言，这使其难以正确解析。但好的一点是之前的程序员已经为我们解决了这个问题。

此前，对于此类项目我经常使用 Beautiful Soup 库。根据其文档：

“Beautiful Soup 可解析你提供的任何内容，并为你遍历树材料。可以命令其'查找所有的链接'或’查找 classexternalLink 的所有链接'或'查找 url 与 "foo.com" 匹配的所有链接或'查找粗体文本的表格标题，然后将该文本发送给我。'"

“这些示例听起来很像我们在某个 div 中查找第一个维基百科链接时遇到的问题！

我们来安装这个库并试试吧！可以使用 pip 安装最新版本的 Beautiful Soup：

$ pip3 install beautifulsoup4
Beautiful Soup 演示

00:00 / 02:03
1x
CC


自己尝试 Beautiful Soup
安装 Beautiful Soup 并试试吧！在终端中打开一个交互式解释器，并在浏览器中浏览你所选择的网页。在页面中选择元素，并尝试用 Beautiful Soup 来选择这些元素！尝试打开浏览器的开发人员工具，这有助于了解 HTML 的建构方式。

浏览页面以及 Beautiful Soup，并回答以下问题。

习题 5/6
哪一项的计算结果为页面中第一段的所有锚标签（）列？









习题 6/6
如果一个 soup 对象的名称为 soup，那么什么代码将选择一个具有 id "image-gallery" 的 div 元素？









