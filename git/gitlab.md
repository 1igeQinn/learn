# GitLab

标签（空格分隔）： gitlab

---

```
# 启动所有的组件
sudo gitlab-ctl start

# 停止所有的组件
sudo gitlab-ctl stop

# 重启所有的组件
sudo gitlab-ctl restart

# 独立的启动某个组件 eg: sidekiq
sudo gitlab-ctl restart sidekiq

#重新配置配置文件
sudo gitlab-ctl reconfigure
```

[gitlab启动、重启参考地址](https://gitlab.com/gitlab-org/omnibus-gitlab/blob/629def0a7a26e7c2326566f0758d4a27857b52a3/README.md#configuring-the-external-url-for-gitlab)


#gitlab的配置
```
# 配置clone 推送的url
external_url 'http://git.mtsports.cn'

# gitlab的nginx的配置 ip的地址
nginx['listen_addresses'] = ['*']
# gitlab的nginx的配置 端口
nginx['listen_port'] = 9191 # override only if you use a reverse proxy: https://gitlab.com/gitlab-org/omnibus-gitlab/blob/master/doc/settings/nginx.md#setting-the-nginx-listen-port
```
[nginx配置的参考地址](https://gitlab.com/gitlab-org/omnibus-gitlab/blob/master/doc/settings/nginx.md#setting-the-nginx-listen-port)


