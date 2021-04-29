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

此时升级gcc生成的动态库没有替换老版本的动态库，

在编译或运行程序时会出现如下错误：
```c
	/usr/lib64/libstdc++.so.6: version `GLIBCXX_3.4.20' not found
```

运行以下命令检查动态库：
```c
	strings /usr/lib64/libstdc++.so.6 | grep GLIBC
```

输出结果如下：
```c
	GLIBCXX_3.4
	GLIBCXX_3.4.1
	GLIBCXX_3.4.2
	GLIBCXX_3.4.3
	GLIBCXX_3.4.4
	GLIBCXX_3.4.5
	GLIBCXX_3.4.6
	GLIBCXX_3.4.7
	GLIBCXX_3.4.8
	GLIBCXX_3.4.9
	GLIBCXX_3.4.10
	GLIBCXX_3.4.11
	GLIBCXX_3.4.12
	GLIBCXX_3.4.13
```

可以看出没有GLIBCXX_3.4.20

接下来先找到新的动态库的位置，
```c++
	find / -name "libstdc++.so*"
```

找到
```c
	/home/user/Downloads/gcc-4.9.2/x86_64-unknown-linux-gnu/libstdc++-v3/src/.libs/libstdc++.so.6.0.20
```

将其复制到/usr/lib64目录下：
```c
	sudo cp /home/user/Downloads/gcc-4.9.2/x86_64-unknown-linux-gnu/libstdc++-v3/src/.libs/libstdc++.so.6.0.20 /usr/lib64
```

切换至目录/usr/lib64:
```c
	cd /usr/lib64
```

删除原来软连接：
```c
	rm -rf libstdc++.so.6
```
```c
将默认库的软连接指向最新动态库：
```c
	ln -s libstdc++.so.6.0.21 libstdc++.so.6
```

默认动态库升级完成。重新运行以下命令检查动态库：
```c
	strings /usr/lib64/libstdc++.so.6 | grep GLIBC
```

### 参考博客：https://blog.csdn.net/yuhuqiao/article/details/83624689
