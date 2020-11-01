# maven 卡住问题
不管是使用IDE 还是maven命令

```
mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=my-app -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
```

生成项目的时候总会卡在`[INFO] Generating project in Batch mode`这边很久，：
通过添加 `-X` 的参数可以查看调试信息,可以看到程序卡在了

```
[DEBUG] Searching for remote catalog: http://repo1.maven.org/maven2/archetype-catalog.xml
```

>主要原因就是网速问题（maven服务器在国外），因为配置文件无法下载造成阻塞

##解决方式
### 一 命令行解决方式 

1. 将archetype-catalog.xml下载到本地。
2. 将archetype-catalog.xml复制到 .m2\repository\org\apache\maven\archetype\archetype-catalog\2.2下面
3. 在上述命令后增加参数-DarchetypeCatalog=local，变成读取本地文件即可。

### 二 Intellij的解决方式
关闭所有的intellij 项目，点开设置。找到maven的runner 在VM Options 里面添加

```
-DarchetypeCatalog=internal 
```

***注意右上角的灰字 ：for dafault projetc 而不是 for current project ***

###参考地址
1. [IDEA新建MAVEN项目时，MVN ARCHETYPE:GENERATE 速度缓慢
](http://www.cnphp6.com/archives/113800)

2. [解决maven生成项目时卡死
](http://www.jianshu.com/p/6e82edb0e5d1)

3 .[maven generating project in batch mode hang
](http://www.cnblogs.com/beiyeren/p/4566485.html)

4.[maven "Generating project in Batch mode"问题的解决
](http://www.cnblogs.com/wardensky/p/4513372.html)

