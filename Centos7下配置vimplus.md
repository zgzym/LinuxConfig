1.	配置Vimplus

建议在root用户下安装，在其他用户下有可能安装插件失败，其它用户要使用vimplus也需要单独安装。

然后输入命令：yum install git安装git；

输入命令：
```c++
  git clone git://github.com/chxuan/vimplus.git ~/.vimplus
  cd ~/.vimplus
  cd autoload/
  vi plug.vim
```
将该行:
```c++
  let fmt = get(g:, 'plug_url_format', 'https://git::@github.com/%s.git')
``` 
改为:
```c++
  let fmt = get(g:, 'plug_url_format', 'https://git::@hub.fastgit.org/%s.git')
```
将

   \ '^https://git::@github\.com', 'https://github.com', '')

改为

   \ '^https://git::@hub.fastgit\.org', 'https://hub.fastgit.org', '')

保存并退出。

返回~/.vimplus，执行安装：

	./install.sh
