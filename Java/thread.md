Java内存模型定义了Java语言中的synchronized、volatile和final等关键词对主存中变量读写操作的意义

对声明为volatile的变量来说，在读取之前，JVM会确保CPU中缓存的值首先会失效，重新从主存中进行读取；而写入之后，新的值会被马上写入到主存中。

而synchronized和volatile关键词也会对编译器优化时候的代码重排带来额外的限制。比如编译器不能把 synchronized块中的代码移出来。对volatile变量的读写操作是不能与其它读写操作一块重新排列的。


wait noity notifyAll 

中断请求
interrupt()

isInterrupt()

sleep 和yeild方法将在当前正在执行的线程上原型。

Thread 类的setDaemon(true) 方法 可以将线程设置为守护线程。需要注意的是在调用start()方法前调用这个方法，否则会抛出IllegalThreadStateException 异常。


ThreadLocal用于创建线程本地变量，一个对象的所有的线程会共享全局变量，所以这些变量不是线程安全的，我们可以使用同步技术但是 我们不想使用同步的时候，可以使用threadlocal变量。


synchronized  lock method  synchronized block

锁住方法就锁住了整个对象，如果方法是静态的，则锁住了整个类（Class） 所以使用synchronized的最好的方式是锁住区域块儿，

当创建synchronize块的时候，我们需要提供资源来被lock，可以是class或者对象的任何属性


join()