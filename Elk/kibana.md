# kibana

版本:kibana-7.4.0

官方下载地址:https://www.elastic.co/cn/downloads/kibana

## 安装运行

项目安装路径:/opt/kibana-7.4.0

kibana不建议以root用户运行，所以需要创建普通用户

### 配置
```
# 端口设置
server.port: 5601

# 域名设置
server.host: "0.0.0.0"

# 名称配置
server.name: "kibana-production"

# 配置kibana语言，支持中文
i18n.locale: "zh-CN" 

# 配置kibana数据存在路径
path.data: /data/kibana/data
```

### 运行
```
su - huawei
cd $KB_HOME
bin/kibana
```

### 以后台守护进程运行
```
# 使用supersovord启动kibana,以下为建议配置

[program:kibana]
command=/opt/kibana-7.4.0/bin/kibana
autostart=true
autorestart=true
startretries=3
user=huawei // 非root用户
redirect_stderr=true
stdout_logfile_maxbytes=200MB
stdout_logfile_backups=20
stdout_logfile=/data/supervisor/kibana-run.log
stderr_logfile=/data/supervisor/kibana-error.log

# 启动进程
supervisorctl kibana start
```