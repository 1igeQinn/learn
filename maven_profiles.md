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