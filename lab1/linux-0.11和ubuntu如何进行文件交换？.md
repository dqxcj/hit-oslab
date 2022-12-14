> 本文由 [简悦 SimpRead](http://ksria.com/simpread/) 转码， 原文地址 [www.lanqiao.cn](https://www.lanqiao.cn/courses/115/learning/?id=374&compatibility=false)

> 蓝桥云课是国内领先的 IT 在线编程及在线实训学习平台，专业导师提供精选的实践项目，创新的技术使得学习者无需配置繁琐的本地环境，随时在线流畅使用。

接下来讲解一下 Ubuntu 和 Linux 0.11 之间的文件交换如何启动。

> 开始设置文件交换之前，务必关闭所有的 Bochs 进程。

oslab 下的 `hdc-0.11-new.img` 是 0.11 内核启动后的根文件系统镜像文件，相当于在 bochs 虚拟机里装载的硬盘。在 Ubuntu 上访问其内容的方法是：

```
$ cd ~/oslab/

# 启动挂载脚本
$ sudo ./mount-hdc
```

> 大家使用 sudo 时，password 是 `shiyanlou`，也有可能不会提示输入密码。

之后，hdc 目录下就是和 0.11 内核一模一样的文件系统了，可以读写任何文件（可能有些文件要用 sudo 才能访问）。

```
# 进入挂载到 Ubuntu 上的目录
$ cd ~/oslab/hdc

# 查看内容
$ ls -al
```

读写完毕，不要忘了卸载这个文件系统：

```
$ cd ~/oslab/

# 卸载
$ sudo umount hdc
```

接下来，我们简单实验一下。

首先通过 `sudo ./mount-hdc` 进行挂载。

然后在 Ubuntu 的 `~/oslab/hdc/usr/root` 目录下创建一个 xxx.c 文件，

```
sudo gedit ~/oslab/hdc/usr/root/xxx.c
```

编辑内容之后记得保存。

最后执行 `sudo umount hdc` 后，再进入 Linux 0.11（即 run 启动 bochs 以后）就会看到这个 xxx.c（即如下图所示）。

这样就避免了在 Linux 0.11 上进行编辑 xxx.c 的麻烦，因为 Linux 0.11 作为一个很小的操作系统，其上的编辑工具只有 vi，使用起来非常不便。

![](https://doc.shiyanlou.com/userid19614labid568time1423993300541)

图 2 用 Ubuntu 和 Linux 0.11 完成文件交换以后再启动 Linux 0.11 以后

另外在 Linux 0.11 上产生的文件，如后面实验中产生的 `process.log` 文件，可以按这种方式 “拿到” Ubuntu 下用 python 程序进行处理，当然这个 python 程序在 Linux 0.11 上显然是不好使的，因为 Linux 0.11 上搭建不了 python 解释环境。

> 注意 1：不要在 0.11 内核运行的时候 mount 镜像文件，否则可能会损坏文件系统。同理，也不要在已经 mount 的时候运行 0.11 内核。
> 
> 注意 2：在关闭 Bochs 之前，需要先**在 0.11 的命令行运行 “sync”，确保所有缓存数据都存盘**后，再关闭 Bochs。