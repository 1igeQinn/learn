# config logback

在classpath 下配置logback.xml或者logback-test.xml

```
<configuration>

  <appender name="STDOUT" class="ch.qos.logback.core.ConsoleAppender">
    <!-- encoders are assigned the type
         ch.qos.logback.classic.encoder.PatternLayoutEncoder by default -->
    <encoder>
      <pattern>%d{HH:mm:ss.SSS} [%thread] %-5level %logger{36} - %msg%n</pattern>
    </encoder>
  </appender>

  <root level="debug">
    <appender-ref ref="STDOUT" />
  </root>
</configuration>

```

configuration 可以设置`debug="true"` 来显示logback的状态。//

- [ ] debug="true"的细节处理

###自动扫描配置文件改动
```
<configuration scan="true"> //默认的1min扫描一次
  ... 
</configuration> 

//set the time 单位可以是  milliseconds, seconds, minutes or hours如果不设置单位默认是milliseconds
<configuration scan="true" scanPeriod="30 seconds" > 
  ...
</configuration> 
```
configuration 下面有一个或多个的<appender> 、<logger>、<root>

配置<logger>

```
<configuration>

  <appender name="STDOUT"
    class="ch.qos.logback.core.ConsoleAppender">
    <encoder>
      <pattern>
        %d{HH:mm:ss.SSS} [%thread] %-5level %logger{36} - %msg%n
     </pattern>
    </encoder>
  </appender>

  <logger name="chapters.configuration" level="INFO" />
  <logger name="chapters.configuration.Foo" level="DEBUG" />

  <root level="DEBUG">
    <appender-ref ref="STDOUT" />
  </root>

</configuration>

// appender

<configuration>

  <appender name="FILE" class="ch.qos.logback.core.FileAppender">
    <file>myApp.log</file>

    <encoder>
      <pattern>%date %level [%thread] %logger{10} [%file:%line] %msg%n</pattern>
    </encoder>
  </appender>

  <appender name="STDOUT" class="ch.qos.logback.core.ConsoleAppender">
    <encoder>
      <pattern>%msg%n</pattern>
    </encoder>
  </appender>

  <root level="debug">
    <appender-ref ref="FILE" />
    <appender-ref ref="STDOUT" />
  </root>
</configuration>
```

