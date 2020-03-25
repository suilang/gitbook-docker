# 本地镜像管理

### **docker images :** 列出本地镜像。

#### 语法

```text
docker images [OPTIONS] [REPOSITORY[:TAG]]
```

OPTIONS说明：

* **-a :**列出本地所有的镜像（含中间映像层，默认情况下，过滤掉中间映像层）；
* **--digests :**显示镜像的摘要信息；
* **-f :**显示满足条件的镜像；
* **--format :**指定返回值的模板文件；
* **--no-trunc :**显示完整的镜像信息；
* **-q :**只显示镜像ID。

### **docker rmi :** 删除本地一个或多少镜像。

#### 语法

```text
docker rmi [OPTIONS] IMAGE [IMAGE...]
```

OPTIONS说明：

* **-f :**强制删除；
* **--no-prune :**不移除该镜像的过程镜像，默认移除；

### **docker tag :** 标记本地镜像，将其归入某一仓库。

#### 语法

```text
docker tag [OPTIONS] IMAGE[:TAG] [REGISTRYHOST/][USERNAME/]NAME[:TAG]
```

#### 实例

将镜像ubuntu:15.10标记为 runoob/ubuntu:v3 镜像。

```text
root@runoob:~# docker tag ubuntu:15.10 runoob/ubuntu:v3
```



### **docker build** 命令用于使用 Dockerfile 创建镜像。

#### 语法

```text
docker build [OPTIONS] PATH | URL | -
```

OPTIONS说明：

* **--build-arg=\[\] :**设置镜像创建时的变量；
* **--cpu-shares :**设置 cpu 使用权重；
* **--cpu-period :**限制 CPU CFS周期；
* **--cpu-quota :**限制 CPU CFS配额；
* **--cpuset-cpus :**指定使用的CPU id；
* **--cpuset-mems :**指定使用的内存 id；
* **--disable-content-trust :**忽略校验，默认开启；
* **-f :**指定要使用的Dockerfile路径；
* **--force-rm :**设置镜像过程中删除中间容器；
* **--isolation :**使用容器隔离技术；
* **--label=\[\] :**设置镜像使用的元数据；
* **-m :**设置内存最大值；
* **--memory-swap :**设置Swap的最大值为内存+swap，"-1"表示不限swap；
* **--no-cache :**创建镜像的过程不使用缓存；
* **--pull :**尝试去更新镜像的新版本；
* **--quiet, -q :**安静模式，成功后只输出镜像 ID；
* **--rm :**设置镜像成功后删除中间容器；
* **--shm-size :**设置/dev/shm的大小，默认值是64M；
* **--ulimit :**Ulimit配置。
* **--tag, -t:** 镜像的名字及标签，通常 name:tag 或者 name 格式；可以在一次构建中为一个镜像设置多个标签。
* **--network:** 默认 default。在构建期间设置RUN指令的网络模式

#### 实例

使用当前目录的 Dockerfile 创建镜像，标签为 runoob/ubuntu:v1。

```text
docker build -t runoob/ubuntu:v1 . 
```

使用URL **github.com/creack/docker-firefox** 的 Dockerfile 创建镜像。

```text
docker build github.com/creack/docker-firefox
```

也可以通过 -f Dockerfile 文件的位置：

```text
$ docker build -f /path/to/a/Dockerfile .
```

在 Docker 守护进程执行 Dockerfile 中的指令前，首先会对 Dockerfile 进行语法检查，有语法错误时会返回：

```text
$ docker build -t test/myapp .
Sending build context to Docker daemon 2.048 kB
Error response from daemon: Unknown instruction: RUNCMD
```



### **docker history :** 查看指定镜像的创建历史。

#### 语法

```text
docker history [OPTIONS] IMAGE
```

OPTIONS说明：

* **-H :**以可读的格式打印镜像大小和日期，默认为true；
* **--no-trunc :**显示完整的提交记录；
* **-q :**仅列出提交记录ID。

#### 实例

查看本地镜像runoob/ubuntu:v3的创建历史。

```text
root@runoob:~# docker history runoob/ubuntu:v3
IMAGE             CREATED           CREATED BY                                      SIZE      COMMENT
4e3b13c8a266      3 months ago      /bin/sh -c #(nop) CMD ["/bin/bash"]             0 B                 
<missing>         3 months ago      /bin/sh -c sed -i 's/^#\s*\(deb.*universe\)$/   1.863 kB            
<missing>         3 months ago      /bin/sh -c set -xe   && echo '#!/bin/sh' > /u   701 B               
<missing>         3 months ago      /bin/sh -c #(nop) ADD file:43cb048516c6b80f22   136.3 MB
```



### **docker save :** 将指定镜像保存成 tar 归档文件。

#### 语法

```text
docker save [OPTIONS] IMAGE [IMAGE...]
```

OPTIONS 说明：

* **-o :**输出到的文件。

#### 实例

将镜像 runoob/ubuntu:v3 生成 my\_ubuntu\_v3.tar 文档

```text
runoob@runoob:~$ docker save -o my_ubuntu_v3.tar runoob/ubuntu:v3
```



### **docker load :** 导入使用 [docker save](https://www.runoob.com/docker/docker-save-command.html) 命令导出的镜像。

#### 语法

```text
docker load [OPTIONS]
```

OPTIONS 说明：

* **--input , -i :** 指定导入的文件，代替 STDIN。
* **--quiet , -q :** 精简输出信息。

#### 实例

导入镜像：

```text
$ docker load < busybox.tar.gz
```



### **docker import :** 从归档文件中创建镜像。

#### 语法

```text
docker import [OPTIONS] file|URL|- [REPOSITORY[:TAG]]
```

OPTIONS说明：

* **-c :**应用docker 指令创建镜像；
* **-m :**提交时的说明文字；

#### 实例

从镜像归档文件my\_ubuntu\_v3.tar创建镜像，命名为runoob/ubuntu:v4

```text
runoob@runoob:~$ docker import  my_ubuntu_v3.tar runoob/ubuntu:v4  
```



