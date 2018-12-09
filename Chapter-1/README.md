## Chapter 1: Introduction to the x86 architecture and about our OS

## 第1章:介绍x86架构和我们的操作系统

### What is the x86 architecture?

### 什么是x86架构?

> The term x86 denotes a family of backward compatible instruction set architectures based on the Intel 8086 CPU.

> x86是指一组基于Intel 8086 CPU的向后兼容指令集架构。

The x86 architecture is the most common instruction set architecture since its introduction in 1981 for the IBM PC. A large amount of software, including operating systems (OS's) such as DOS, Windows, Linux, BSD, Solaris and Mac OS X, function with x86-based hardware.

x86体系结构是自1981年引入IBM PC以来最常见的指令集体系结构。大量的软件，包括DOS、Windows、Linux、BSD、Solaris和Mac OS X等操作系统，都使用基于x86的硬件。

In this course we are not going to design an operating system for the x86-64 architecture but for x86-32, thanks to backward compatibility, our OS will be compatible with our newer PCs (but take caution if you want to test it on your real machine).

在本课程中，我们不打算设计x86-64架构的操作系统，而是设计x86-32的操作系统，由于向后兼容性，我们的操作系统将与我们的新pc兼容(但如果您想在实际机器上测试它，请谨慎)。

### Our Operating System

### 我们的操作系统

The goal is to build a very simple UNIX-based operating system in C++, but the goal is not to just build a "proof-of-concept". The OS should be able to boot, start a userland shell and be extensible.

目标是用c++构建一个非常简单的基于unix的操作系统，但目标不仅仅是构建一个“概念验证”。该操作系统应该能够引导、启动用户界面shell并具有可扩展性。

The OS will be built for the x86 architecture, running on 32 bits, and compatible with IBM PCs.

该操作系统将为x86架构构建，运行在32位上，并与IBM pc兼容。

**Specifications(规范):**

* Code in C++ | c++代码
* x86, 32 bit architecture | x86, 32位架构
* Boot with Grub | 使用Grub启动
* Kind of modular system for drivers | 驱动程序的模块化系统
* Kind of UNIX style | UNIX风格
* Multitasking | 多任务
* ELF executable in userland
* Modules (accessible in userland using /dev/...) | 模块(可在用户区使用/dev/…访问): :
    * IDE disks | IDE磁盘
    * DOS partitions | DOS分区
    * Clock | 时钟
    * EXT2 (read only) | EXT2(只读)
    * Boch VBE | 卷VBE
* Userland : | 用户:
    * API Posix
    * LibC
    * "Can" run a shell or some executables (e.g., lua) “可以”运行shell或一些可执行文件(例如lua)
