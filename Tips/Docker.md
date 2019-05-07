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

***管理 docker 网络***

```
$ docker network ls # 列出网络
$ docker network rm # 删除一个或多个网络
$ docker network create \ # 创建网络
  --driver=bridge \ -d, 默认 bridge, 驱动程序管理网络
  --subnet=172.18.0.0/16 \ 表示网段的 CIDR 格式的子网
  --gateway=172.18.0.1 \ 用于主子网的 IPv4 或 IPv6 网关
  NETWORK
$ docker run --name containername --network NETWORK --ip IP -d imagename:tagname # 容器加入网路设置固定 IP
```

***CentOS 升级 Docker***

```
$ sudo yum remove docker docker-common \ 
  container-selinux docker-selinux \ 
  docker-engine docker-engine-selinux # 卸载旧版本
$ sudo yum install -y yum-utils device-mapper-persistent-data lvm2 # 安装依赖
$ sudo yum-config-manager \ 
  --add-repo https://download.docker.com/linux/centos/docker-ce.repo # 安装 Docker 官方仓库
$ sudo yum makecache fast # 更新仓库源
$ sudo yum install docker-ce # 安装 Docker-CE docker-ce-<VERSION> 特定版本
$ sudo systemctl start docker
$ sudo systemctl enable docker
```