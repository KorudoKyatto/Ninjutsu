# Linux
***CentOS 7 安装 [BBR](https://github.com/google/bbr)***

```
$ uname -r # 查看当前系统内核版本
$ yum update
$ rpm --import https://www.elrepo.org/RPM-GPG-KEY-elrepo.org # 导入 ELRepo 软件源的 GPG 公钥
$ rpm -Uvh https://www.elrepo.org/elrepo-release-7.0-3.el7.elrepo.noarch.rpm # 导入 ELRepo 软件源
$ yum --enablerepo=elrepo-kernel install kernel-ml -y # 下载并安装最新稳定版内核
$ rpm -qa | grep kernel # 确认内核列表
$ egrep ^menuentry /etc/grub2.cfg | cut -f 2 -d \' # 查看 grub2 菜单条目
$ grub2-set-default 0 # 设置 grub2 缺省引导（数字依据上一命令结果）
$ reboot
$ uname -r # 确认内核版本
$ yum -y remove kernel kernel-tools # 删除旧内核，防止 yum 更新旧版内核之后覆盖了 grub 默认启动项
$ echo 'net.core.default_qdisc=fq' | sudo tee -a /etc/sysctl.conf
$ echo 'net.ipv4.tcp_congestion_control=bbr' | sudo tee -a /etc/sysctl.conf
$ sysctl -p # 加载系统参数
$ sysctl -n net.ipv4.tcp_congestion_control # 验证 bbr 是否开启
$ lsmod | grep bbr # 检查内核模块是否加载
```