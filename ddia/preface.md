# 序

如果近几年从业于软件工程，特别是服务器端和后端系统开发，那么您很有可能已经被大量关于数据存储和处理的时髦词汇轰炸过了： NoSQL！大数据！Web-Scale！分片！最终一致性！ACID！ CAP定理！云服务！MapReduce！实时！

在最近十年中，我们看到了很多有趣的进展，关于数据库，分布式系统，以及在此基础上构建应用程序的方式。这些进展有着各种各样的驱动力：

* 谷歌，雅虎，亚马逊，脸书，领英，微软和推特等互联网公司正在和巨大的流量/数据打交道，这迫使它们创造能有效应对这种规模的新工具。
* 企业需要敏捷，廉价地测试假设，通过缩短开发周期和保持数据模型的灵活性，快速响应新的市场洞察。
* 免费和开源软件变得非常成功，在许多环境中比商业软件和定制软件更受欢迎。
* 处理器主频几乎没有增长，但是多核处理器已经成为标配，网络也越来越快。这意味着并行程度只增不减。
* 即使您在一个小团队中工作，现在也可以构建分布在多台计算机甚至多个地理区域的系统，这要归功于譬如亚马逊网络服务（AWS）等基础设施即服务（IaaS）概念的践行者。
* 许多服务都要求高可用，因停电或维护导致的服务不可用，变得越来越难以接受。

数据密集型应用正在通过利用这些技术进步推动可能性的边界。如果**数据是其主要挑战**（数据量，数据复杂度或数据变化速度），我们称这类应用为**数据密集型**，与之相对的是**计算密集型**，即处理器速度是瓶颈。

帮助数据密集型应用程序存储和处理数据的工具和技术已经迅速适应这些变化。新型数据库系统（“NoSQL”）已经引起了人们的关注，但消息队列，缓存，搜索索引，批处理和流处理框架以及相关技术也非常重要。许多应用程序组合使用这些技术。

这些充满整个空间的流行语是对新的可能性的热情的表现，这是一件好事。但是，作为软件工程师和架构师，如果我们想要建立良好的应用程序，我们还需要对各种层出不穷的技术持有准确而严谨的技术性理解，以及它们之间的取舍权衡。为此，我们必须深入挖掘流行语背后的内容。

幸运的是，在技术快速变化的背后，无论您使用的是什么版本的特定工具，都存在一些持久的原则。如果你了解这些原则，你就可以看到每个工具的适用位置，如何充分利用它们，以及如何避免其中的陷阱。这是本书的初衷。

本书的目标是帮助您在多样而快速变化的处理和存储数据技术的大观园中找到方向。这本书不是一个特定工具的教程，也不是一本充满干枯理论的教科书。相反，我们将看到一些成功的数据系统示例：一些构成了许多流行应用程序基础，必须在每天的生产中满足可伸缩性，性能和可靠性需求的技术。

我们将深入这些系统的内部，梳理他们的关键算法，讨论他们的原则和它们必须做出的权衡。在这个过程中，我们将尝试寻找有用的思考数据系统的方式 —— 不仅仅关于它们是如何工作的，还包括为什么它们以这种方式工作，以及我们需要问什么问题。

阅读本书后，您将能够很好地决定哪种技术适合哪种用途，并了解如何将工具组合起来，形成良好应用架构的基础。您不会获得从头开始构建自己的数据库存储引擎的能力，但幸运的是，这是很少有必要的。您将会获得的是，对你的系统在底层做什么有一个很好的直觉，这样您就可以推断它们的行为，做出好的设计决定，并追踪任何可能出现的问题。



## 本书的目标读者

如果您开发的应用程序具有用于存储或处理数据的某种服务器/后端系统，并且您的应用程序使用互联网（例如，Web应用程序，移动应用程序或连接到互联网的传感器），那么本书就是为您准备的。

本书适用于热爱编写代码的软件工程师，软件架构师和技术经理。如果您需要就您所从事的系统架构做出决定，例如您需要选择解决某个特定问题的工具，并找出如何最好地应用这些工具来解决问题，那么这本书对您尤其重要。但即使您不能选择您的工具，这本书仍将帮助您更好地了解您所使用工具的长处和短处。

您应该具有构建基于Web的应用程序或网络服务的一些经验，并且您应该熟悉关系数据库和SQL。任何您了解的非关系型数据库和其他与数据相关的工具都会更有帮助，但不是必需的。常见的网络协议如TCP和HTTP的一般理解是有帮助的。编程语言或框架的选择对阅读本书没有任何不同影响。

如果以下任何一条对你是真的，你会发现这本书很有价值：

* 您想了解如何使数据系统可扩展，例如，支持拥有数百万用户的Web或移动应用程序。
* 您需要提高应用程序的可用性（最大限度地减少停机时间）和运行稳定。
* 您正在寻找使系统长期易于维护的方法，即使随着需求和技术的变化而变化。
* 您对事物的运作方式有着天然的好奇心，并且希望知道一些主要网站和在线服务背后发生的事情。这本书打破了各种数据库和数据处理系统的内幕，探索他们设计中的智慧是非常有趣的。

有时在讨论可扩展的数据系统时，人们会评论：“你又不在谷歌或亚马逊，别操心可扩展性了，直接上关系数据库。“这个陈述有一定的道理：为了您不需要的规模而构建程序不仅会浪费不必要的精力，并且可能会把您锁死在一个不灵活的设计中。实际上这是“过早优化”的一种形式。不过，选择合适的工具确实很重要，而不同的技术各有优缺点。我们将会看到，关系数据库虽然很重要，但绝不是数据处理的终章。



## 本书涉及的领域

本书不会试图给出详细的指导，说明如何安装或使用特定的软件包或API，因为已经有大量的文档。相反，我们讨论了基本的数据系统的各种原则和权衡，并探讨了不同产品所做出的不同设计决策。

在电子书版本中，我们包含了在线资源全文的链接。所有链接都在发布时进行了验证，但不幸的是，由于网络的性质，链接往往频繁地中断。如果您遇到链接断开的情况，或者您正在阅读本书的打印副本，则可以使用搜索引擎查找引用。对于学术论文，您可以在Google学术搜索中搜索标题以查找开放获取的PDF文件。或者，您可以在[DDIA-Reference](https://github.com/ept/ddia-references)上找到所有的参考资料，我们在那里维护最新的链接。

我们主要关注数据系统的体系结构以及它们被集成到数据密集型应用程序中的方式。本书没有讨论部署，操作，安全，管理等领域的空间 —— 这些都是复杂而重要的话题，仅仅在本书中用肤浅的注解讨论它们对它们不公平。它们各自配得上一本单独的书。

本书中描述的许多技术都被涵盖在**大数据**这个时髦词的范畴中。然而“大数据”这个术语被滥用，缺乏明确定义，以至于在严肃的工程讨论中没有用处。这本书使用更少歧义的术语，如“单点系统”之于”分布式系统“，或”在线/交互式“之于”离线/批处理系统“。

本书对自由和开放源码的软件（FOSS）有一定偏好，因为阅读，修改和执行源代码是了解一个东西详细工作原理的好方法。开放平台还可以降低供应商垄断的风险。然而，在适当的情况下，我们也讨论专有软件（封闭源码软件，软件即服务，或一些公司内部的仅在文献中描述但未公开发布的软件）。



## 本书纲要

本书分为三部分：

1. 在[第一部分](part-i.md)中，我们会讨论设计数据密集型应用所赖的基本思想。我们从[第1章](ch1.md)开始，讨论我们实际要达到的目标：可靠性，可扩展性和可维护性；我们该如何考虑它们；以及如何实现它们。在[第2章](ch2.md)中，我们比较了几种不同的数据模型和查询语言，看看它们是如何适用于不同的场景。在[第3章](ch3.md)中将讨论存储引擎：数据库如何在磁盘上摆放数据，以便能高效地再次找到它。[第4章](ch4.md)转向数据编码（序列化），以及随时间演化的模式。

2. 在[第二部分](part-ii.md)中，我们从讨论存储在一台机器上的数据转向讨论分布在多台机器上的数据。这对于可扩展性通常是必需的，但带来了各种独特的挑战。我们首先讨论复制（[第5章](ch5.md)），分区/分片（[第6章](ch6.md)）和事务（[第7章](ch7.md)）。我们然后探索关于分布式系统的问题的更多细节（[第8章](ch8.md)），以及在分布式系统中实现共识和一致性意味着什么（[第9章](ch9.md)）。

3. 在[第三部分](part-iii.md)中，我们讨论从其他数据集衍生一些数据集的系统。派生数据经常发生在异构系统中：当没有一个数据库可以把所有事都做好时，应用程序需要集成几个不同的数据库，缓存，索引等等。在[第10章](ch10.md)中我们将从一种批处理派生数据的方法开始，然后我们将在第11章中在此基础上用流处理构建。最后，在[第12章](ch12.md)中，我们将所有内容放在一起，并讨论未来构建可靠，可伸缩和可维护的应用程序的方法。




## 参考文献与延伸阅读

本书中讨论的大部分内容已经在其它地方以某种形式出现过了 —— 会议演示文稿，研究论文，博客文章，代码，BUG跟踪器，邮件列表，以及工程习惯中。本书总结了不同来源资料中最重要的想法，并在文本中包含了指向原始文献的指针。 如果你想更深入地探索一个领域，那么每章末尾的参考文献都是很好的资源，其中大部分可以免费在线获取。



## O‘Reilly Safari

[Safari](http://oreilly.com/safari)赛高！



## 致谢

本书融合了学术研究和工业实践的经验，是大量其他人的思想和知识的融合与系统化。在计算中，我们往往会被新的东西所吸引，但是我认为我们有很多东西可以从以前的东西中学习。这本书有超过800篇文章，博客文章，讲座，文档等参考资料，对我来说这是一个宝贵的学习资源。我非常感谢这些材料的作者分享他们的知识。

我也从个人对话中学到了很多东西，这要感谢大量的人花时间讨论想法，耐心地向我解释。特别感谢Joe Adler, Ross Anderson, Peter Bailis, Márton Balassi, Alastair Beresford, Mark Callaghan, Mat Clayton, Patrick Collison, Sean Cribbs, Shirshanka Das, Niklas Ekström, Stephan Ewen, Alan Fekete, Gyula Fóra, Camille Fournier, Andres Freund, John Garbutt, Seth Gilbert, Tom Haggett, Pat Hel‐ land, Joe Hellerstein, Jakob Homan, Heidi Howard, John Hugg, Julian Hyde, Conrad Irwin, Evan Jones, Flavio Junqueira, Jessica Kerr, Kyle Kingsbury, Jay Kreps, Carl Lerche, Nicolas Liochon, Steve Loughran, Lee Mallabone, Nathan Marz, Caitie McCaffrey, Josie McLellan, Christopher Meiklejohn, Ian Meyers, Neha Narkhede, Neha Narula, Cathy O’Neil, Onora O’Neill, Ludovic Orban, Zoran Perkov, Julia Powles, Chris Riccomini, Henry Robinson, David Rosenthal, Jennifer Rullmann, Matthew Sackman, Martin Scholl, Amit Sela, Gwen Shapira, Greg Spurrier, Sam Stokes, Ben Stopford, Tom Stuart, Diana Vasile, Rahul Vohra, Pete Warden, 以及 Brett Wooldridge.

通过审阅草案并提供反馈意见，更多的人对本书的撰写非常有价值。对于这些贡献，我特别感谢Raul Agepati，Tyler Akidau，Mattias Andersson，Sasha Baranov，Veena Basavaraj，David Beyer，Jim Brikman，Paul Carey，Raul Castro Fernandez，Joseph Chow，Derek Elkins，Sam Elliott，Alexander Gallego，Mark Grover ，斯图尔·万洛威（Stu Hallow Halloway），海蒂·霍华德（Heidi Howard），尼科拉·克莱普曼（Nicola Kleppmann），斯特凡·克鲁帕（Stefan Kruppa），比约恩·马德森（Bjorn Madsen），麦克尔·桑德（Sandder Mak），斯特凡·波德科维斯基（Stefan Podkowinski），菲尔·波特（Phil Potter）当然，对于本书中的任何遗留错误或不愉快的意见，我承担全部责任。

为了帮助这本书出版，并且耐心地处理我缓慢的写作和不寻常的要求，我感谢编辑Marie Beaugureau，Mike Loukides，Ann Spencer和O'Reilly的所有团队。为了帮助找到合适的单词，我要感谢Rachel Head。尽管有其他的工作承诺给了我写作的时间和自由，但我要感谢Alastair Beresford，Susan Goodhue，Neha Narkhede和Kevin Scott。

非常特别的感谢是Shabbir Diwan和Edie Freedman，他们非常小心的说明了各章的地图。他们以非常规的创作地图的想法，使他们如此美丽和令人兴奋，真是太棒了。

最后，我的爱情传到了我的家人和朋友身上，没有他，我将无法完成这个花了近四年时间的写作过程。你是最好的。