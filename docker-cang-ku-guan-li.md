# Docker 仓库管理

### Docker Hub

目前 Docker 官方维护了一个公共仓库 [Docker Hub](https://hub.docker.com/)。

大部分需求都可以通过在 Docker Hub 中直接下载镜像来实现。

#### 注册

在 [https://hub.docker.com](https://hub.docker.com/) 免费注册一个 Docker 账号。

#### 登录和退出

登录需要输入用户名和密码，登录成功后，我们就可以从 docker hub 上拉取自己账号下的全部镜像。

```text
$ docker login
```

**退出**

退出 docker hub 可以使用以下命令：

```text
$ docker logout
```

#### 推送镜像

用户登录后，可以通过 docker push 命令将自己的镜像推送到 Docker Hub。

以下命令中的 username 请替换为你的 Docker 账号用户名。

```bash
$ docker tag ubuntu:18.04 username/ubuntu:18.04
$ docker push username/ubuntu:18.04
```



