# docker web应用

## 运行一个 web 应用

前面我们运行的容器并没有一些什么特别的用处。

接下来让我们尝试使用 docker 构建一个 web 应用程序。

我们将在docker容器中运行一个 Python Flask 应用来运行一个web应用。

```text
runoob@runoob:~# docker pull training/webapp  # 载入镜像
runoob@runoob:~# docker run -d -P training/webapp python app.py
```

![](https://www.runoob.com/wp-content/uploads/2016/05/docker29.png)

参数说明:

* **-d:**让容器在后台运行。
* **-P:**将容器内部使用的网络端口映射到我们使用的主机上。

### 查看 WEB 应用容器

使用 docker ps 来查看我们正在运行的容器：

```text
runoob@runoob:~#  docker ps
CONTAINER ID        IMAGE               COMMAND             ...        PORTS                 
d3d5e39ed9d3        training/webapp     "python app.py"     ...        0.0.0.0:32769->5000/tcp
```

这里多了端口信息。

```text
PORTS
0.0.0.0:32769->5000/tcp
```

Docker 开放了 5000 端口（默认 Python Flask 端口）映射到主机端口 32769 上。

我们也可以通过 -p 参数来设置不一样的端口：

```text
runoob@runoob:~$ docker run -d -p 5000:5000 training/webapp python app.py
```

容器内部的 5000 端口映射到我们本地主机的 5000 端口上。

### 网络端口的快捷方式

通过 **docker ps** 命令可以查看到容器的端口映射，**docker** 还提供了另一个快捷方式 **docker port**，使用 **docker port** 可以查看指定 （ID 或者名字）容器的某个确定端口映射到宿主机的端口号。

上面我们创建的 web 应用容器 ID 为 **bf08b7f2cd89** 名字为 **wizardly\_chandrasekhar**。

我可以使用 docker port bf08b7f2cd89 或 docker port wizardly\_chandrasekhar 来查看容器端口的映射情况。

### 查看 WEB 应用程序日志

docker logs \[ID或者名字\] 可以查看容器内部的标准输出。

```text
runoob@runoob:~$ docker logs -f bf08b7f2cd89
```

### 查看WEB应用程序容器的进程

我们还可以使用 docker top 来查看容器内部运行的进程

```text
runoob@runoob:~$ docker top wizardly_chandrasekhar
UID     PID         PPID          ...       TIME                CMD
root    23245       23228         ...       00:00:00            python app.py
```

### 检查 WEB 应用程序

使用 **docker inspect** 来查看 Docker 的底层信息。它会返回一个 JSON 文件记录着 Docker 容器的配置和状态信息。

```text
runoob@runoob:~$ docker inspect wizardly_chandrasekhar
[
    {
        "Id": "bf08b7f2cd897b5964943134aa6d373e355c286db9b9885b1f60b6e8f82b2b85",
        "Created": "2018-09-17T01:41:26.174228707Z",
        "Path": "python",
        "Args": [
            "app.py"
        ],
        "State": {
            "Status": "running",
            "Running": true,
            "Paused": false,
            "Restarting": false,
            "OOMKilled": false,
            "Dead": false,
            "Pid": 23245,
            "ExitCode": 0,
            "Error": "",
            "StartedAt": "2018-09-17T01:41:26.494185806Z",
            "FinishedAt": "0001-01-01T00:00:00Z"
        },
......
```

