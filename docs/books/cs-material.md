---
icon: material/book
---

# CS

## 语言相关

### Java

~~2018 年，一位十三十四岁的少年因 Minecraft 误入了编程歧途~~

《Java 从入门到精通》是我入门编程的梦的开始，是引领我入门开发的第一本书。这本书写的内容很书面化离实践太远了，真正上手主要还是靠当时写 Minecraft 的 Bukkit 插件学习入门的。

此外，吐槽下 Java 是真的很啰嗦（

- 《Java 从入门到精通》


### C++

因为大一时候要学 C++ 课程就看了《C++ Primer Plus》当时没学过不带 GC 的语言，选了 Primer Plus 而不是 Primer。  

- 《C++ Primer Plus》

### Python

学习 C++ 后入门的第三门语言是 Python ，因为已经有很多的语言基础了，因此对 Python 官方教程都是挑着看的。

爬虫入门，主要直接用和看的 Scrapy 的文档，直接实践爬取我做项目要的词典数据了。至于数据分析和机器学习，选择了 Kaggle 学习相关的部分课，还有Michael Nielsen 的[NNDL](http://neuralnetworksanddeeplearning.com/)，相关见[人工智能与机器学习](#ai-machine-learning)。

- [Python 官方教程](https://docs.python.org/zh-cn/3.12/tutorial/index.html)


### 前端类

由于想要开发应用和网站的需求，还是接触了前端的 HTML，CSS，TypeScript 入门。对于 HTML 和 CSS 部分主要看 MDN 学习，CSS 只看了选择器很基础的部分，布局什么的没看（因为自我觉得没 UI 设计天赋，主要还是靠 LLM 帮我处理 。TypeScript 只大概看了官方的[HandBook](https://www.typescriptlang.org/docs/handbook/intro.html)。

之后我就紧接着就去学习框架 [Angular](https://angular.dev/) 了，顺带入门了 RxJS，看的是这篇博客，叫 [The introduction to Reactive Programming you've been missing](https://gist.github.com/staltz/868e7e9bc2a7b8c1f754)，GitHub 上有对应的翻译[ RP 入门](https://github.com/benjycui/introrx-chinese-edition)。


- [学习 Web 开发 | MDN](https://developer.mozilla.org/zh-CN/docs/Learn_web_development)
- [TypeScript Handbook](https://www.typescriptlang.org/docs/handbook/intro.html)
- [RP 入门](https://github.com/benjycui/introrx-chinese-edition)

## 算法与数据结构

这部分学习材料比较零散，都没有一个比较满意的系统书籍，主要还是靠做 CS61B lab 练习。

CS61B 没全部看完，做到实现简易的 Git 就没做了，后面的课也没看了。红皮的算法主要看的图和排序部分，Hello 算法主要是补充概念上的知识。 CLRS 主要是作为工具书便用变学看的。


- CS61B 国外课程
- 红皮的《算法（第四版）》
- [Hello 算法](https://www.hello-algo.com/)
- Introduction to Algorithms (CLRS) 

## 操作系统

《Operating Systems Principles and Practice》给我感觉收获很多，可惜没非常硬核的代码示例也没实际的工程实践结合。
对于只想了解多线程开发，这本书只有第二卷值得读，主要是以条件变量和锁去构建多线程应用，对于信号量（semaphore）非常少，CAS 有提及，但是也不是很深入。除此之外，也另外做了一点 MIT 6.828 的 lab，但太枯燥了就没继续做下去。

- 《Operating Systems Principles and Practice Vol.1 Kernels and Processes》
- 《Operating Systems Principles and Practice Vol.2 Concurrency》
- 《Operating Systems Principles and Practice Vol.3 Memory and Management 》(在看)


## 计算机网络

《Computer Networking: A Top-Down Approach》这本书，只看了从 1 到 6 章，第 7 章开始从标题离应用层面太远了就没看了（
搓完了 CS144 2024 Winter 的所有 lab，主要还对 TCP 和 ARP 协议上促进更深的理解。

- Computer Networking: A Top-Down Approach  
- CS144 2024 Winter lab

## 数据库

《Database System Concepts》这本书，主要是看的 PART 1 的 SQL 各种语句，其他部分还在考虑要不要看，感觉对实际应用帮助不大。  

强烈推荐看[Use The Index, Luke!](https://use-the-index-luke.com/) ，对数据库查询优化有很大的理解和帮助，很贴近实际的工程场景，实践性很强。

- 《Database System Concepts》
- [Use The Index, Luke!](https://use-the-index-luke.com/) (在看)

## 计算机体系结构

《Computer Organization and Design RISC-V Edition》这本书，只看了 1，2，3，5章，主要还是不太感兴趣，没继续看下去，对汇编倒是有了一些了解。

- Computer Organization and Design RISC-V Edition
- CS61C 的 risc-v 的 lab (没做完)

## 编译原理

因为对写一个字幕文件的解析器有需求，去了解了下相关工具处理看了 [LLVM Tutorial](https://llvm.org/docs/tutorial/) 的前两章，前两章已经完全够我当时处理字幕文件的需求了。不过，我本身对编译原理并不是特别感兴趣，因此也没有继续深入学习下去。

- [LLVM Tutorial](https://llvm.org/docs/tutorial/)

<a id="ai-machine-learning"></a>
## 人工智能与机器学习

一开始，本身对机器学习没啥兴趣（因为大家都在做，但出于想做的东西需要就去学习了。

Michael Nielsen 的 [Neural Networks and Deep Learning](http://neuralnetworksanddeeplearning.com/)，挺适合深度学习入门的，还在看。

- [Kaggle](https://www.kaggle.com)
- [Neural Networks and Deep Learning](http://neuralnetworksanddeeplearning.com/)

## 工具类

[《Pro Git》](https://github.com/progit/progit2-zh)这本书，主要是看了前几章对暂存区，工作区概念的学习，剩下的其他东西主要还是边用边学了。  

Linux 入门主要看的社区翻译的 [The Linux Command Line](https://github.com/billie66/TLCL)，不过翻译有些糟糕，不过有双语对照问题不大。

Docker 入门看的[Docker Curriculum](https://docker-curriculum.com/) 主要是入门了解 Docker 的基本概念和使用。

- [《Pro Git》](https://github.com/progit/progit2-zh)
- [The Linux Command Line](https://github.com/billie66/TLCL)
- [Docker Curriculum](https://docker-curriculum.com/)