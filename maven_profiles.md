#Maven profile 环境的配置

1. 在build 里面添加 resources并配置`<filtering>`

```

    <build>
    ...
        <resources>
            <resource>
                <directory>src/main/resources</directory>
                <filtering>true</filtering>
            </resource>
        </resources>
       ...
    </build>

    <profiles>
        <profile>
            <id>local</id>
            <activation>
                <activeByDefault>true</activeByDefault>
            </activation>
            <build>
                <filters>
                    <filter>local.properties</filter>
                </filters>
            </build>
        </profile>
        <profile>
            <id>test</id>
            <activation>
                <activeByDefault>false</activeByDefault>
            </activation>
            <build>
                <filters>
                    <filter>test.properties</filter>
                </filters>
            </build>
        </profile>
        <profile>
            <id>product</id>
            <activation>
                <activeByDefault>false</activeByDefault>
            </activation>
            <build>
                <filters>
                    <filter>product.properties</filter>
                </filters>
            </build>
        </profile>
    </profiles>

```

在pom文件同路径下配置不同环境的配置文件 local.properties、product.properties、test.properties
local.properties 文件的内容如下

```
domain=http://test.mtsports.cn:8182/
apiDomain=http://test.mtsports.cn:8181/v1/
```

在项目的resources 的properties文件中 配置如下

```
domain=${domain}
apiDomain=${apiDomain}
```

在编译项目时，可以使用 -P 参数指定需要使用的 profile 的 id，比如下面命令将会使用 local profile：

```
$mvn clean compile -Plocal
```

## 过滤不需要替换的变量。

由于项目的所有的配置文件都在resources目录，导致一些本来不要被替换的都替换了如某个xml文件中的

```
    <rabbit:connection-factory id="rabbitmqConnectionFactory"
                               host="${rabbitmq.host}"
                               username="${rabbitmq.username}"
                               password="${rabbitmq.password}"
                               virtual-host="${rabbitmq.virtual-host}"
                               publisher-confirms="true"
                               publisher-returns="true"/>

```
中的是不需要被替换的 也被替换了。

### 解决方式
1. 第一种 首先想到的是将 需要替换的和不需要替换的分离， 即将原来的environment.properties 单独的放到一个文件夹下面（如var）
则原来的配置改为

```
<build>
 <resources>
            <resource>
                <directory>src/main/var</directory>
                <filtering>true</filtering>
            </resource>
            <resource>
                <directory>src/main/resources</directory>
            </resource>
        </resources>
        ...
</build>

```

2. 查询官方的文档发现[Escape filtering](http://maven.apache.org/plugins/maven-resources-plugin/examples/escape-filtering.html)
可以声明一个转义的符号来防止替换。

在pom文件里面`<build>`节点下添加配置

```
<plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-resources-plugin</artifactId>
                <version>3.0.0</version>
                <configuration>
                    <escapeString>\</escapeString>
                </configuration>
            </plugin>
```

将xml文件中不需要替换的属性用`\`来转义即：

```
<rabbit:connection-factory id="rabbitmqConnectionFactory"
                               host="\${rabbitmq.host}"
                               username="\${rabbitmq.username}"
                               password="\${rabbitmq.password}"
                               virtual-host="\${rabbitmq.virtual-host}"
                               publisher-confirms="true"
                               publisher-returns="true"/>
```

这样既可。
(Apache Maven 使用 profile 和 filtering 实现多种环境下的资源配置管理)[http://archboy.org/2012/05/21/apache-maven-profile-filtering-multiple-build-environments/]