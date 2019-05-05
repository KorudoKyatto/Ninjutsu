# Docker
***镜像推送到 [Docker Hub](https://hub.docker.com/)***

```
$ docker login # 登录 docker hub
$ docker tag imagename:tagname username/imagename:tagname # 修改为规范镜像
$ docker push username/imagename:tagname
```

***修改 docker 配置***

```
$ vim /etc/docker/daemon.json

{
    "registry-mirrors": [
        "https://*****.mirror.aliyuncs.com"
    ], # 镜像仓库地址
    "log-driver": "json-file", # 容器日志格式
    "log-opts": {
        "max-size": "100m", # 容器日志大小上限
        "max-file": "3" # 容器日志个数
    }
}

$ systemctl daemon-reload
$ systemctl restart docker
```