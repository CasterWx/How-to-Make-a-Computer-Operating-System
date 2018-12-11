## Chapter 2: Setup the development environment

## 第2章:设置开发环境

The first step is to setup a good and viable development environment. Using Vagrant and Virtualbox, you'll be able to compile and test your OS from all the OSs (Linux, Windows or Mac).

第一步是建立一个良好和可行的开发环境。使用Vagrant和Virtualbox，您将能够从很多平台(Linux、Windows或Mac)编译和测试您的操作系统。

### Install Vagrant

### 安装Vagrant

> Vagrant is free and open-source software for creating and configuring virtual development environments. It can be considered a wrapper around VirtualBox.

> Vagrant是一款用于创建和配置虚拟开发环境的免费开源软件。它可以看作是VirtualBox的包装器。

Vagrant will help us create a clean virtual development environment on whatever system you are using.
The first step is to download and install Vagrant for your system at http://www.vagrantup.com/.

Vagrant将帮助我们在您使用的任何系统上创建一个干净的虚拟开发环境。第一步是在 [http://www.vagrantup.com/](http://www.vagrantup.com/) 为您的系统下载并安装Vagrant。

### Install Virtualbox

### 安装Virtualbox

> Oracle VM VirtualBox is a virtualization software package for x86 and AMD64/Intel64-based computers.

> Oracle VM VirtualBox是一个针对x86和AMD64/intel64计算机的虚拟化软件包。

Vagrant needs Virtualbox to work, Download and install for your system at https://www.virtualbox.org/wiki/Downloads.

Vagrant先需要安装Virtualbox，将它下载和安装到您的系统,下载地址:[https://www.virtualbox.org/wiki/Downloads](https://www.virtualbox.org/wiki/Downloads)。

### Start and test your development environment

### 启动并测试您的开发环境

Once Vagrant and Virtualbox are installed, you need to download the ubuntu lucid32 image for Vagrant:

安装好Vagrant和Virtualbox后，需要下载ubuntu lucid32的Vagrant:

```
vagrant box add lucid32 http://files.vagrantup.com/lucid32.box
```

Once the lucid32 image is ready, we need to define our development environment using a *Vagrantfile*, [create a file named *Vagrantfile*](https://github.com/SamyPesse/How-to-Make-a-Computer-Operating-System/blob/master/src/Vagrantfile). This file defines what prerequisites our environment needs: nasm, make, build-essential, grub and qemu.

一但lucid32映像准备好了，我们就可以使用 *Vagrantfile* 定义开发环境，[创建一个名为 *Vagrantfile* 的文件](https://github.com/SamyPesse/How-to-Make-a-Computer-Operating-System/blob/master/src/Vagrantfile)。使用这个文件需要先准备以下环境:nasm、make、build-essential、grub和qemu。

Start your box using:

启动你的虚拟机

```
vagrant up
```

You can now access your box by using ssh to connect to the virtual box using:

您现在可以使用ssh访问您的虚拟机，使用:

```
vagrant ssh
```

The directory containing the *Vagrantfile* will be mounted by default in the */vagrant* directory of the guest VM (in this case, Ubuntu Lucid32):

包含*Vagrantfile*的目录将默认挂载在客户VM的 */vagrant* 目录中(本例中为Ubuntu Lucid32):

```
cd /vagrant
```

#### Build and test our operating system

#### 构建和测试我们的操作系统

The file [**Makefile**](https://github.com/SamyPesse/How-to-Make-a-Computer-Operating-System/blob/master/src/Makefile) defines some basics rules for building the kernel, the user libc and some userland programs.

文件[**Makefile**](https://github.com/SamyPesse/How-to-Make-a-Computer-Operating-System/blob/master/src/Makefile)定义了一些构建内核、用户libc和一些用户空间程序的基本命令规则。

Build:

构建:

```
make all
```

Test our operating system with qemu:

使用qemu测试我们的操作系统:

```
make run
```

The documentation for qemu is available at [QEMU Emulator Documentation](http://wiki.qemu.org/download/qemu-doc.html).

You can exit the emulator using: Ctrl-a.

qemu的文档可以在[QEMU Emulator Documentation(qemu模拟器文档)](http://wiki.qemu.org/download/qemu-doc.html)中找到。


您可以使用:Ctrl-a退出模拟器。