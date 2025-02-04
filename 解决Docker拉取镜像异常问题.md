

# 解决Docker拉取镜像异常问题

报错内容：Error response from daemon: Get “https://registry-1.docker.io/v2/”: ........

ubuntu解决方案：

https://blog.csdn.net/qq_40821260/article/details/144870431

https://blog.csdn.net/weixin_46028606/article/details/142663559

### root用户执行下面命令：

```shell
touch /etc/docker/daemon.json
```

```shell
chmod 777 -R /etc/docker/daemon.json
```

```shell
vi /etc/docker/daemon.json
```



## daemon.json添加以下内容：

更新daemon.json的内容如下：

```sh
{
    "registry-mirrors": [
        "https://docker.m.daocloud.io",
        "https://dockerhub.icu",
        "https://docker.anyhub.us.kg",
        "https://docker.1panel.live"
    ]
}
```

为了避免docker日志文件过大的异常，建议同时开启IPV6的功能并限制日志的大小到20m.完成的Json文件内容如下：

```sh
{
    "log-driver": "json-file",
    "log-opts": {
        "max-size": "20m",
        "max-file": "3"
    },
    "ipv6": true,
    "fixed-cidr-v6": "fd00:dead:beef:c0::/80",
    "experimental":true,
    "ip6tables":true,
    "registry-mirrors": [
      "https://docker.m.daocloud.io",
      "https://dockerhub.icu",
      "https://docker.anyhub.us.kg",
      "https://docker.1panel.live"
    ]
}
```



## 1. 重启dockers

```sh
sudo systemctl restart docker
```



## 2. 检查配置是否生效

```shell
sudo docker info
```



## 3. Docker镜像源检查

```shell
sudo docker pull hello world
```

