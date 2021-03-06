# Docker 容器连接

### 网络端口映射

我们创建了一个 python 应用的容器。

```text
runoob@runoob:~$ docker run -d -P training/webapp python app.py
fce072cc88cee71b1cdceb57c2821d054a4a59f67da6b416fceb5593f059fc6d
```

可以使用 **-p** 标识来指定容器端口绑定到主机端口。

两种方式的区别是:

* **-P :**是容器内部端口**随机**映射到主机的高端口。
* **-p :** 是容器内部端口绑定到**指定**的主机端口。

```text
runoob@runoob:~$ docker run -d -p 5000:5000 training/webapp python app.py
```

可以指定容器绑定的网络地址，比如绑定 127.0.0.1。

```text
runoob@runoob:~$ docker run -d -p 127.0.0.1:5001:5000 training/webapp python app.py
```

默认都是绑定 tcp 端口，如果要绑定 UDP 端口，可以在端口后面加上 **/udp**。

```text
runoob@runoob:~$ docker run -d -p 127.0.0.1:5000:5000/udp training/webapp python app.py
```

### Docker 容器互联

端口映射并不是唯一把 docker 连接到另一个容器的方法。

docker 有一个连接系统允许将多个容器连接在一起，共享连接信息。

docker 连接会创建一个父子关系，其中父容器可以看到子容器的信息。

#### 容器命名

当我们创建一个容器的时候，docker 会自动对它进行命名。另外，我们也可以使用 **--name** 标识来命名容器，例如：

```text
runoob@runoob:~$  docker run -d -P --name runoob training/webapp python app.py
```

#### 新建网络

下面先创建一个新的 Docker 网络。

```text
$ docker network create -d bridge test-net
```

参数说明：

**-d**：参数指定 Docker 网络类型，有 bridge、overlay。

#### 连接容器

运行一个容器并连接到新建的 test-net 网络:

```text
$ docker run -itd --name test1 --network test-net ubuntu /bin/bash
```

打开新的终端，再运行一个容器并加入到 test-net 网络:

```text
$ docker run -itd --name test2 --network test-net ubuntu /bin/bash
```

### 配置 DNS

我们可以在宿主机的 /etc/docker/daemon.json 文件中增加以下内容来设置全部容器的 DNS：

```text
{
  "dns" : [
    "114.114.114.114",
    "8.8.8.8"
  ]
}
```

设置后，启动容器的 DNS 会自动配置为 114.114.114.114 和 8.8.8.8。

配置完，需要重启 docker 才能生效。

查看容器的 DNS 是否生效可以使用以下命令，它会输出容器的 DNS 信息：

```text
$ docker run -it --rm ubuntu  cat etc/resolv.conf
```

**手动指定容器的配置**

如果只想在指定的容器设置 DNS，则可以使用以下命令：

```text
$ docker run -it --rm host_ubuntu  --dns=114.114.114.114 --dns-search=test.com ubuntu
```

参数说明：

* **-h HOSTNAME 或者 --hostname=HOSTNAME**： 设定容器的主机名，它会被写到容器内的 /etc/hostname 和 /etc/hosts。
* **--dns=IP\_ADDRESS**： 添加 DNS 服务器到容器的 /etc/resolv.conf 中，让容器用这个服务器来解析所有不在 /etc/hosts 中的主机名。
* **--dns-search=DOMAIN**： 设定容器的搜索域，当设定搜索域为 .example.com 时，在搜索一个名为 host 的主机时，DNS 不仅搜索 host，还会搜索 host.example.com。



