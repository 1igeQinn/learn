# svn-git 迁移

tags： svn-git-迁移 hhh

---
## cmd 
### tong 
```

> git svn clone svn://yangyunzhong@192.168.8.186/project/api/blackholeAPI --no-metadata --authors-file=/Users/myrna/Desktop/userinfo.txt  blackholeAPI

#说明
svn://yangyunzhong@192.168.8.186/project/api/blackholeAPI svn对应的项目的链接
--authors-file 的配置的对应的用户信息的文件
blackholeAPI 对应项目的名称

# 配置用户信息
> cd blackholeAPI
> git config user.name "yzyang"
> git config user.email "yunzhong_yang@fountask"

# 在git上新建项目 推送
```

##userinfo.txt内容
```
yangyunzhong=yzyang<yunzhong_yang@fountask.com>
lijingrong=lijingrong<jingrong_li@fountask.com>
huangjiang=hj<jiang_huang@fountask.com>
wujing=jwu< jing_wu@fountask.com>
```

svn://192.168.8.186/project/api/blackholeAPI
在此输入正文


##问题

- 1 错误
`error: RPC failed; result=22, HTTP code = 411`
git的http 推送大小限制 
<font color="red">运行命令</font> 执行 `git config http.postBuffer 524288000`
[参考地址](http://my.oschina.net/luozheng/blog/382610?p=1)




