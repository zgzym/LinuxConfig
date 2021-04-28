首先在站长工具网站查询访问github.com最快的IP地址

*http://tool.chinaz.com/dns?type=1&host=github.com&ip=*

找到TTL值最小的IP,例如：192.30.255.112

按windows+R，输入c:\windows\system32\drivers\etc，

进入/etc文件夹后，编辑hosts文件。

在hosts文件最后一行加入

```c
# 192.30.255.112 https://github.com
```
