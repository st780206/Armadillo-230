# Armadillo-230
Armadillo-230

目标：升级系统

https://armadillo.atmark-techno.com/armadillo-230

https://download.atmark-techno.com/armadillo-230/



基于arm的Linux内核编译
https://www.cnblogs.com/wanghuaijun/p/13928450.html

我的Ubuntu版本是14.04

1、在官网下载Linux内核源码
    官网地址：https://www.kernel.org/

2、解压Linux内核源码

3、安装arm-gcc交叉编译工具链:sudo apt-get install arm-linux-gnueabi

4、内核版本大于3.0的方法：(2.6的版本好像更直接一点)
    到Linux内核源码的arch/arm/config找到对应的配置文件，将需要的配置文件拷贝到Linux内核的根目录下，例如：
    我使用的内核版本是：linux-3.16.57.tar.xz
    我到  ./linux-3.16.57/arch/arm/configs目录下，找到我对应的配置文件。我的硬件型号是NXP的IMX7，所以我将imx_v6_v7_defconfig文件拷贝到./linux-3.16.57目录下

    
5、修改Makefile，Makefile在解压的源码的根目录下：
    打开Makefile在Makefile中找到

        ARCH        ?= $(SUBARCH)
        CROSS_COMPILE    ?= $(CONFIG_CROSS_COMPILE:"%"=%)
    并修改成：
        ARCH        ?= arm
        CROSS_COMPILE    ?= arm-linux-gnueabi-
     保存。
        
6、执行命令：make imx_v6_v7_defconfig
    会生成一个.config的隐藏文件，通过ls -a命令可以显示出来

7、安装图形界面：sudo apt-get install ncurses-dev

8、执行make menuconfig打开图形界面，通过对图形界面的选择来配置内核，你想要什么功能，你就选择什么功能。
    按 y 是选中
    按 n 是取消
    按 m 是将改功能编译成模块
    
    选择完毕之后，保存，退出。
    
    
9、执行 make -j2 zImage 开始编译内核
    -j2 ：    开启两个线程进行编译。-j4就是开启4个线程编译
    zImage    是我们要生成的目标镜像

 

注：在编译的过程中，有可能会出现错误，我就出现了：

/bin/sh: 1: lzop: not found

出现错误后，我开始很慌张，后来我把错误进行了百度，网上一般都有解决的办法。

我这个问题解决的办法是：

sudo apt-get install lzop

然后 ：

      make -j2 zImage

继续编译，编译会从错误处继续。





