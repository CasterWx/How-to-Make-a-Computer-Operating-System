How to Make a Computer Operating System
如何制作一个操作系统
=======================================

Online book about how to write a computer operating system in C/C++ from scratch.

一本关于如何用C/ c++从零开始编写计算机操作系统的在线书籍。

**Caution**: This repository is a remake of my old course. It was written several years ago [as one of my first projects when I was in High School](https://github.com/SamyPesse/devos), I'm still refactoring some parts. The original course was in French and I'm not an English native. I'm going to continue and improve this course in my free-time.

**谨慎**:这个资源库是我以前课程的翻版。它是几年前写的[作为我高中时的第一个项目之一](https://github.com/SamyPesse/devos)，我仍然在重构一些部分。这个课程最初的是用法语，我的母语不是英语。我打算在空闲时间继续改进这门课。

**Book**: An online version is available at [http://samypesse.gitbooks.io/how-to-create-an-operating-system/](http://samypesse.gitbooks.io/how-to-create-an-operating-system/) (PDF, Mobi and ePub). It was generated using [GitBook](https://www.gitbook.com/).

**书籍**: 网上版本可于[http://samypesse.gitbooks.io/howtocreateanoperating-system/](http://samypesse.gitbooks.io/howtocreateanoperating-system/) (PDF, Mobi及ePub)下载。它是使用[GitBook](https://www.gitbook.com/)生成的。

**Source Code**: All the system source code will be stored in the [src](https://github.com/SamyPesse/How-to-Make-a-Computer-Operating-System/tree/master/src) directory. Each step will contain links to the different related files.

**源代码**:所有系统源代码将存储在[src](https://github.com/samypesse/howto - make -a- computer - operating-system/tree/master/src)目录中。每个步骤将包含指向不同相关文件的链接。

**Contributions**: This course is open to contributions, feel free to signal errors with issues or directly correct the errors with pull-requests.

**投稿**:本课程开放投稿，有问题可以随时通知错误，也可以直接用pull-request更正错误。

**Questions**: Feel free to ask any questions by adding issues or commenting sections.

**问题**:可以通过添加问题(issues)或评论(commenting)来提问。

You can follow me on Twitter [@SamyPesse](https://twitter.com/SamyPesse) or [GitHub](https://github.com/SamyPesse).

你可以关注我的推特[@SamyPesse](https://twitter.com/SamyPesse)或者[GitHub](https://github.com/SamyPesse)。

### What kind of OS are we building?

### 我们在构建什么样的操作系统?

The goal is to build a very simple UNIX-based operating system in C++, not just a "proof-of-concept". The OS should be able to boot, start a userland shell, and be extensible.

目标是用c++构建一个非常简单的基于UNIX的操作系统，而不仅仅是“概念验证”。操作系统应该能够引导、启动用户界面shell并具有可扩展性。

![Screen](./preview.png)
