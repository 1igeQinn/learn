# Spring 文档阅读

###5.3.1

###5.3.2 实例化bean
bean的本质上就是创建一个或者多个对象。

- 通过xml配置的时候 通过`</bean>`的class属性来制定对象的类型
-  典型的 根据构造函数来实例化bean
-  内部类的实例化 需要使用（java类编译之后的二进制码来使用）如：
`Foo` 有个内部类`Bar` 则class 应该是`Foo$Bar`

####依赖注入
- 构造器的依赖注入（通过type（java的类型） 或者index（参数的索引） 来制定构造器的参数类型）


# TODO 继续阅读的起点
Dependency resolution process
1 20
Collection merging

# 配置文件属性的覆盖
在父子关系的两个bean中 子配置的属性会覆盖父的值

##Spring bean的作用范围（scope）
- singleton（默认）
 是指在spring Container里面只有一个bean 实例，设计模式中的单例是指ClassLoader中的bean 只有一个实例
- prototype 
 每次请求该bean的时候都会创建该bean的实例 所有有状态的bean都是使用prototype，无状态的bean使用singleton
- session
- request
- globalsession
- application

##  注解配置的spring

- `@Required`
- `@Autowired`
 JSR330的`@Inject`注解可以替换`@Autowired`？（JSR 330’s @Inject annotation can be used in place of Spring’s @Autowired annotation in the examples below. See here for more details
 ）
 - 可以在任意的方法上使用注解？
 - 可以在构造器上和成员上使用`@Autowired`
 
 ```
 public class MovieRecommender {

    @Autowired
    private MovieCatalog movieCatalog;

    private CustomerPreferenceDao customerPreferenceDao;

    @Autowired
    public MovieRecommender(CustomerPreferenceDao customerPreferenceDao) {
        this.customerPreferenceDao = customerPreferenceDao;
    }
    // ...
	}
 ```
 - 固定类型的数组、集合上都可以注解`@Autowired`
可以通过实现`org.springframework.core.Ordered`或者使用`@Order`或者标准的`@Priority`注解来实现数组、集合内部成员的排序。

####spring 文档5.9.3
- `@Qualifier` 注释注入指定的bean。所以 @Autowired 和 @Qualifier 结合使用时，自动注入的策略就从 byType 转变成 byName 了。

####5.9.6 @Resource
spring 支持使用JSR-250`@Resource`注解在成员变量或者setter方法上`@Resource`使用name属性来告知需要注入哪个类。

```
public class SimpleMovieLister {

    private MovieFinder movieFinder;

    @Resource(name="myMovieFinder")
    public void setMovieFinder(MovieFinder movieFinder) {
        this.movieFinder = movieFinder;
    }

}
```
如果没有指定name属性值，则会根据属性名，setter的方法名来推断

####5.9.6 @PostConstruct and @PreDestroy
###5.10 Classpath scanning（类路径扫描） and managed components（组件管理）

