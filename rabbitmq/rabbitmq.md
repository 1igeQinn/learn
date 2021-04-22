# RabbitMQ 安装及常见问题解决。
## 安装
1. 下载文件[rabbitmq-server-mac-standalone-3.6.2.tar.xz](https://www.rabbitmq.com/releases/rabbitmq-server/v3.6.2/rabbitmq-server-mac-standalone-3.6.2.tar.xz)
2. 解压文件` tar -xf rabbitmq-server-mac-standalone-3.6.2.tar.xz`
3. 启动mq 

```
./sbin/rabbitmq-server start
```
4. 启用界面管理插件
```
./sbin/rabbitmq-plugins enable rabbitmq_management
```
启动的初始化 用户密码是guest、guest

## 常见问题
1.启动的时候遇到的遇到如下的错误

```
Warning: PID file not written; -detached was passed.
ERROR: epmd error for host Yzyang: timeout (timed out)
```
解决方式 ：
修改本地的host文件

```
sudo vi /etc/host
```

在host中增加 `127.0.0.1 Yzyang`


