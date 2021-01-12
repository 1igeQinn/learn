# NGINX

标签（空格分隔）： nginx-1 20150522

---

##负载均衡
### nginx的 upstream目前支持四种的分配方式
- 轮询（默认）
    每个请求按时间顺序逐一分配到不同的后端服务器，如果后端服务器down掉，能自动剔除。

- weight
指定轮询几率，weight和访问比率成正比，用于后端服务器性能不均的情况。

- ip_hash
每个请求按访问的ip的hash结果分配，这样每个访客固定访问一个后端服务器。可以解决session的问题

- fair（第三方）
安后端服务器响应时间来分配请求，相应时间短的优先分配。
- url_hash(第三方)

###配置

- 在http节点里添加：
####定义负载均衡设备的ip及设备状态

```
upstream myServer{
    server 127.0.0.1:9090 down；
    server 127.0.0.1:8080 weight=2；
    server 127.0.0.1:6060；
    server 127.0.0.1:7070 backup；
}
      
```

- 在需要使用负载的Server的节点下添加

```
proxy_pass http://myServer;
```

#### upstream 每个设备的状态 :
- down 表示当前的server暂时不参与负载
- weight默认为1，weight越大，负载的权重越大
- max_fails 允许请求失败的次数，默认为1，当超过最大次数时，返回proxy_next_upstream 模块定义的错误

- fail_timeout max_fails次失败后，暂停的时间。
- backup：其他所有的非backup机器down或者忙的时候，请求backup机器。所以这台机器压力会最轻。

Nginx 还支持多组的负载均衡，可以配置多个upstream，来服务于不同的Server。

## Session 共享问题
配置负载均衡比较简单，但是最关键的是怎么实现多态服务器之间的session共享。
 - 不适用session 换做cookie
 能把session改成cookie，就能避开session的一些弊端。系统不复杂的情况下尽量的避免是用session。

- 应用服务器的自行实现共享
asp.net 可以用数据或者memcached来保存session

- ip_hash
nginx 中的ip_hash 技术能够将ip请求定向到同一台后端。这样一来这个ip下的某个客户端和某个后端能建立稳固的session。ip_hash中定义的
upstream backend{
    server 12.0.0.1:8080；
    server 12.0.0.1:8080；
    ip_hash;
}


[没看完的地址](http://www.cnblogs.com/xiaogangqq123/archive/2011/03/04/1971002.html)




#Nginx 进程与模块
【实验楼】
## Nginx架构介绍