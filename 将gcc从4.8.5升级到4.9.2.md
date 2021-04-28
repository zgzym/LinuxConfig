Centos7自带的gcc版本为gcc-4.8.5，该版本不支持正则表达式，

因此需要将其版本更新至gcc-4.9.2.

首先安装gcc的依赖包：

```c
    sudo yum install libmpc-devel mpfr-devel gmp-devel
```
接着下列网址下载源码包：
	*ftp://ftp.mirrorservice.org/sites/sourceware.org/pub/gcc/releases/gcc-4.9.2/gcc-4.9.2.tar.bz2*
	
将下载的源码包放在Linux系统的/Downloads目录下；

解压并安装：
```c
	tar xvfj gcc-4.9.2.tar.bz2
	
	cd gcc-4.9.2
	
	./configure --disable-multilib --enable-languages=c,c++
	
	make -j 4
	
	make install
```
