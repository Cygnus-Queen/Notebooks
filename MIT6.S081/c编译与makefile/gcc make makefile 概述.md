MIT6.S081的实验都是基于C语言完成的，每当完成一个新函数（例如Lab1的sleep函数），都需要将它加入到makefile文件中编辑，那么弄清楚makefile，gcc相关的一些编译知识就非常有必要了。

## GCC概述
gcc是一个编译器，将一个c语言代码编译为可执行文件的流程如下：
![[Pasted image 20230714160858.png]]

**1. 预处理（pre-processing）**
`gcc -E hello.c -o hello.i`，将引入的头文件（#include）和定义的宏（#define）扩展到代码中，预处理之后的程序还是文本，可以用文本编辑器打开，上述命令中-E是让编译器在预处理之后就退出，不进行后续编译过程

**2. 编译（compilation）**
`gcc -S hello.i -o hello.s`，将预处理过的文件编译成汇编程序，在编译时，编译器只检测程序语法，和函数、变量是否被声明。如果函数未被声明，编译器会给出一个警告，但可以生成Object File。而在链接程序时，链接器会在所有的Object File中找寻函数的实现，如果找不到，那到就会报链接错误码（Linker Error）

**3. 汇编（assembly）**
`gcc -c hello.s hello.o`，将汇编程序转换成目标文件，二进制格式机器码，每一个源文件都需要产生一个目标文件

**4. 链接（linker）**
`gcc hello.o -o hello`，将一个或多个目标文件连接成最终的可执行文件

## GCC常用参数
1. --version 查看版本
2. -v（verbose冗长的），输出编译的详细信息 
3. -std 指定标准
4. -o 指定输出文件的名称
5. -Wall 输出所有的警告信息
6. -c 只将源文件编译为 object 文件（*.o），而不进行链接，之后可以使用 `gcc -o myprog.exe file1.o file2.o` 将多个 object 文件连接成可执行文件
7. -shared 编译为共享库（*.dll，*.so）
8. -S 编译为汇编代码

## Makefile

**会不会写makefile，从一个侧面说明了一个人是否具备完成大型工程的能力**。因为，makefile关系到了整个工程的编译规则。一个工程中的源文件不计数，其按**类型、功能、模块**分别放在若干个目录中，makefile定义了一系列的规则来指定，哪些文件需要先编译，哪些文件需要后编译，哪些文件需要重新编译，甚至于进行更复杂的功能操作

因为makefile就像一个Shell脚本一样，其中也可以执行操作系统的命令。makefile带来的好处就是“自动化编译”，一旦写好，只需要一个make命令，整个工程完全自动编译，极大的提高了软件开发的效率。make是一个命令工具，是一个解释makefile中指令的命令工具，一般来说，大多数的IDE都有这个命令，比如：Delphi的make，Visual C++的nmake，Linux下GNU的make。可见，makefile成为了一种在工程方面的编译方法。

但是不同的厂商make各不相同，本介绍只对GNU的make进行介绍。

#### Makefile里有什么？
Makefile里主要包含了**五个东西：显式规则、隐晦规则、变量定义、文件指示和注释。**
