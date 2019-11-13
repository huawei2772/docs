# firewalld

centos7 防火墙相关操作

```
service firewalld status // 查看防火墙状态
service firewalld stop // 临时关闭防火墙
service firewalld start // 启动防火墙

/bin/systemctl disable firewalld.service // 禁止开机启动
```