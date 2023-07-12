
[课程地址]([Lab: Xv6 and Unix utilities (mit.edu)](https://pdos.csail.mit.edu/6.828/2021/labs/util.html))_

## 1. 配置环境

- 安装依赖
````bash
sudo apt-get install git build-essential gdb-multiarch qemu-system-misc gcc-riscv64-linux-gnu binutils-riscv64-linux-gnu
````
出现网速不够的情况自行换源

- git获取课程配套代码
```bash
git clone git://g.csail.mit.edu/xv6-labs-2021
```
在根目录下运行`make qemu`，看见如下输出即启动成功
```
qemu-system-riscv64 -machine virt -bios none -kernel kernel/kernel -m 128M -smp 3 -nographic -drive file=fs.img,if=none,format=raw,id=x0 -device virtio-blk-device,drive=x0,bus=virtio-mmio-bus.0

xv6 kernel is booting

hart 1 starting
hart 2 starting
init: starting sh
```

## 2. sleep指令

安装好xv6系统内核后，观察项目代码（我这里已经编译过，所以实际可能有所不同），可以发现用户态的代码聚集在user文件夹下，内核态的代码聚集在kernel文件夹下

课程需要我们仿照user目录下的命令（例如ls），写一个sleep命令，在开始这个任务前，我们有一些前置工作需要完成
1. 阅读[xv6 book](https://pdos.csail.mit.edu/6.828/2021/xv6/book-riscv-rev2.pdf)中的Chapter 1
2. 阅读user/目录下的所有程序，理解如何编写一个命令行程序

[这个链接]()包含了我对整本书的阅读理解

