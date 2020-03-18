# docker 容器使用

## Docker 客户端

docker 客户端非常简单 ,我们可以直接输入 docker 命令来查看到 Docker 客户端的所有命令选项。

```text
runoob@runoob:~# docker
```

通过命令 **docker command --help** 更深入的了解指定的 Docker 命令使用方法。

例如我们要查看 **docker stats** 指令的具体使用方法：

```text
runoob@runoob:~# docker stats --help
```

## 容器使用

### 1. 获取镜像

如果我们本地没有 ubuntu 镜像，我们可以使用 docker pull 命令来载入 ubuntu 镜像：

```text
$ docker pull ubuntu
```

### 启动容器

以下命令使用 ubuntu 镜像启动一个容器，参数为以命令行模式进入该容器：

```text
$ docker run -it ubuntu /bin/bash
```

![](https://www.runoob.com/wp-content/uploads/2016/05/docker-container-run.png)

参数说明：

* **-i**: 交互式操作。
* **-t**: 终端。
* **ubuntu**: ubuntu 镜像。
* **/bin/bash**：放在镜像名后的是命令，这里我们希望有个交互式 Shell，因此用的是 /bin/bash。

要退出终端，直接输入 **exit**:

```text
root@ed09e4490c57:/# exit
```

![](https://www.runoob.com/wp-content/uploads/2016/05/docker-container-exit.png)

### 查看所有的容器命令如下：

```text
$ docker ps -a
```

### 后台运行

在大部分的场景下，我们希望 docker 的服务是在后台运行的，我们可以过 -d 指定容器的运行模式。

```text
$ docker run -itd --name ubuntu-test ubuntu /bin/bash
```

**注：**加了 -d 参数默认不会进入容器，想要进入容器需要使用指令 **docker exec**（下面会介绍到）。

### 停止一个容器

停止容器的命令如下：

```text
$ docker stop <容器 ID>
```

![](https://www.runoob.com/wp-content/uploads/2016/05/docker-stop-1.png)

停止的容器可以通过 docker restart 重启：

```text
$ docker restart <容器 ID>
```

### 进入容器

在使用 **-d** 参数时，容器启动后会进入后台。此时想要进入容器，可以通过以下指令进入：

* **docker attach**
* **docker exec**：推荐大家使用 docker exec 命令，因为此退出容器终端，不会导致容器的停止。



#### **attach 命令**

下面演示了使用 docker attach 命令。

```text
$ docker attach 1e560fca3906 
```

[![](https://www.runoob.com/wp-content/uploads/2016/05/docker-attach.png)](https://www.runoob.com/wp-content/uploads/2016/05/docker-attach.png)

**注意：** 如果从这个容器退出，会导致容器的停止。

**exec 命令**

下面演示了使用 docker exec 命令。

```text
docker exec -it 243c32535da7 /bin/bash
```

[![](https://www.runoob.com/wp-content/uploads/2016/05/docker-exec.png)](https://www.runoob.com/wp-content/uploads/2016/05/docker-exec.png)

**注意：** 如果从这个容器退出，不会导致容器的停止，这就是为什么推荐大家使用 **docker exec** 的原因。

更多参数说明请使用 docker exec --help 命令查看。

### 导出和导入容器

**导出容器**

如果要导出本地某个容器，可以使用 **docker export** 命令。

```text
$ docker export 1e560fca3906 > ubuntu.tar
```

导出容器 1e560fca3906 快照到本地文件 ubuntu.tar。

**导入容器快照**

可以使用 docker import 从容器快照文件中再导入为镜像，以下实例将快照文件 ubuntu.tar 导入到镜像 test/ubuntu:v1:

```text
$ cat docker/ubuntu.tar | docker import - test/ubuntu:v1
```

[![](https://www.runoob.com/wp-content/uploads/2016/05/docker-import.png)](https://www.runoob.com/wp-content/uploads/2016/05/docker-import.png)

此外，也可以通过指定 URL 或者某个目录来导入，例如：

```text
$ docker import http://example.com/exampleimage.tgz example/imagerepo
```

### 删除容器

删除容器使用 **docker rm** 命令：

```text
$ docker rm -f 1e560fca3906
```

下面的命令可以清理掉所有处于终止状态的容器。

`$ docker container prune`

### 查看应用程序日志

docker logs \[ID或者名字\] 可以查看容器内部的标准输出。

```text
runoob@runoob:~$ docker logs -f bf08b7f2cd89
```

**-f:** 让 **docker logs** 像使用 **tail -f** 一样来输出容器内部的标准输出。



