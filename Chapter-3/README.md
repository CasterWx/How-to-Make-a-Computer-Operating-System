## Chapter 3: First boot with GRUB

## 第3章:GRUB主引导

#### How the boot works?

引导是如何工作的?

When an x86-based computer is turned on, it begins a complex path to get to the stage where control is transferred to our kernel's "main" routine (`kmain()`). For this course, we are only going to consider the BIOS boot method and not it's successor (UEFI).

当一台基于x86的计算机被启动时，它会经历一段很复杂的路程，以到达将控制权转移到内核“主”例程(“kmain()”)的阶段。对于本课程，我们只考虑BIOS引导方法，而不考虑它的后续方法(UEFI)。

The BIOS boot sequence is: RAM detection -> Hardware detection/Initialization -> Boot sequence.

BIOS引导序列为:RAM检测->硬件检测/初始化->引导序列。

The most important step for us is the "Boot sequence", where the BIOS is done with its initialization and tries to transfer control to the next stage of the bootloader process.

对我们来说最重要的步骤是“引导序列”，此时BIOS完成了初始化，并试图将控制转移到引导加载程序的下一个阶段。

During the "Boot sequence", the BIOS will try to determine a "boot device" (e.g. floppy disk, hard-disk, CD, USB flash memory device or network). Our Operating System will initially boot from the hard-disk (but it will be possible to boot it from a CD or a USB flash memory device in future). A device is considered bootable if the bootsector contains the valid signature bytes `0x55` and `0xAA` at offsets 511 and 512 respectively (called the magic bytes of the Master Boot Record, also known as the MBR). This signature is represented (in binary) as 0b1010101001010101. The alternating bit pattern was thought to be a protection against certain failures (drive or controller). If this pattern is garbled or 0x00, the device is not considered bootable.

在“引导顺序”期间，BIOS将尝试确定一个“引导设备”(例如软盘、硬盘、CD、USB闪存设备或网络)。我们的操作系统最初将从硬盘引导(但是将来可以从CD或USB闪存设备引导它)。如果引导扇区在偏移量511和512处分别包含有效的签名字节' 0x55 '和' 0xAA '(称为主引导记录的魔法字节，也称为MBR)，则认为设备是可引导的。此签名(以二进制)表示为0b1010101001010101。交替位模式被认为是对某些故障(驱动或控制器)的保护。如果该模式被打乱或0x00，则认为该设备不可引导。

BIOS physically searches for a boot device by loading the first 512 bytes from the bootsector of each device into physical memory, starting at the address `0x7C00` (1 KiB below the 32 KiB mark). When the valid signature bytes are detected, BIOS transfers control to the `0x7C00` memory address (via a jump instruction) in order to execute the bootsector code.

BIOS从地址“0x7C00”(低于32 KiB标记的1 KiB)开始，通过将每个设备的引导扇区中的前512字节加载到物理内存中来物理搜索引导设备。当检测到有效的签名字节时，BIOS将控制传输到“0x7C00”内存地址(通过跳转指令)，以便执行引导扇区代码。

Throughout this process the CPU has been running in 16-bit Real Mode, which is the default state for x86 CPUs in order to maintain backwards compatibility. To execute the 32-bit instructions within our kernel, a bootloader is required to switch the CPU into Protected Mode.

在整个过程中，CPU一直以16位实模式运行，这是x86 CPU为了保持向后兼容性的默认状态。要在内核中执行32位指令，需要一个引导加载程序将CPU切换到保护模式。

#### What is GRUB?

#### 什么是GRUB?

> GNU GRUB (short for GNU GRand Unified Bootloader) is a boot loader package from the GNU Project. GRUB is the reference implementation of the Free Software Foundation's Multiboot Specification, which provides a user the choice to boot one of multiple operating systems installed on a computer or select a specific kernel configuration available on a particular operating system's partitions.

GNU GRUB (GNU GRand Unified Bootloader的简称)是GNU项目中的一个引导加载程序包。GRUB是自由软件基金会(Free Software Foundation)的多引导规范的参考实现，该规范为用户提供了从安装在计算机上的多个操作系统中引导一个操作系统或选择特定操作系统分区上可用的特定内核配置的选项。

To make it simple, GRUB is the first thing booted by the machine (a boot-loader) and will simplify the loading of our kernel stored on the hard-disk.

简单来说，GRUB是机器(引导加载程序)启动的第一件事，它将简化存储在硬盘上的内核的加载

#### Why are we using GRUB?

#### 我们为什么要使用GRUB?

* GRUB is very simple to use
* Make it very simple to load 32bits kernels without needs of 16bits code
* Multiboot with Linux, Windows and others
* Make it easy to load external modules in memory

* GRUB非常容易使用
* 使加载32位内核非常简单，不需要16位代码
* 多引导与Linux, Windows和其他
* 便于在内存中加载外部模块

#### How to use GRUB?

#### 如何使用GRUB?

GRUB uses the Multiboot specification, the executable binary should be 32bits and must contain a special header (multiboot header) in its 8192 first bytes. Our kernel will be a ELF executable file ("Executable and Linkable Format", a common standard file format for executables in most UNIX system).

GRUB使用多引导规范，可执行二进制文件应该是32位的，并且必须包含一个特殊的头(多引导头)，头8192个字节。我们的内核将是ELF可执行文件(“可执行和可链接格式”，大多数UNIX系统中可执行文件的通用标准文件格式)。

The first boot sequence of our kernel is written in Assembly: [start.asm](https://github.com/SamyPesse/How-to-Make-a-Computer-Operating-System/blob/master/src/kernel/arch/x86/start.asm) and we use a linker file to define our executable structure: [linker.ld](https://github.com/SamyPesse/How-to-Make-a-Computer-Operating-System/blob/master/src/kernel/arch/x86/linker.ld).

我们内核的第一个引导序列是使用汇编编写的:[start.asm](https://github.com/SamyPesse/How-to-Make-a-Computer-Operating-System/blob/master/src/kernel/arch/x86/start.asm)，我们使用一个链接器文件来定义我们的可执行结构:[linker.ld](https://github.com/SamyPesse/How-to-Make-a-Computer-Operating-System/blob/master/src/kernel/arch/x86/linker.ld)。

This boot process also initializes some of our C++ runtime, it will be described in the next chapter.

这个引导过程还初始化了一些c++运行时，将在下一章中进行描述。

Multiboot header structure:

Multiboot头结构:

```cpp
struct multiboot_info {
	u32 flags;
	u32 low_mem;
	u32 high_mem;
	u32 boot_device;
	u32 cmdline;
	u32 mods_count;
	u32 mods_addr;
	struct {
		u32 num;
		u32 size;
		u32 addr;
		u32 shndx;
	} elf_sec;
	unsigned long mmap_length;
	unsigned long mmap_addr;
	unsigned long drives_length;
	unsigned long drives_addr;
	unsigned long config_table;
	unsigned long boot_loader_name;
	unsigned long apm_table;
	unsigned long vbe_control_info;
	unsigned long vbe_mode_info;
	unsigned long vbe_mode;
	unsigned long vbe_interface_seg;
	unsigned long vbe_interface_off;
	unsigned long vbe_interface_len;
};
```

You can use the command ```mbchk kernel.elf``` to validate your kernel.elf file against the multiboot standard. You can also use the command ```nm -n kernel.elf``` to validate the offset of the different objects in the ELF binary.

您可以使用命令 ```mbchk kernel.elf```来根据多引导标准验证kernel.elf文件。您还可以使用```nm -n kernel.elf```验证elf二进制文件中不同对象的偏移量。

#### Create a disk image for our kernel and grub

#### 为内核和grub创建一个磁盘映像

The script [diskimage.sh](https://github.com/SamyPesse/How-to-Make-a-Computer-Operating-System/blob/master/src/sdk/diskimage.sh) will generate a hard disk image that can be used by QEMU.

脚本[diskimage.sh](https://github.com/SamyPesse/How-to-Make-a-Computer-Operating-System/blob/master/src/sdk/diskimage.sh)将生成一个可以使用QEMU启动的硬盘映像。

The first step is to create a hard-disk image (c.img) using qemu-img:

第一步是使用qemu-img创建硬盘映像(c.img):

```
qemu-img create c.img 2M
```

We need now to partition the disk using fdisk:

我们现在需要使用fdisk来分区磁盘:

```bash
fdisk ./c.img

# Switch to Expert commands 切换到专家命令
> x

# Change number of cylinders (1-1048576) 修改柱面数量(1-1048576)
> c
> 4

# Change number of heads (1-256, default 16) 改变磁头数量(1-256，默认16)
> h
> 16

# Change number of sectors/track (1-63, default 63) 更改磁道数目(1-63，默认63)
> s
> 63

# Return to main menu 返回主菜单
> r

# Add a new partition 添加一个新分区
> n

# Choose primary partition 选择主分区
> p

# Choose partition number 选择分区号
> 1

# Choose first sector (1-4, default 1) 选择第一个扇区(1-4，默认1)
> 1

# Choose last sector, +cylinders or +size{K,M,G} (1-4, default 4) 选择最后一个扇区，+柱面或+大小{K,M,G}(1-4，默认4)
> 4

# Toggle bootable flag 切换启动的标志
> a

# Choose first partition for bootable flag 为可引导标志选择第一个分区
> 1

# Write table to disk and exit 将表写到磁盘并退出
> w
```

We need now to attach the created partition to the loop-device using losetup. This allows a file to be access like a block device. The offset of the partition is passed as an argument and calculated using: **offset= start_sector * bytes_by_sector**.

现在我们需要使用losetup命令将创建的分区附加到循环设备上。这允许像块设备一样访问文件。分区的偏移量作为参数传递并使用:**offset= start_扇区* bytes_by_扇区**计算。

Using ```fdisk -l -u c.img```, you get: 63 * 512 = 32256.

使用 ```fdisk -l -u c.img```, 你将得到: 63 * 512 = 32256.

```bash
losetup -o 32256 /dev/loop1 ./c.img
```

We create a EXT2 filesystem on this new device using:

我们使用以下命令在这个新设备上创建EXT2文件系统:

```bash
mke2fs /dev/loop1
```

We copy our files on a mounted disk:

我们复制我们的文件在一个挂载磁盘:

```bash
mount  /dev/loop1 /mnt/
cp -R bootdisk/* /mnt/
umount /mnt/
```

Install GRUB on the disk:

在磁盘上安装GRUB:

```bash
grub --device-map=/dev/null << EOF
device (hd0) ./c.img
geometry (hd0) 4 16 63
root (hd0,0)
setup (hd0)
quit
EOF
```

And finally we detach the loop device:

最后我们分离驱动循环:

```bash
losetup -d /dev/loop1
```

#### See Also

#### 参考

* [GNU GRUB on Wikipedia](http://en.wikipedia.org/wiki/GNU_GRUB)
* [Multiboot specification](https://www.gnu.org/software/grub/manual/multiboot/multiboot.html)
