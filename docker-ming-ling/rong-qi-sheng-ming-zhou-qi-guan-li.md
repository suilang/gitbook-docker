# 容器生命周期管理

## **docker run ：**创建一个新的容器并运行一个命令

#### 语法

```text
docker run [OPTIONS] IMAGE [COMMAND] [ARG...]
```

OPTIONS说明：

* **-a stdin:** 指定标准输入输出内容类型，可选 STDIN/STDOUT/STDERR 三项；
* **-d:** 后台运行容器，并返回容器ID；
* **-i:** 以交互模式运行容器，通常与 -t 同时使用；
* **-P:** 随机端口映射，容器内部端口**随机**映射到主机的高端口
* **-p:** 指定端口映射，格式为：主机\(宿主\)端口:容器端口
* **-t:** 为容器重新分配一个伪输入终端，通常与 -i 同时使用；
* **--name="nginx-lb":** 为容器指定一个名称；
* **--dns 8.8.8.8:** 指定容器使用的DNS服务器，默认和宿主一致；
* **--dns-search example.com:** 指定容器DNS搜索域名，默认和宿主一致；
* **-h "mars":** 指定容器的hostname；
* **-e username="ritchie":** 设置环境变量；
* **--env-file=\[\]:** 从指定文件读入环境变量；
* **--cpuset="0-2" or --cpuset="0,1,2":** 绑定容器到指定CPU运行；
* **-m :**设置容器使用内存最大值；
* **--net="bridge":** 指定容器的网络连接类型，支持 bridge/host/none/container: 四种类型；
* **--link=\[\]:** 添加链接到另一个容器；
* **--expose=\[\]:** 开放一个端口或一组端口；
* **--volume , -v:** 绑定一个卷

#### 实例

使用docker镜像nginx:latest以后台模式启动一个容器,并将容器命名为mynginx。

```text
docker run --name mynginx -d nginx:latest
```

使用镜像nginx:latest以后台模式启动一个容器,并将容器的80端口映射到主机随机端口。

```text
docker run -P -d nginx:latest
```

使用镜像 nginx:latest，以后台模式启动一个容器,将容器的 80 端口映射到主机的 80 端口,主机的目录 /data 映射到容器的 /data。

```text
docker run -p 80:80 -v /data:/data -d nginx:latest
```

绑定容器的 8080 端口，并将其映射到本地主机 127.0.0.1 的 80 端口上。

```text
$ docker run -p 127.0.0.1:80:8080/tcp ubuntu bash
```

使用镜像nginx:latest以交互模式启动一个容器,在容器内执行/bin/bash命令。

```text
runoob@runoob:~$ docker run -it nginx:latest /bin/bash
root@b8573233d675:/# 
```

## Docker start/stop/restart 命令

[![ Docker &#x547D;&#x4EE4;&#x5927;&#x5168;](https://www.runoob.com/images/up.gif)Docker 命令大全](https://www.runoob.com/docker/docker-command-manual.html)

**docker start** :启动一个或多个已经被停止的容器

**docker stop** :停止一个运行中的容器

**docker restart** :重启容器

#### 语法

```text
docker start [OPTIONS] CONTAINER [CONTAINER...]
```

```text
docker stop [OPTIONS] CONTAINER [CONTAINER...]
```

```text
docker restart [OPTIONS] CONTAINER [CONTAINER...]
```

#### 实例

启动已被停止的容器myrunoob

```text
docker start myrunoob
```

停止运行中的容器myrunoob

```text
docker stop myrunoob
```

重启容器myrunoob

```text
docker restart myrunoob
```

