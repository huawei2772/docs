# ssh

系统：centos7.6

## 登录端口修改

### 修改配置文件
配置文件：/etc/ssh/sshd_config

```
#Port 22
#AddressFamily any
#ListenAddress 0.0.0.0
#ListenAddress ::
```

修改为
```
Port 22
Port 1130 // 1130未指定的端口，可以随意设置，不要占用系统端口
#AddressFamily any
#ListenAddress 0.0.0.0
#ListenAddress ::
```

### 重启ssh服务
```
/etc/init.d/sshd restart // 或者
service sshd restart
```

### 修改防火墙策略
```
// 关闭firewalld防火墙
service firewalld stop

// 新增一条放行策略
iptables -I INPUT -p tcp --dport 1130 -j ACCEPT
```
> 使用阿里云服务器时，需要在阿里云服务器安全组开放1130端口

> 修改成功后，禁用22端口

## 设置免密登录

### 获取免密登录使用的公钥
```
ssh-keygen -t rsa // 生成公钥
cat ~/.ssh/id_rsa.pub // 查看公钥
```

### 添加公钥到服务器
```
vim  ~/.ssh/authorized_keys // 在此文件中添加公钥
```