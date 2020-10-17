#Lambda 表达式 和函数式接口
```

Arrays.asList("a","b","c").forEach(e -> System.out.println(e))
// 编译器会根据上下文推测参数的类型。 或者也可以显示的指定参数类型。
Arrays.asList("a","b","c").forEach((String e) -> System.out.println(e))

```

接口的默认方法和静态方法。
Java 8 允许通过`default` 关键字来为接口添加默认实现的方法，

```
interface Foumula{
    double calculate(int a);
    default double sqrt(int a){
        return Math.sqrt(a);
    }
}
```


## 4 新的特性
###4.1 Optional
Optional 只是一个容器，它 可以保存一些类型的