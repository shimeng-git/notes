## shell常用变量/常量

关于`shell`脚本脚本所在目录，参考这篇文章：[获取shell脚本目录](https://www.junmajinlong.com/shell/get_script_dir/)。

获取脚本所在路径，直接在脚本中使用pwd命令是不可行的，pwd获取的是当前工作目录的路径。例如在`/tmp`目录下执行`~/junma/a.sh时，a.sh`中的`pwd`将输出`/tmp`。同样也不能在脚本中使用`dirname $0`来获取该脚本的路径。因为如果脚本`a.sh`是在脚本`c.sh`中被`source`加载的，那么`a.sh`中的`$0`将是c.sh，`dirname $0`获取到的将是`c.sh`所在的目录。

```shell
$(dirname "$(realpath "${BASH_SOURCE[0]}")
```



`iconv`命令用于转换文件编码。一般格式“`iconv -f encoding -t encoding`。同时，`C语言`中有`iconv`函数可以完成字符编码的转换

```shell
cat log | grep 'filter' | iconv -f gb18030 -t utf-8
# 不加 -o 选项则输出到标准输出
iconv src_file -f utf-8 -t gb2312 -o dst_file

# 常用选项
-f encoding :把字符从encoding编码开始转换。 
-t encoding :把字符转换到encoding编码。 
-l :列出已知的编码字符集合 
-o file :指定输出文件 
-c :忽略输出的非法字符 
-s :禁止警告信息，但不是错误信息 
--verbose :显示进度信息 
-f和-t所能指定的合法字符在-l选项的命令里面都列出来了。 
```



### PS

`ps`命令用于获取程序执行快照。由于`ps`命令存在时间较长，在`linux`, `unix`等系统中都支持，因此存在一些历史问题，主要是包含多种风格的命令选项，因此存在不同命令选项执行结果几乎没有区别的现象。[很详细的ps命令介绍](https://juejin.cn/post/6844903938144075783)，其中有一部分细节较多，留用察看。

```shell

ps u #BSD 风格语法，必须不能以中横线开头；
ps -l #SYSV 风格语法，必须仅一个中横线开头；
ps --pid 1 #GNU 风格语法，必须以两个中横线开头；几乎不用

# 解析BSD和SYSV风格的命令时会将字符串解析成单独字母
ps -ef 		<--> ps -e -f
ps -el en <--> ps -e -l e n


选项 - e：显示所有进程的记录，记住这个参数就可以保证把当前系统的所有进程都输出。需要筛选进程时，可以结合 grep 等文本处理命令实现目的。

选项 h：选中时可以隐藏输出结果的标题栏信息，在一些自动化脚本中使用此参数可以去除页头信息。

选项 k：通过此选项可以实现对输出结果的排序。

选项 - L：通过此选项可以把多线程的进程展开每个线程的细颗粒度。

选项 - l：或选项 l，此选项可以列出进程的最基本信息，包括 s、pid、ppid、time 和 ucmd 等字段信息。

选项 u：此选项可以列出 cpu 使用率、mem 使用率、rss 内存等字段信息。

选项 - o：或选项 o，通过此选项可以自定义输出符合自己需求的字段信息。

各列信息：
UID //用户ID、但输出的是用户名
PID //进程的ID
PPID //父进程ID
C //进程占用CPU的百分比
STIME //进程启动时间
TTY //该进程在那个终端上运行，若与终端无关，则显示? 若为pts/0等，则表示由网络连接主机进程。
TIME //进程使用cpu的时间
CMD //命令的名称和参数
```



## touch

`touch`一般用于修改时间戳或者创建一个空文件。如果文件不存在则创建空文件，否则修改时间戳。

```shell
touch filename
stat filename	#检查时间戳

-c   或--no-create 　不建立任何文档。
-d 　使用指定的日期时间，而非现在的时间。
-f 　此参数将忽略不予处理，仅负责解决BSD版本touch指令的兼容性问题。
-m   或--time=mtime或--time=modify 　只更改变动时间。
-r 　把指定文档或目录的日期时间，统统设成和参考文档或目录的日期时间相同。
-t 　使用指定的日期时间，而非现在的时间。


```

