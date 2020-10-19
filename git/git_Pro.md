# git pro

标签（空格分隔）： git 工具

---

# 基础

##### 2.1取得项目的git仓库
有两种取得 Git 项目仓库的方法。第一种是在现存的目录下，通过导入所有文件来创建新的Git仓库。第二种是从已有的Git仓库克隆出一个新的镜像仓库来。
要对现有的某个项目开始用Git管理，只需到此项目所在的目录，执行：
```
$ git init    
```

```
$ git add *.c 
$ git add README
$ git commit -m 'initial project version'  
$ git clone git://github.com/schacon/grit.git

 //自己定义要新建的项目目录名称，可以在上面的命令最后指定：
$ git clone git://github.com/schacon/grit.git mygrit

//检查当前文件状态
$ git status

```

##### 2.2忽略某些文件

文件 .gitignore 的格式规范如下：
• 所有空行或者以注释符号 ＃ 开头的行都会被 Git 忽略。
• 可以使用标准的 glob 模式匹配。
• 匹配模式最后跟反斜杠（/）说明要忽略的是目录。
• 要忽略指定模式以外的文件或目录，可以在模式前加上惊叹号（!）取反。

```
# 此为注释 – 将被 Git 忽略
*.a # 忽略所有 .a 结尾的文件
!lib.a # 但 lib.a 除外
/TODO # 仅仅忽略项目根目录下的 TODO 文件，不包括 subdir/TODO
build/ # 忽略 build/ 目录下的所有文件
doc/*.txt # 会忽略 doc/notes.txt 但不包括 doc/server/arch.txt

```

要查看尚未暂存的文件更新了哪些部分，不加参数直接输入 git diff：
```
$ git diff
diff --git a/benchmarks.rb b/benchmarks.rb
index 3cb747f..da65585 100644
--- a/benchmarks.rb
+++ b/benchmarks.rb
@@ -36,6 +36,10 @@ def main
@commit.parents[0].parents[0].parents[0]
end
+ run_code(x, 'commits 1') do
+ git.commits.size
+ end
+
run_code(x, 'commits 2') do
log = git.commits('master', 15)
log.size
```

此命令比较的是工作目录中当前文件和暂存区域快照之间的差异，也就是修改之后还没有暂存起来的变化内
容。
若要看已经暂存起来的文件和上次提交时的快照之间的差异，可以用 git diff --cached 命令。（Git 1.6.1
及更高版本还允许使用 git diff --staged，效果是相同的，但更好记些。）来看看实际的效果：
```
$ git diff --cached

diff --git a/README b/README
new file mode 100644
index 0000000..03902a1
--- /dev/null
```
#####6 提交更新
```
$ git commit

$ git commit -m "Story 182: Fix benchmarks for speed"

//只要在提交的时候，给 git commit加上-a选项，Git就会自动把所有已经跟踪过的文件暂存起来一并提交，从而跳过 git add 步骤：
$ git commit -a -m 'added new benchmarks'

//移除文件 具体参考文档的2.2.8
git rm [文件名]
// 移动文件 2.2.9
$ git mv file_from file_to

git log 
//我们常用 -p 选项展开显示每次提交的内容差异，用 -2 则仅显示最近的两次更新

$ git log –p -2

//比如 --stat，仅显示简要的增改行数统计：
$ git log --stat

#修改最后一次提交
#有时候我们提交完了才发现漏掉了几个文件没有加，或者提交信息写错了。想要撤消刚才的提交操作，可以使用 --amend 选项重新提交：
$ git commit --amend

$ git reset HEAD benchmarks.rb

git checkout []
$ git remote -v
$ git remote add pb git://github.com/paulboone/ticgit.git
//从远程仓库抓取数据
$ git fetch [remote-name]

//4 推送数据到远程仓库
$ git push origin master

//git remote show [remote-name]
$ git remote show origin

//创建一个新的分支
$ git branch testing
//切换到其他分支
$ git checkout testing
//合并到 master 分支
$ git merge hotfix
//可以先删掉它。使用 git branch 的 -d 选项表示删除：
$ git branch -d hotfix

```





##推送到远程仓库

```
git init
git remote add orign https://git.oschina.net/JoNas4Yzy/empty.git
git remote -v
git pull https://git.oschina.net/JoNas4Yzy/empty.git
git push orign master

#Git 全局设置:
git config --global user.name "JoNas4Yzy"
git config --global user.email "yyz201000@163.com"

#创建 git 仓库:
mkdir hfh
cd hfh
git init
touch README.md
git add README.md
git commit -m "first commit"
git remote add origin https://git.oschina.net/JoNas4Yzy/hfh.git
git push -u origin master

#已有项目?

cd existing_git_repo
git remote add origin https://git.oschina.net/JoNas4Yzy/hfh.git
git push -u origin master

#clone version

git clone -b v1.5.0.RELEASE --depth 1 https://github.com/spring-projects/spring-data-redis.git

```

###[REBASE](http://gitbook.liuhui998.com/4_2.html)
###[Git的撤消操作 - 重置, 签出 和 撤消](http://gitbook.liuhui998.com/4_9.html)

```
git cherry-pick  //cpoy

```
[test teach palce](http://pcottle.github.io/learnGitBranching/?NODEMO)

#git 分支
查看远程的分支
```
> git branch -r 

 origin/HEAD -> origin/master
  origin/dev
  origin/master
  
# 查看本地分支
myrna@Yayng ~/I/A/blackholeAPI> git branch -a
  dev
* master
  remotes/origin/HEAD -> origin/master
  remotes/origin/dev
  remotes/origin/master

#
git branch

#重命名分支
git branch -m | -M oldbranch newbranch

#删除branchname分支
git branch -d | -D branchname 

#删除远程branchname分支
git branch -d -r branchname 
或者
 git push origin --delete  branchname

```

## git tag操作

```
# 查看已经有的tag
git tag 
# 增加tag
git tag [标签名] -m [描述]
git tag v0.01 -m "add a tag"
#删除tag
git tag -d [标签名]
git tag -d v0.01
```


```
# 创建新的分支 并直接切换到新的分支
git checkout -b "newBranch"
```

## PUSH
 git push <远程主机名> <本地分支名> <本地分支名>:<远程分支名>

 ```
 #推送远程不存在的分支
git push origin dev:dev # 推送本第的dev分支到远程 如果分支不存在 就会创建

git push origin :dev #推送空的分支到远程 等同于删除远程的分支效果等同于 git push origin --delete  branchname

 ```


