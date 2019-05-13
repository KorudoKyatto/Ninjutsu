# Git

***同步 Github fork***

```
$ git remote -v # 列出 remote 配置
$ git remote add upstream https://github.com/ORIGINAL_OWNER/ORIGINAL_REPOSITORY.git # 指向上游仓库
$ git fetch upstream # 拉取上游仓库到本地 upstream/master 分支
$ git checkout master
$ git merge upstream/master # 合并 upstream/master 分支到 master 分支
```