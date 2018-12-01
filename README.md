# centos7-gcc4.9

centos7内核下载地址：

官方：https://elrepo.org/linux/

第三方：http://mirror.rc.usf.edu/compute_lock/elrepo/kernel/el7/x86_64/RPMS/

官方项目地址：http://elrepo.org/tiki/tiki-index.php

操作系统：CentOS7 64bit

centos 查看操作系统版本信息主要有以下几种方式：

a、通过 cat /proc/version 、uname

b、通过cat /etc/issue 、cat /etc/redhat-release

c、查看64位还是32位：

getconf LONG_BIT

d、使用 file /bin/ls

使用 file /bin/ls

先安装gcc、g++编译器

yum install gcc

yum install gcc-c++ bzip2 lbzip2

gcc：4.8.5

1、下载源码

wget http://ftp.gnu.org/gnu/gcc/gcc-4.9.4/gcc-4.9.4.tar.bz2（如果需安装其他版本修改版本号即可）

2、解压文件

tar xfv gcc-4.9.4.tar.bz2

3、下载依赖文件

cd gcc-4.9.4 ///注意，要在gcc根目录执行

./contrib/download_prerequisites

如果连接失败，无法下载的话，就打开此文件，手动下载下面5个文件，然后将文件放在gcc根目录，再屏蔽contrib/download_prerequisites文件里面的wget操作，再重新执行一次./contrib/download_prerequisites。这样的话，后面编译gcc时，这几个依赖库会自动先编译，不用自动手动一个个编译。

cloog-0.18.1.tar.gz

gmp-4.3.2.tar.bz2

isl-0.12.2.tar.bz2

mpc-0.8.1.tar.gz

mpfr-2.4.2.tar.bz2

4、创建GCC临时编译目录

cd ..

mkdir build-gcc

创建与gcc根目录平级的临时目录

5、编译GCC

cd build-gcc


../gcc-4.9.4/configure --enable-checking=release --enable-languages=c,c++ --disable-multilib

make -j8 // -j利用多核处理器加快速度，机器核数*2

make install

 

gcc 编译配置参数说明:

--enable-languages //指定 gcc 能编译哪些语言的文件，每种语言用逗号分隔, 例如 c,c++,Java

--disable-multilib //默认gcc 能在32位系统上将代码编译成64位程序，或者在64位系统上编译成32位程序，如果加上这个编译选项则表示关闭这个gcc的交叉编译功能。

 

6、在~/.bash_profile配置库文件和头文件路径

exportLD_LIBRARY_PATH=/usr/local/lib:/usr/local/lib64/:$LD_LIBRARY_PATH

exportC_INCLUDE_PATH=/usr/local/include/:$C_INCLUDE_PATH

exportCPLUS_INCLUDE_PATH=/usr/local/include/:$CPLUS_INCLUDE_PATH

centos7升级GCC4.8.5到GCC4.9.0：

https://blog.csdn.net/guo_lei_lamant/article/details/79591986

centos安装高版本的gcc：

http://www.cnblogs.com/zhming26/p/6691465.html
