### 本文参考博客https://blog.csdn.net/jiao_mrswang/article/details/99288762

以下所有命令均在root用户下

1. 首先安装cmake,cmake的版本要求在3.15.1以上，在这里我们安装CMake3.15.5
	
	1.1 首先安装gcc
	```c++
		yum -y install gcc gcc_c++
	```
		其中，参数-y表示在安装过程中默认选择“yes"
		
	1.2 获取源码
	```c++
		wget https://down.24kplus.com/linux/cmake/cmake-3.15.5.tar.gz
	```
	1.3 解压压缩包
	```c++
		tar -zxf cmake-3.15.5.tar.gz
	```
	1.4 进入解压后的目录
	```c++
		cd cmake-3.15.5
	```
	1.5 编译并安装
	```c++
		./bootstrap --prefix=/usr --datadir=share/cmake --docdir=doc/cmake && make
		
		sudo make install
	```
	1.6 检查版本
	```c++
		cmake --version
	```

2 安装opencv4所依赖的库
```c++
	2.1 yum install gcc gcc-c++ kernel-devel
	
	2.2 yum install gcc-gfortran
	
	2.3 yum install git
	
	2.4 yum install libgnomeui-devel
	
	2.5 yum install gtk2 gtk2-devel gtk2-devel-docs
	
	2.6 yum install gnome-devel gnome-devel-docs
	
	2.7 pkg-config --version （查看pky-config版本，若没有安装则先安装pkg-config）
	
	2.8 yum -y install epel-release
	
	2.9 yum localinstall --nogpgcheck https://download1.rpmfusion.org/free/el/rpmfusion-free-release-7.noarch.rpm 

	2.10 yum localinstall –-nogpgcheck https://download1.rpmfusion.org/nonfree/el/rpmfusion-nonfree-release-7.noarch.rpm 
	
	2.11 rpm –-import http://li.nux.ro/download/nux/RPM-GPG-KEY-nux.ro 
	
	2.12 rpm -Uvh http://li.nux.ro/download/nux/dextop/el7/x86_64/nux-dextop-release-0-1.el7.nux.noarch.rpm

	2.13 yum -y install ffmpeg ffmpeg-devel
	
	2.14 ffmpeg --version （检查ffmpeg是否成功安装）
	
	2.15 yum install python-devel numpy

	2.16 yum install libdc1394-devel

	2.17 yum install libv4l-devel
	
	2.18 yum install gstreamer-plugins-base-devel
```

3 下载opencv4.1.0安装包，下载地址：https://opencv.org/releases/page/3/，下载完成后拷贝到Linux中
	
	3.1 解压压缩包，得到opencv-4.1.0/文件夹
	
	3.2 进入opencv-4.1.0/目录，输入下面命令编译并安装：
	```c++
		cd opencv-4.1.0/

		mkdir build
		
		cd build/
		
		cmake  -D CMAKE_BUILD_TYPE=RELEASE -D OPENCV_GENERATE_PKGCONFIG=ON -D CMAKE_INSTALL_PREFIX=/usr/local ..

		make -j8 （表示并行8个编译命令）

		sudo make install
	```

4 配置opencv4环境

	4.1 找到opencv4.pc所在目录
	```c++
		sudo find / -iname opencv4.pc
	```
		所在目录类似于：/usr/local/lib64/pkgconfig/opencv4.pc
	
	4.2 将opencv4.pc的路径添加到PKG_CONFIG_PATH:
	```c++
		vi /etc/profile.d/pkgconfig.sh
	```
	添加一行：export PKG_CONFIG_PATH=/usr/local/lib64/pkgconfig:$PKG_CONFIG_PATH
	
	保存并退出。
	
	4.3 使修改生效
	```c++
		source /etc/profile
	```
	注意，每个命令终端都需要输入这个命令才能生效
	
	4.4 配置编译环境
	```c++
		vi /etc/ld.so.conf.d/opencv4.conf
	```
	添加一行：/usr/local/lib64
	
	保存并退出，然后生效配置：
	```c++
		ldconfig
	``` 
	4.5 检查opencv的版本
	```c++
		pkg-config --modversion opencv4
	``` 
	如果显示4.1.0，则表示安装成功

5 测试opencv4是否正常运行

	5.1 进入sample文件目录下
	```c++
		/opencv-4.1.0/samples/cpp/example_cmake
	``` 
	5.2 修改Makefile文件
	```c++
		vi Makefile
	``` 
	
![1fd](https://github.com/zgzym/LinuxConfig/blob/main/images/opencv4_1.png)
	
	保存并退出。
	
	5.3 输入下面命令，若出现hello opencv的图片，则说明opencv4可以正常运行
	```c++
		make
		
		./opencv_example
	``` 
