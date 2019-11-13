# elasticsearch

版本:elasticsearch-7.4.0

官方下载地址:https://www.elastic.co/cn/downloads/elasticsearch

## 安装运行

项目安装路径:/opt/elasticsearch-7.4.0

elasticsearch不建议以root用户运行，所以需要创建普通用户

### 创建运行用户并修改目录权限
```
useradd huawei -p 123456
chown -R huawei:huawei /opt/elasticsearch-7.4.0
```

### 切换用户运行
```
su - huawei
cd $ES_HOME
/bin/elasticsearch
```

### 以守护进程模式运行
```
./bin/elasticsearch -d -p pid
pkill -F pid // 关闭后天守护进程
```