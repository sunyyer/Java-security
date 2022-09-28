# 碎碎念

1. JVM是java可以跨多平台使用的原因，将.class二进制编译与各版本系统内核交互.

2. JRE是java的运行环境，不同操作系统都有自己的JRE.

3. JDK包含jre,同时提供开发工具。

4. C这种叫做编译型语言，编译为二进制后交互；python叫做解释性语言，通过python解释器运行。所以java既是编译性语言，也是解释性语言。

5. java必须包含一个主类，内部有一个主方法。

   ```java
   public class main {
       public static void main(String[] args) {
           System.out.println("hello world");
       }
   }
   ```

   



# Java语言规范

-  Java的所有语句必须以`；`结尾！

- 无论是（）、[]还是{}，所有括号必须一一匹配
- 主方法的代码只能写在{}中！