# nginx 操作

标签（空格分隔）： 操作

---

## 安装 
```
./configure
make 
make install

#选项设置各个模块的使用情况
./configure --help 

#“--with-http_stub_status_module”可以用来启用 Nginx 的 NginxStatus 功能，以监控 Nginx 的当前状态。
./configure --with-http_stub_status_module  --prefix=/opt/nginx 
```
## 配置 
###1、虚拟主机
####什么是虚拟主机
虚拟机使用的是特殊的软硬件技术，他把一台运行在因特网上的服务器分成一台台“虚拟”的主机，每台虚拟都可以主机都可以是一个独立的网站，可以具有独立的域名，具体完整的internet服务器功能（WWW、FTP、Email etc.）,同一台主机上的虚拟主机之间是完全独立的。从网站的访问者来看，每一台虚拟机和一台独立的主机完全一样。

####Nginx 也可以配置多种类型的虚拟主机：
- 基于IP的虚拟主机
- 基于域名的虚拟主机
- 基于端口的虚拟主机

#### <i class="icon-bookmark"></i> 基于IP的虚拟主机
```
http
{
    # 第一个虚拟主机
    server
    {
        # 监听的IP和端口
        listen          192.168.8.43:80;
        # 主机名称
        server_name    192.168.8.43;
        # 访问日志文件存放路径
        access_log      logs/server1.access.log combined;
        location /
        {
            # 默认首页文件，顺序从左到右，如果找不到index.html文件，则查找index.htm文件作为首页文件
            index index.html index.htm;
            # HTML网页文件存放的目录
            root  /data0/htdocs/server1;
        }
    }
    # 第二个虚拟主机
    server
    {
        # 监听的IP和端口
        listen          192.168.8.44:80;
        # 主机名称
        server_name    192.168.8.44;
        # 访问日志文件存放路径
        access_log      logs/server2.access.log combined;
        location /
        {
            # 默认首页文件，顺序从左到右，如果找不到index.html文件，则查找index.htm文件作为首页文件
            index index.html index.htm;
            # HTML网页文件存放的目录
            root  /data0/htdocs/server2;
        }
    }
    # 第三个虚拟主机
    server 
    {
        # 监听的IP和端口
        listen          192.168.8.45:80;
        # 主机名称
        server_name    192.168.8.45;
        # 访问日志文件存放路径
        access_log      logs/server3.access.log combined;
        location /
        {
            # 默认首页文件，顺序从左到右，如果找不到index.html文件，则查找index.htm文件作为首页文件
            index index.html index.htm;
            # HTML网页文件存放的目录
            root  /data0/htdocs/server3.com;
        }
    }
}
```

#### <i class="icon-circle"></i> 基于域名的虚拟主机

```
http
{
    # 第一个虚拟主机
    server
    {
        # 监听的端口
        listen     80;
        # 主机名称
        server_name    aaa.domain.com;
        # 访问日志文件存放路径
        access_log      logs/aaa.domain.com.access.log combined;
        location /
        {
            # 默认首页文件，顺序从左到右，如果找不到index.html文件，则查找index.htm文件作为首页文件
            index index.html index.htm;
            # HTML网页文件存放的目录
            root  /data0/htdocs/aaa.domain.com;
        }
    }
    # 第二个虚拟主机
    server
    {
        # 监听的IP和端口
        listen     80;
        # 主机名称
        server_name    bbb.otherdomain.com;
        # 访问日志文件存放路径
        access_log      logs/bbb.otherdomain.com.access.log combined;
        location /
        {
            # 默认首页文件，顺序从左到右，如果找不到index.html文件，则查找index.htm文件作为首页文件
            index index.html index.htm;
            # HTML网页文件存放的目录
            root  /data0/htdocs/bbb.otherdomain.com;
        }
    }
    # 第三个虚拟主机
    server
    {
        # 监听的IP和端口
        listen     80;
        # 主机名称
        server_name    www.domain.com domain.com *.domain.com;
        # 访问日志文件存放路径
        access_log      logs/bbb.domain.com.access.log combined;
        location /
        {
            # 默认首页文件，顺序从左到右，如果找不到index.html文件，则查找index.htm文件作为首页文件
            index index.html index.htm;
            # HTML网页文件存放的目录
            root  /data0/htdocs/domain.com;
        }
    }
}
```

### <i class="icon-bookmark"></i> 完整的配置文件示例
Nginx的配置文件是一个纯文本文件，它一般位于Nginx安装目录的conf目录下



```
#开启进程数 <=CPU数
worker_processes 1;

#错误日志保存位置
#error_log logs/error.log;
#error_log logs/error.log notice;
#error_log logs/error.log info;

#进程号保存文件
#pid logs/nginx.pid;

#等待事件
events {
#每个进程最大连接数（最大连接=连接数x进程数） 
worker_connections 1024;
}


http {
#文件扩展名与文件类型映射表
include mime.types;

#默认文件类型
default_type application/octet-stream;

#日志文件输出格式 这个位置相于全局设置
#log_format main '$remote_addr - $remote_user [$time_local] "$request" '
# '$status $body_bytes_sent "$http_referer" '
# '"$http_user_agent" "$http_x_forwarded_for"';

#请求日志保存位置
#access_log logs/access.log main;

#打开发送文件
sendfile on;
#tcp_nopush on;

#连接超时时间
#keepalive_timeout 0;
keepalive_timeout 65;

#打开gzip压缩
#gzip on;

#设定请求缓冲
client_header_buffer_size 1k;
large_client_header_buffers 4 4k;

#设定负载均衡的服务器列表
upstream myproject { 
#weigth参数表示权值，权值越高被分配到的几率越大
#max_fails 当有#max_fails个请求失败，就表示后端的服务器不可用，默认为1，将其设置为0可以关闭检查
#fail_timeout 在以后的#fail_timeout时间内nginx不会再把请求发往已检查出标记为不可用的服务器
#这里指定多个源服务器，ip:端口,80端口的话可写可不写 
server 192.168.1.78:8080 weight=5 max_fails=2 fail_timeout=600s;
#server 192.168.1.222:8080 weight=3 max_fails=2 fail_timeout=600s; 
}

#第一个虚拟主机
server {
    #监听IP端口
    listen 80;

    #主机名
    server_name localhost;

    #设置字符集
    #charset koi8-r;

    #本虚拟server的访问日志 相当于局部变量
    #access_log logs/host.access.log main; 

    #对本server"/"启用负载均衡
    location / { 
        #root /root; #定义服务器的默认网站根目录位置
        #index index.php index.html index.htm; #定义首页索引文件的名称
        proxy_pass http://myproject; #请求转向myproject定义的服务器列表

        #以下是一些反向代理的配置可删除.
        # proxy_redirect off; 
        # proxy_set_header Host $host; 
        # proxy_set_header X-Real-IP $remote_addr; 
        # proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for; 
        # client_max_body_size 10m; #允许客户端请求的最大单文件字节数 
        # client_body_buffer_size 128k; #缓冲区代理缓冲用户端请求的最大字节数， 
        # proxy_connect_timeout 90; #nginx跟后端服务器连接超时时间(代理连接超时) 
        # proxy_send_timeout 90; #后端服务器数据回传时间(代理发送超时) 
        # proxy_read_timeout 90; #连接成功后，后端服务器响应时间(代理接收超时) 
        # proxy_buffer_size 4k; #设置代理服务器（nginx）保存用户头信息的缓冲区大小 
        # proxy_buffers 4 32k; #proxy_buffers缓冲区，网页平均在32k以下的话，这样设置 
        # proxy_busy_buffers_size 64k; #高负荷下缓冲大小（proxy_buffers*2） 
        # proxy_temp_file_write_size 64k; #设定缓存文件夹大小，大于这个值，将从upstream服务器传
        } 
    location /upload { 
        alias e:/upload; 
    }
    #设定查看Nginx状态的地址 
    location /NginxStatus { 
        stub_status on; 
        access_log off; 
        #allow 192.168.0.3;
        #deny all;
        #auth_basic "NginxStatus"; 
        #auth_basic_user_file conf/htpasswd; 
    }

    #error_page 404 /404.html;
    
    # redirect server error pages to the static page /50x.html
    # 定义错误提示页面
    error_page 500 502 503 504 /50x.html;
    location = /50x.html {
        root html;
    }


# proxy the PHP scripts to Apache listening on 127.0.0.1:80
#
#location ~ \.php$ {
# proxy_pass http://127.0.0.1;
#}

# pass the PHP scripts to FastCGI server listening on 127.0.0.1:9000
#
#location ~ \.php$ {
# root html;
# fastcgi_pass 127.0.0.1:9000;
# fastcgi_index index.php;
# fastcgi_param SCRIPT_FILENAME /scripts$fastcgi_script_name;
# include fastcgi_params;
#}

# deny access to .htaccess files, if Apache's document root
# concurs with nginx's one
#
#location ~ /\.ht {
# deny all;
#}
} 


# another virtual host using mix of IP-, name-, and port-based configuration
#
#server {
#多监听 
# listen 8000;
#主机名
# listen somename:8080;
# server_name somename alias another.alias;

# location / {
#WEB文件路径
# root html;
#默认首页
# index index.html index.htm;
# }
#}


# HTTPS server HTTPS SSL加密服务器
#
#server {
# listen 443;
# server_name localhost;

# ssl on;
# ssl_certificate cert.pem;
# ssl_certificate_key cert.key;

# ssl_session_timeout 5m;

# ssl_protocols SSLv2 SSLv3 TLSv1;
# ssl_ciphers HIGH:!aNULL:!MD5;
# ssl_prefer_server_ciphers on;

# location / {
# root html;
# index index.html index.htm;
# }
#} 
}

```

##nginx启动，重启，关闭命令

### 启动
假设Nginx的安装目录是/usr/local/nginx 目录中，那么启动命令就是
```
/usr/local/nginx/sbin/ -c /usr/local/nginx/conf/nginx.conf
```
参数`-c` 制定了配置文件的路径，***如果不加，nginx会默认加载其安装目录的conf目录下的nginx.conf文件***

### 关闭
```
ps -ef | grep nginx

#从容停止Nginx：
kill -QUIT 主进程号
#快速停止Nginx：
kill -TERM 主进程号
#强制停止Nginx：
pkill -9 nginx

```
### 重启
平滑重启
如果更改了配置就要重启Nginx，要先关闭Nginx再打开？不是的，可以向Nginx 发送信号，平滑重启。
平滑重启命令：
```
kill -HUP 住进称号或进程号文件路径
```

或者使用
```
/usr/nginx/sbin/nginx -s reload
```

###检测配置文件是否有错误
```
nginx -t -c /usr/nginx/conf/nginx.conf
#或者
/usr/nginx/sbin/nginx -t
```

###平滑升级

如果服务器正在运行的Nginx要进行升级、添加或删除模块时，我们需 要停掉服务器并做相应修改，这样服务器就要在一段时间内停止服务，Nginx可以在不停机的情况下进行各种升级动作而不影响服务器运行。

- 步骤1：
如 果升级Nginx程序，先用新程序替换旧程序文件，编译安装的话新程序直接编译到Nginx安装目录中。
- 步 骤2：执行命令
***`kill -USR2`*** 旧版程序的主进程号或进程文件名
此时旧的Nginx主进程将会把自己的进程文件改名为.oldbin，然后执行新版 Nginx。新旧Nginx会同市运行，共同处理请求。
这时要逐步停止旧版 Nginx，输入命令：
***`kill -WINCH`*** 旧版主进程号
慢慢旧的工作进程就都会随着任务执行完毕而退出，新版的Nginx的工作进程会逐渐取代旧版 工作进程。
此 时，我们可以决定使用新版还是恢复到旧版。
不重载配置启动新/旧工作进程
***`kill -HUP`*** 旧/新版主进程号
从容关闭旧/新进程
```
 kill -HUP 【进程id】 //具体位置 查看配置见中得pid 配置
 // 不指定配置文件会优先加载默认的配置文件
```
***`kill -QUIT`*** 旧/新主进程号
如果此时报错，提示还有进程没有结束就用下面命令先关闭旧/新工作进程，再关闭主进程号：
***`kill -TERM`*** 旧/新工作进程号
这样下来，如果要恢复到旧版本，只需要上面的几个步 骤都是操作新版主进程号，如果要用新版本就上面的几个步骤

