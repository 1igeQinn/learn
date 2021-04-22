#Spring AOP
Spring AOP 的原理是***JDK动态代理***和***CGLIB字节码***，

- 动态代理：前者需要被代理类实现相应的接口， 也只有接口中的方法可以被JDK动态代理技术所处理；
- CGLIB后者实际上是生成一个子类，来覆盖被代理类， 那么父类的final方法就不能代理，因为父类的final方法不能被子类覆盖。

 一般Spring 默认有限使用JDK动态代理技术，只有在被代理类没有实现接口时，才会选择CGLIB技术来实现AOP。
  Spring 也提供了配置参数来强制选择使用CGLIB技术

  ```
  <aop:config proxy-target-class="true"/>
  //表示强制使用CGLIB技术来实现AOP
  ```


 ## 参考
 [AOP 那些事] (http://blog.jobbole.com/103213/)

