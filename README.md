
# 部署方式
## 复制
```apacheconf
# 复制
cp docker-compose.yml.sample 为 docker-compose.yml
# 修改 的端口号，或者其它微调
vi docker-compose.yml
```
## 执行
```apacheconf
# 注意需要换成 root:{1000UID的用户}，不知道可以先不改，等报错了去 ekfg_logstash 里看同目录其它配置的权限
sudo chown -R root:1000 ./.docker/logstash/config/logstash.conf ./.docker/filebeat/config/nginx.yml ./.docker/filebeat/config/filebeat.yml
sudo chmod go-w ./.docker/filebeat/config/filebeat.yml ./.docker/filebeat/config/nginx.yml
sudo chmod -R 777 ./.docker/elasticsearch/logs/
docker-compose up
```
##  会提示密码不对, 需要去ES配置密码
```apacheconf
docker exec -ti ekfg_es sh
cd bin
elasticsearch-setup-passwords interactive
## 所有账号都输入密码：asdf2x2023
```

# ES HEAD
```URL
# IP 换成你的机器的ip
http://127.0.0.1:9100/?base_uri=http://127.0.0.1:9200&auth_user=elastic&auth_password=asdf2x2023
```
