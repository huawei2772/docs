# logstash

版本:logstash-7.4.0

官方下载地址:https://www.elastic.co/cn/downloads/logstash

## 安装运行

项目安装路径:/opt/logstash-7.4.0

### 配置
```
# 获取数据来源，redis
input {
  redis {
        data_type => "list"
        host => "localhost"
        port => 6379
        db => 10
        key => "redis-key"
  }
}

# 数据过滤
filter {
  geoip {
    source => "client_ip"
  }
  date{
    match => ["timestamp", "UNIX", "ISO8601"]
    target => "@timestamp"
    remove_field => ["timestamp"]
  }
}

# 数据输出，输出到elasticsearch跟控制台直接输出
output {
  elasticsearch {
      hosts => ["localhost:9200"]
      index => "logstash-%{+YYYY.MM.dd}"
  }

  stdout {
    codec => rubydebug
  }
}
```

### 运行命令
```
# 检测配置文件是否正常
bin/logstash -f config/logstash-config-file.conf --config.test_and_exit

# 运行，修改配置后自动生效
bin/logstash -f config/logstash-config-file.conf --config.reload.automatic
```