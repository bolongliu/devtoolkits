# Linux 命令行操作

## 1. ubuntu杀死含有指定字符串的的一系列进程

```shell
ps -ef|grep strName|grep -v grep|cut -c 9-16|xargs kill -9
```
使用时，将strName换为指定的字符串，管道符 | 左边的执行结果作为右边的输入，其中各项指令表示的含义如下：

ps -ef：Linux系统中列出所有的进程

grep strName： 过滤出进程名字中包含strName的进程

grep -v grep： 过滤掉包含grep的进程

cut -c 9-16： 截取每一行进程信息的第9-16个字节，即PID号

xargs kill -9：输入kill -9的作为参数，将这些进程杀死
