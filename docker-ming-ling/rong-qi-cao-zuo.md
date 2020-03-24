# 容器操作

### **docker ps :** 列出容器

#### 语法

```text
docker ps [OPTIONS]
```

OPTIONS说明：

* **-a :**显示所有的容器，包括未运行的。
* **-f :**根据条件过滤显示的内容。
* **--format :**指定返回值的模板文件。
* **-l :**显示最近创建的容器。
* **-n :**列出最近创建的n个容器。
* **--no-trunc :**不截断输出。
* **-q :**静默模式，只显示容器编号。
* **-s :**显示总的文件大小。

### **docker inspect :** 获取容器/镜像的元数据。

#### 语法

```text
docker inspect [OPTIONS] NAME|ID [NAME|ID...]
```

OPTIONS说明：

* **-f :**指定返回值的模板文件。
* **-s :**显示总的文件大小。
* **--type :**为指定类型返回JSON。

获取正在运行的容器mymysql的 IP。

```text
docker inspect --format='{{range .NetworkSettings.Networks}}{{.IPAddress}}{{end}}' mymysql
```

### **docker top :**查看容器中运行的进程信息，支持 ps 命令参数。

#### 语法

```text
docker top [OPTIONS] CONTAINER [ps OPTIONS]
```

容器运行时不一定有/bin/bash终端来交互执行top命令，而且容器还不一定有top命令，可以使用docker top来实现查看container中正在运行的进程。

#### 实例

查看容器mymysql的进程信息。

```text
runoob@runoob:~/mysql$ docker top mymysql
UID    PID    PPID    C      STIME   TTY  TIME       CMD
999    40347  40331   18     00:58   ?    00:00:02   mysqld
```

查看所有运行容器的进程信息。

```text
for i in  `docker ps |grep Up|awk '{print $1}'`;do echo \ &&docker top $i; done
```

### **docker attach :**连接到正在运行中的容器。

#### 语法

```text
docker attach [OPTIONS] CONTAINER
```

要attach上去的容器必须正在运行，可以同时连接上同一个container来共享屏幕（与screen命令的attach类似）。

官方文档中说attach后可以通过CTRL-C来detach，如果container当前在运行bash，CTRL-C自然是当前行的输入，没有退出；如果container当前正在前台运行进程，如输出nginx的access.log日志，CTRL-C不仅会导致退出容器，而且还stop了。这不是我们想要的，detach的意思按理应该是脱离容器终端，但容器依然运行。好在attach是可以带上--sig-proxy=false来确保CTRL-D或CTRL-C不会关闭容器。

#### 实例

容器mynginx将访问日志指到标准输出，连接到容器查看访问信息。

```text
runoob@runoob:~$ docker attach --sig-proxy=false mynginx
```

### **docker events :** 从服务器获取实时事件

#### 语法

```text
docker events [OPTIONS]
```

OPTIONS说明：

* **-f ：**根据条件过滤事件；
* **--since ：**从指定的时间戳后显示所有事件;
* **--until ：**流水时间显示到指定的时间为止；

#### 实例

显示docker 2016年7月1日后的所有事件。

```text
runoob@runoob:~/mysql$ docker events  --since="1467302400"
```

显示docker 镜像为mysql:5.6 2016年7月1日后的相关事件。

```text
runoob@runoob:~/mysql$ docker events -f "image"="mysql:5.6" --since="1467302400" 
```

如果指定的时间是到秒级的，需要将时间转成时间戳。如果时间为日期的话，可以直接使用，如--since="2016-07-01"。

### **docker logs :** 获取容器的日志

#### 语法

```text
docker logs [OPTIONS] CONTAINER
```

OPTIONS说明：

* **-f :** 跟踪日志输出
* **--since :**显示某个开始时间的所有日志
* **-t :** 显示时间戳
* **--tail :**仅列出最新N条容器日志

#### 实例

跟踪查看容器mynginx的日志输出。

```text
runoob@runoob:~$ docker logs -f myngin
```

查看容器mynginx从2016年7月1日后的最新10条日志。

```text
docker logs --since="2016-07-01" --tail=10 mynginx
```

### **docker wait :** 阻塞运行直到容器停止，然后打印出它的退出代码。

#### 语法

```text
docker wait [OPTIONS] CONTAINER [CONTAINER...]
```

#### 实例

```text
docker wait CONTAINER
```

### **docker export :**将文件系统作为一个tar归档文件导出到STDOUT。

#### 语法

```text
docker export [OPTIONS] CONTAINER
```

OPTIONS说明：

* **-o :**将输入内容写到文件。

#### 实例

将id为a404c6c174a2的容器按日期保存为tar文件。

```text
runoob@runoob:~$ docker export -o mysql-`date +%Y%m%d`.tar a404c6c174a2
```

**docker port :**列出指定的容器的端口映射，或者查找将PRIVATE\_PORT NAT到面向公众的端口。

#### 语法

```text
docker port [OPTIONS] CONTAINER [PRIVATE_PORT[/PROTO]]
```

#### 实例

查看容器mynginx的端口映射情况。

```text
runoob@runoob:~$ docker port mymysql
3306/tcp -> 0.0.0.0:3306
```



