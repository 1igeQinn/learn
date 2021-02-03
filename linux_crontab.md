# linux crontab 定时任务的使用.md

```
crontab -e 直接编辑 任务 进行修改

# * * * * * date >> /Users/myrna/testtime.txt
 * * * * * python /Users/myrna/Downloads/test.py
 * * * * * /Users/myrna/Desktop/oooo.sh
 * * * * * say hello
# * * * * * sh /usr/myrna/test.sh
```

