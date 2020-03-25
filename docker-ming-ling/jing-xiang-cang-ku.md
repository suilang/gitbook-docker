# 镜像仓库

### **docker login :** 登陆到一个Docker镜像仓库，如果未指定镜像仓库地址，默认为官方仓库 Docker Hub

### **docker logout :** 登出一个Docker镜像仓库，如果未指定镜像仓库地址，默认为官方仓库 Docker Hub

#### 语法

```text
docker login [OPTIONS] [SERVER]
```

```text
docker logout [OPTIONS] [SERVER]
```

OPTIONS说明：

* **-u :**登陆的用户名
* **-p :**登陆的密码

#### 实例

登陆到Docker Hub

```text
docker login -u 用户名 -p 密码
```

登出Docker Hub

```text
docker logout
```

### **docker pull :** 从镜像仓库中拉取或者更新指定镜像

#### 语法

```text
docker pull [OPTIONS] NAME[:TAG|@DIGEST]
```

OPTIONS说明：

* **-a :**拉取所有 tagged 镜像
* **--disable-content-trust :**忽略镜像的校验,默认开启

#### 实例

从Docker Hub下载java最新版镜像。

```text
docker pull java
```

从Docker Hub下载REPOSITORY为java的所有镜像。

```text
docker pull -a java
```

### **docker push :** 将本地的镜像上传到镜像仓库,要先登陆到镜像仓库

#### 语法

```text
docker push [OPTIONS] NAME[:TAG]
```

OPTIONS说明：

* **--disable-content-trust :**忽略镜像的校验,默认开启

#### 实例

上传本地镜像myapache:v1到镜像仓库中。

```text
docker push myapache:v1
```

### **docker search :** 从Docker Hub查找镜像

#### 语法

```text
docker search [OPTIONS] TERM
```

OPTIONS说明：

* **--automated :**只列出 automated build类型的镜像；
* **--no-trunc :**显示完整的镜像描述；
* **-s :**列出收藏数不小于指定值的镜像。

#### 实例

从Docker Hub查找所有镜像名包含java，并且收藏数大于10的镜像

```text
runoob@runoob:~$ docker search -s 10 java
```

