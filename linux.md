# linux 交互 自动输入

标签（空格分隔）： linux shell 

---
使用了linux下的`spawn` `expect`  `send` 命令

push.sh 脚本

```
#!/usr/bin/expect -f
spawn git push sc master

# expect "Username for 'https://git.coding.net':"
# send "username\n"
# expect "Password for 'https://username@git.coding.net':"
# send "password\n"
expect {
    "Username for 'https://git.coding.net':"
    {send "username\n";exp_continue}
    "Password for 'https://username@git.coding.net':"
    {send "password\n"}
}
interact
#send 后面跟的值必须是双引号
```
autopush.sh

```
#!/bin/bash
# 这个分支做了ssh无需做配置
echo 20 >> README.md
git commit -a -m 'change'
git push origin master

```

## 说明
 使用 spawn的 时候上面的声明必须是`#!/usr/bin/expect -f`
 单独执行push.sh 脚本时候不需要使用
 
```
  sh push.sh  
```
 
 而是直接执行
 
```
 ./push.sh
```



