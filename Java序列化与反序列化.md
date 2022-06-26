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
![](../Asstes/java1.jpg)
