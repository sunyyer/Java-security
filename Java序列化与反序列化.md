### 0x01

java的序列化机制就是为了持久化存储某个对象或者网络上传输某个对象。一旦jvm关闭，那么java中的对象也就会销毁掉，所以想要保存它，就需要把它转换为字节序列写道某个文件或者是其它地方。

序列化：把对象转换为字节序列
反序列化：把字节序列转换为对象

### 0x02

一个类对象要想实现序列化，必须满足两个条件：
1. 该类必须实现java.io.Serializable对象。
2. 该类的所有属性必须是可系列化的。

### 0x03

要序列化一个对象，首先要创建OutputStream对象，再将其封装在一个ObjectOutputStream对象内，接着只需要调用writeObject()即可将对象序列化，并将其发送给OutputStream(对象是基于字节的，因此要使用InputStream和OutputStream来继承层次结构)。
要反序列化一个对象，需要将一个InputStream封装在ObjectInputSteam内，然后调用readObject()即可。上代码：

```
import java.io.*;

public class Test{
  public static void main(String[] args){
    User user = new User("syy", 18, 180);
    try{
      //创建一个FileOutputStream}}}
```
### 0x04 反序列化漏洞
反序列化漏洞是指在反序列化过程中自动执行类中readObject方法导致的漏洞，类似于PHP反序列化时会自动执行__wakeup方法一样。如果readObject中执行了某种危险的操作，就可能到做反序列化漏洞。

实际情况不会有这么简单的情况，真实的环境下一定是一种利用链的调用关系。
![](https://github.com/sunyyer/Java-security/blob/23d75db16555fb7960573d2291c736406720f40b/Asstes/picture/java1.jpg)
反序列化调用链从本质来说就是构造一条从反序列化入口Source到危险方法Sink的调用链。反序列化的Source点一定是从readObject方法开始，但是Sink点却可以有很多种不同的类型。最常见的反序列化Sink是命令执行，但是也有可能是文件上传、SSRF、XXE等其他类型的Sink。

### 0x04 JAVA与PHP反序列化对比

- 反序列化的数据存储格式
### 0x04 JAVA与PHP反序列化对比

1) **反序列化的数据存储格式**

JAVA序列化之后的数据是满足特定序列化协议的字符流，PHP序列化之后是一种类似json的格式。JAVA序列化之后的数据是不可读的，PHP序列化之后的数据是可读的。如图:

![](https://github.com/sunyyer/Java-security/blob/2fdb94a51d4a636064aafd84d6545acd864d73a4/Asstes/picture/java2.jpg)

不同语言对于序列化有不同的实现方式，同一种语言也有多种不同的序列化方式。相对于JAVA而言，PHP的序列化可读性更强，序列化之后的数据可以按照字段含义进行直接修改。

2) **反序列化触发点不同**

从上面的关于JAVA反序列化的分析中可以看出，JAVA反序列化的入口点Source是readObject方法。而PHP与JAVA不同，PHP反序列化的入口点Source是__wakeup和__destruct方法。

3) **类加载机制不同**

在PHP中要调用某个类必须要引入，PHP引入类文件常见的是这四种方式require、require_once、inclue、include_once。在反序列化的过程中，反序列化利用链中的每一个类也都必须是显式引入的，即必须通过上面四个函数中的某一个引入对应的类文件。如果不引入，就会报错。

与PHP的类加载机制不同，JAVA中类加载只与classpath有关，只要是在classpath中的类就能被直接调用。JAVA中并不要求在调用类之前进行显式引入，一般来说项目jar包中的类都可以任意调用。这也是java反序列化漏洞远比PHP反序列化漏洞多的原因之一。

4) 应用场景不同

PHP一般用于中小型项目，项目一般比较简单，代码较少。传统PHP项目是直接编写代码，现在的PHP项目会采用一些主流的PHP框架。但是PHP项目中很少使用其他第三方的组件（其实现在已经慢慢开始流行使用composer来加载第三方组件了）。

JAVA一般用于大型项目，项目结构和功能复杂，代码较多。JAVA项目中一般会引入大量第三方jar包，而第三方jar包通常是反序列化利用链的重要组成部分。

### 0x05 Conclusion

JAVA反序列化是经典的JAVA漏洞，上面的文章分析的都是JDK中最常见的序列化和反序列化方式。但是JAVA中还有其他的序列化和反序列化方式，包括：基于Externalizable接口的序列化和反序列化、基于fastjson的序列化与反序列化、基于XStream的序列化与反序列化、基于jackson的序列化与反序列化等。每一种序列化与反序列化都可能出现对应的反序列化漏洞，而这也是研究反序列化漏洞的重要组成部分。
