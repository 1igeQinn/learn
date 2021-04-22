# Spring scope


##5.3.1
每一个bean都一个或者多个标识，这些标识在bean容器里面必须是唯一的，通常情况下一个bean只有个标识，如果需要更多的标识的话，则通过aliases来标识
在xml配置文件中 通过id、name属性来声明bean的标识



##选择需要创建的代理类型
Choosing the type of proxy to create (spring 手册说明)
跨域（request、session ）引用时用代理`<aop:scoped-proxy/> `

```
<!-- DefaultUserPreferences implements the UserPreferences interface -->
<bean id="userPreferences" class="com.foo.DefaultUserPreferences" scope="session">
    <aop:scoped-proxy proxy-target-class="false"/>
</bean>
<bean id="userManager" class="com.foo.UserManager">
    <property name="userPreferences" ref="userPreferences"/>
</bean>
```
##Spring bean的作用范围（scope）
- singleton（默认）
 是指在spring Container里面只有一个bean 实例，设计模式中的单例是指ClassLoader中的bean 只有一个实例
- prototype 
 每次请求该bean的时候都会创建该bean的实例 所有有状态的bean都是使用prototype，无状态的bean使用singleton

- globalsession
- application

`request`,`session`,`global session` 范围只有在使用web容器的时候才能用

使用`request`,`session`,`global session`之前需要进行一些配置，怎么使用则依赖于项目使用的web框架
如果通过springmvc，则无需这些配置因为在`DispatcherServlet`,`DispatcherPortlet`已经实现了相应的关联。
如果使用servlet 2.5 web 容器需要注册`org.springframework.web.context.request.RequestContextListener`

```
<web-app>
    ...
    <listener>
        <listener-class>
            org.springframework.web.context.request.RequestContextListener
        </listener-class>
    </listener>
    ...
</web-app>
```
如果使用配置listener的时候出现问题 则可以使用一下的方式

```
<web-app>
    ...
    <filter>
        <filter-name>requestContextFilter</filter-name>
        <filter-class>org.springframework.web.filter.RequestContextFilter</filter-class>
    </filter>
    <filter-mapping>
        <filter-name>requestContextFilter</filter-name>
        <url-pattern>/*</url-pattern>
    </filter-mapping>
    ...
</web-app>
```
#### Request scope
```
<bean id="loginAction" class="com.foo.LoginAction" scope="request"/>
```
spring 容器会在每次HTTP请求的时候创建一个loginAction的实例。你可以任意的修改loginAction实例的状态。其他的实例是看不到这个实例内部的改动的。对于每个请求来说实例是唯一。当这个请求结束之后，该实例也随之消失。

####Session scope
```
<bean id="userPreferences" class="com.foo.UserPreferences" scope="session"/>
```
 基本同request
 
#### Global session scope
 
###5.5.4


