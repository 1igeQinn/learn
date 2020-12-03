# 类型转换（Type Conversion）

spring 的`core.convert`包提供了一些基本的类型转换的类

spring中的类的接口

```
package org.springframework.core.convert.converter;
  public interface Converter<S, T> {
    T convert(S var1);
} 
```
##7.6 Formatter

一般目的的类型转换用实现Converter 接口来实现。
在有客户端交互的情况下的装换实现Formatter接口来实现
### FormatterRegistry SPI
用来注册formatters和converters，`FormattingConversionService`是`FormatterRegistry`的一个能够适应大多数情况的实现
### FormatterRegistrar SPI

###Configuring Formatting in Spring MVC
在SpringMVC应用中，你可以通过`annotaion-driven`的属性来自定义 `ConversionService` ，之后这个转化服务可以随意的在Controller model绑定的时候用.如果没有明确（explicitly）的配置，springMVC会使用默认的formatters和converters。
使用默认的格式化只需要在配置文件中开启是spring的注解就行
> <mvc:annotation-driven/>

> todo 写个自定义的例子和配置
> 

自定义的配置的例子

```
<mvc:annotation-driven conversion-service="conversionService"/>
<bean id="conversionService" class="org.springframework.format.support.FormattingConversionServiceFactoryBean"> <property name="converters">
     <set>
         <bean class="org.example.MyConverter"/>
     </set>
</property>
<property name="formatters"> 
    <set>
        <bean class="org.example.MyFormatter"/>
        <bean class="org.example.MyAnnotationFormatterFactory"/> 
    </set>
</property>
    <property name="formatterRegistrars">
<set>
    <bean class="org.example.MyFormatterRegistrar"/>
</set>
        </property>
</bean>
```

##7.7配置全局的日期和时间格式化

```
@Configuration public class AppConfig {     @Bean     public FormattingConversionService conversionService() {         //使用DefaultFormattingConversionService，但是不注册默认的fomatters         DefaultFormattingConversionService conversionService =                 new DefaultFormattingConversionService(false);          conversionService.addFormatterForFieldAnnotation(new NumberFormatAnnotationFormatterFactory());         DateFormatterRegistrar registrar = new DateFormatterRegistrar();         registrar.setFormatter(new DateFormatter("yyyyMMdd"));         registrar.registerFormatters(conversionService);         return conversionService;     }  }

```

