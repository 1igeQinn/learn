# Ch13  字符串 String

##13.1 不可变的String
***String 对象是不可变的***，String类中每一个看起来会修改String值得方法，实际上都是创建了一个全新的String对象，以包含修改后的字符串的内容，而最初的String对象则丝毫未动。

##13.2 重载“+” 与StringBuilder
不可变性会带来一定的效率问题。为String重载的“+”操作符就是一个例子。***重载的意思是一个操作符在应用于特定的类时，被赋予了特殊的意义***。（用于String的`+`和`+=`是java中仅有的两个重载过的操作符。）

在循环中使用`+`号时会循环产生StringBuilder对象来连接。

```Java
public class StringTest{
	public static void main(String[] args){
		String mango = "mango";
		for(int i=0;i<20;i++){
		// 在循环中会重复的生成StringBuiler对象，使用其append方法来连接字符串。
			mango+=i;
		}
		System.out.println(mango);
	}
}
```
StringBuilder 是javaSE5引入的，在之前java用的是StringBuffer。StringBuffer是线程安全的，因而开销会大些。

##13.3 无意识的递归

```Java
import java.util.*
public class Test{
	public String toString(){
		//这里使用字符串拼接的时候 发现this不对String对象会对String进行转换为String（调用toString()方法），发生无限的循环递归。
		//如果要打印出该对象的地址，应该调用Object。toString()方法，而不应该使用this。
		return “Test address”+this+“\n”；
	}
	
	public static void main(String[] args){
		List<Test> test = new ArrayList<Test>();
		for (int i=0;i<10;i++){
			test.add(new Test());
		}
		System.oout.println(test.toString());
	}
}
```

##13.4 Strng 上的操作
##13.5 格式化输出
Java SE5 推出了格式化输出这一功能。
###13.5.1 printf()
讲解的c语言的printf使用
###13.5.2 System.out.format()
###13.5.3 ForMatter类
###13.5.4 格式化说明符

```
%[argument_index$][flags][width][.precison]conversion
```
最常见的应用是控制一个域的最小尺寸，这个可以通过指定width来实现。Formatter对象通过在必要时添加空格，来确保一个域至少达到某个长度，***在默认情况下数据是右对齐的，不过可以通过使用`-`来改变对齐的方向.***[P291](p291)

###13.5.5 Formatter转换
###13.5.6 String.format()
## 13.6 正则表达式
java中字符串的操作主要集中在String、StringBuffer、和StringTokenizer类。与正则表达式相比，他只是提供相当简单的功能。

###13.6.1
一个以“-”开头的数字 `-?`
`\d`表示一位数字
Java的\表示转义 \\表示一个\ 
对于换行和制表符只需要使用单反斜杠即可`\n\t`.
表示一个或多个用`+`
`-?\\d+`  可能有一个负号后面跟着一位或多位数字。

应用正则表达式的最简单的途径，就是String的内建功能（matchs()方法）。

```
"-1234".matchs("-?\\d+");
```

括号（`()`）有着将表达式分组的效果，`|`表示或操作，也就是：
（-|\\+)?

String 类还自带另一个非常有用的正则表达式的工具——split()方法，其功能是”将字符串从正则表达式匹配的地方切开“。

String.split() 还有一个重载的版本，它允许你限制字符串分割的次数。

###13.6.2 创建正则表达式
>java.util.regex.Pattern

###13.6.3 量词
>量词描述了一个模式吸收输入文本的方式。

- 贪婪型

贪婪表达式会为所有可能的模式发现尽可能多的匹配
- 勉强型

用问号来指定，这个量词匹配满足满足模式所需要的最少字符数。
- 占有型 [p299](p299)

这种类型只有在Java中才可用。 

###13.6.4 Pattern 和 Matcer
正则表达式对象

#####Group
组是用括号划分的正则表达式，可根据组的编号来引用某个组，***组号为0表示整个表达式。组号1表示第一对括号括起来的组***
A(B(C))D 中 0组是ABCD 1组是BC 2组是C
###13.6.5 split()
###13.6.6 替换操作


