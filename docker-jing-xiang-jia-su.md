# docker 镜像加速

Docker 官方和国内很多云服务商都提供了国内加速器服务，例如：

* Docker官方提供的中国镜像库：**https://registry.docker-cn.com**
* 七牛云加速器：**https://reg-mirror.qiniu.com**

### Ubuntu14.04、Debian7Wheezy

对于使用 upstart 的系统而言，编辑 /etc/default/docker 文件，在其中的 DOCKER\_OPTS 中配置加速器地址：

```text
DOCKER_OPTS="--registry-mirror=https://registry.docker-cn.com"
```

重新启动服务:

```text
$ sudo service docker restart
```

### Ubuntu16.04+、Debian8+、CentOS7

对于使用 systemd 的系统，请在 /etc/docker/daemon.json 中写入如下内容（如果文件不存在请新建该文件）：

```text
{"registry-mirrors":["https://registry.docker-cn.com"]}
```

之后重新启动服务：

`$ sudo systemctl daemon-reload  
$ sudo systemctl restart docker`

### Mac OS X

对于使用 Mac OS X 的用户，在任务栏点击 Docker for mac 应用图标-&gt; Perferences...-&gt; Daemon-&gt; Registrymirrors。在列表中填写加速器地址 **https://registry.docker-cn.com** 。修改完成之后，点击 Apply&Restart 按钮，Docker 就会重启并应用配置的镜像地址了。

