# Ninjutsu
> Cheatsheets & Tips

## Docker
镜像推送到 [Docker Hub](https://hub.docker.com/)

```
$ docker login # 登录 docker hub
$ docker tag imagename:tagname username/imagename:tagname # 修改为规范镜像
$ docker push username/imagename:tagname
```