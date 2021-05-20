本人在配置共享文件夹失败后，重启centos7，系统进入了Emergency mode，输入下面命令然后重启即可：

xfs_repair -v -L /dev/dm-0
