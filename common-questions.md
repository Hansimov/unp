# 常见问题

## 初始化项目

首先将随书源码下载到本地：

* [https://github.com/unpbook/unpv13e](https://github.com/unpbook/unpv13e)

然后根据项目的 README 开始配置

* [https://github.com/unpbook/unpv13e/blob/master/README](https://github.com/unpbook/unpv13e/blob/master/README)

在 Ubuntu 18.04.1 环境下，依次执行如下命令：（其他 Unix 系统会有所不同，详见 README）

```bash
./configure

cd lib
make

cd ../libfree
make

cd ../intro
make daytimetcpcli

./daytimetcpcli 127.0.0.1
```

运行最后一行时，有可能会出现如下报错：

```text
connect error: Connection refused
```

原因是没有安装 xinetd，这是一个运行于类 Unix 操作系统的超级服务器守护进程。只需运行如下命令安装：

```bash
sudo apt-get install xinetd
```

并修改配置文件中的内容：

```bash
sudo subl /etc/xinetd.d/daytime
```

将 TCP 和 UDP 下的 disable 均从 yes 改为 no：

```bash
# This is the tcp version.
...
disable		= no
...
# This is the udp version.
...
disable		= no
...
```

重启 xinetd 服务：

```bash
sudo /etc/init.d/xinetd restart
```

再次运行，可以得到如下结果：

```bash
xxx@ubuntu:***/src/intro$ ./daytimetcpcli 127.0.0.1
23 NOV 2020 23:40:09 CST
```

### 参考链接

* unpbook/unpv13e: UNIX Network Programming, Volume 1, Third Edition Source Code 
  * [https://github.com/unpbook/unpv13e](https://github.com/unpbook/unpv13e)
* UNP环境配置 - thcarl - 博客园 
  * [https://www.cnblogs.com/thecarl/p/4471765.html](https://www.cnblogs.com/thecarl/p/4471765.html)
* UNP源码使用及编译\_jjcoder的专栏-CSDN博客 
  * [https://blog.csdn.net/u010956473/article/details/76218130](https://blog.csdn.net/u010956473/article/details/76218130)

