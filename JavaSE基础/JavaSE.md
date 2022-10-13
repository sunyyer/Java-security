# Java基础语法（面向过程）

## 变量和关键字

Java是强类型语言，只有明确定义了变量之后，才能使用！一旦被指定某个数据类型，那么它将始终被认为是对应的类型（和JS不同）。

定义一个变量的格式如下：

```java
[类型] [标识符（名字）] = [初始值（可选）]
    int a = 10;
```

注意：标识符不能为以下内容~

1. 标识符以由大小写字母，数字，下划线和$组成，不能以数字开头。
2. 大小写敏感。
3. 不能有空格、@、#、+、-、/ 等符号。
4. 应该使用有意义的名称，最好以小写字母开头
5. 不可以是true 或 false.
6. 不能与Java语言的关键字重名。

## 常量

常量就是无法修改值的变量，常量的值，只能定义一次：

```java
final int a = 10;
a = 10 //报错
```

常量前面必须添加final关键字，这只是final关键字的第一个用法，后门还会有更多语法。

## 注释

```java
//单行注释
/**
多行注释
**/
//TODO 待做标记
```

## 基本数据类型

Java中的数据类型分为基本数据类型和引用数据类型。

### 计算机中的二进制表示

略~

在Java中，无论试试小数还是整数，他们都要带有符号（和C语言不通，C语言有无符号数），所以，首位就作为我们的符号位，还是以4个bit为例，首位现在作为符号位（1代表复数，0代表正数）：

min: 1111 =>-(2^2+2^1+2^0) = -7

max: 0111 =>+(2^2+2^1+2^0) = 7

### 计算机中的加减法

#### 反码

- 正数的反码是其本身
- 负数的反码是在其源码的基础上，符号位不变，其余各个位取反。

#### 补码

- 正数的补码就是其本身
- 负数的补码是在其原码的基础上，符号位不变，其余各个位取反，最后+1.（在反码的基础上+1）

1+（-1）= 0001 + 1111 = （1）0000 = +0 因为就是4位，所以（1）被丢弃

JAVA用到的就是补码

### 整数类型

- byte 字节型（8个bit,一个字节） 范围：-128~++127
- short 短针型（16 bit）
- int 整形（32 bit）
- long 长整型 （16 bit）,最好需要加L
- BigInteger 最大

### 字符类型和字符串

- char字符型（16个bit，2个字节，它不带符号），字符要用单引号扩起来，如 `char = 's'`

  字符其实本质上也是数字，这些数字通过编码表进行映射，Java的char采用Unicode编码表，但是char只能表示一个字符，如果想要包含更多字符，就需要字符串。

- String字符串

  字符串就是Java中的字符串类型，它是一个类，创建出来的字符串本质上是一个对象，不是我们的基本类型。

  字符串是用 `""`号括起来的。

### 小数类型

- float 单精度浮点型（32 bit）
- double 双精度浮点型(64 bit)

### 布尔类型

- true
- false

## 类型转换

### 隐式类型转换

隐式类型转换支持字节数小的类型自动转换为字节数大的类型，整数类型自动转换为小数类型，转换规则如下：

byte-short(char)-int-long-float-double

float是比long更大的，小数存储用阶码

### 显示类型转换

显示类型转换也叫做强制型转换，违反隐式规则，强行转换。

```java
int i = 128;
byte b = (byte) i;
System.out.print(b);
//输出-128
```

### 数据类型自动提升

在参与运算时，所有的byte型、short型和char型的值将被提升到int型：

```java
byte b = 105;
b = b + 1;//wrong
System.out.print(b);
```

这个特性时由 Java**虚拟机规范** 定义的，也是为了提高运行的效率。

## 运算符

赋值运算符，算数运算符略~（整数除以整数，得到的依然是一个整数）

自增,自减同理~

```java
int a = 10;
a++;
++a;
System.out.println(a++); //10 先返回值，再自增
System.out.println(++a); //11 先自增，再返回值

int a = 10;
int b = 2;
System.out.println(b+++a++);//12
```

### 关系运算符

关系运算符的结果只能是布尔类型，也就是要么为真要么为假：

`> < == >= <= !=` 结果只能是boolean(布尔类型)

### 逻辑运算符

逻辑运算符两边只能是boolean类型或是关系/逻辑运算表达式，返回值只能是boolean：

```java
&& //与运算
|| //或运算
！ // 非运算，一般放在表达式最前面，表达式用括号括起来
```

### 位运算符

按位运算实际上是根据值的二进制编码来计算结果

```java
& //按位与，注意，返回的是运算后的同类型值，不是boolean
| //按位或
^ //按位异或
~ //按位非
```

### 三目运算符

为了简化代码，根据条件是否满足决定返回值

```java
int a = 7, b = 15;
String str = a > b ? "可以" : "不可以"
System.out.Println("今晚有时间吗？" + str);
```

## 流程控制

### 选择结构

选择结构包含 `if,switch`

#### if

```java
public class main {
    public static void main(String[] args) {
        int  a = 7;
        int  b = 5;
        if (a<b){
            System.out.println(a+b);
        }else if (a==b) {
            System.out.println(b);
        }else {
            System.out.println(a);
        }
        //System.out.println(a);
    }
}
```

其中 `if,else if ,else` 都不是必须的，且可以嵌套。

#### switch

switch采用二分思想进行查找。

### 循环结构

#### for

```java
public class main {
    public static void main(String[] args) {
        int  a = 7;
        int  b = 5;
        for (int i = 1 ;i < 40 ; i++){
            System.out.println("xixi");
        }
    }
}
```

- 初始条件：循环开始的条件，一般用于定义控制循环的变量。

- 循环条件：每轮循环开始之前，进行一次判断，如果满足则继续，不满足则结束，要求boolean变量或是boolean表达式。

- 更新：每轮循环结束后都会执行的内容，一般写增量表达式。

  初始条件，循环条件，更新不是缺一不可，甚至都可以缺。

#### while

while循环和for类似，但是它更加的简单，只需要添加维持循环的判断条件即可！

```java
while(循环条件){
//循环执行的内容
}
```

和for一样，每次循环开始，当循环条件不满足时，自动退出！那么有时候我们希望执行了我们的代码再去判断怎么办呢，我们可以使用do-while语句：

```java
do{
//
}while (false)
```

一定会执行do里面的内容，再做判断

####  break和continue

它两只能控制自己块里面的循环。

```java
public class main {
    public static void main(String[] args) {
        int  a = 7;
        int  b = 5;
        while (a < 10){
            if (a ==8)
            break;//执行到8结束
            System.out.println("xixi");
            a++;
        }
    }
}

		int  a = 7;
        while (a < 10){
           	a++;
            if (a ==8)
           
            continue;//执行到8略过。打印9和10.
            System.out.println("xixi");
```

# Java对象和多态（面向对象）

## 面向对象基础

对象基于类创建，类相当于一个模板，对象就是根据模板创建出来的实体（好比做一个月饼，模具就是类，月饼就是类的实现，也叫做对象）。类具有自己的属性，包括成员变量，成员方法等，我们可以调用类的成员方法让类进行一些操作。

```java
Scanner sc = new Scanner(System,in);
String str = sc.nextline();
System.out.println("输入" + str);
sc.close();		
```

所有的对象，都需要通过new关键字创建，基本数据类型不是对象，Java不是纯面象对象语言。

不是基本类型的变量，都是引用类型，引用类型变量代表一个对象，而基本数据类型变量，保存的是基于数据类型的值，可以通过引用来对对象进行操作。

## 类的基本结构

创建类的文件名称应该和类名一致。

### 成员变量

在类中，可以包含许多的成员变量，也叫做成员属性，成员字段通过`.`来访问类中的成员变量。我们可以通过类创建的对象来访问和修改这些变量。成员变量是属于对象的。

### 成员方法

```
public static void main(String[] args){
//Body
}
```

方法是语句的集合，是为了完成某件事而存在的。完成某件事情，可以有结果，也可以做了就做了，不返回结果。

#### 方法的定义与使用

在类中，我们可以定义自己的方法：

```java
[返回值类型] 方法名称([参数]){
//方法体
return 结果;		
}
```

- 返回值类型：可以是引用类型和基本类型，还可以是void，表示没有返回值
- 方法名称：和标识符的规则一致，和变量一样，规范小写字母开头
- 参数：例如方法需要计算两个数的和，那么我们就要把两个数到底是什么告诉方法，那么他们就可以作为参数传入方法
- 方法体：方法具体要干的事
- 结果：方法执行的结恶果通过return返回（如果返回类型为void，可以省略return）

非void犯法中，return关键字不一定需要放在最后，但是一定要保证方法在任何情况下都具有返回值；return也能用来提前结束整个方法，无论此时程执行到何处，无论return位于哪里，都会立即结束这个方法。



传入方法的参数，如果是基本类型，会在调用方法的时候，对参数的值进行复制，方法中的参数变量，不是我们传入的变量本身

```java
//输出还是a=5,b=3
public static void main(String[] args) {
        int a = 5;
        int b =3;
        Student s = new Student();
        s.swap(a,b);
        System.out.println("a="+a+"b="+b);
    }
}
```

传入方法的参数，如果是引用类型，那么传入的依然是该对象的引用！

方法之间可以相互调用

```java
public class Student {
    String name;
    int age;

    void a(){
        b();
    }
    void b(){
        a();
    }
}

```

当方法在自己内部调用自己时，称为递归调用，（递归调用很危险）

```java
int a(){
	return a();
}
```

#### 练习：

```java
//Student.java
public class Student {
    int age;
    String name;

    void study(){
        System.out.println("study");
    }
    void sport(){
        System.out.println("sport");
    }
    void speak(String word){
        System.out.println(name+":"+word);
    }
}
//main.java
import java.util.Scanner;

public class main {
    public static void main(String[] args) {
    Student s = new Student();
    s.name = "aa";
    s.age = 0;

    s.study();
    s.sport();

    s.speak("ss");
    }
}

```

#### 方法的重载

一个类中可以包含多个同名的方法，但是需要的形式参数不一样。（形式参数就是定义方法需要的参数，实际参数就传入的参数）方法的返回类型，可以相同，也可以不同，但是仅返回类型不同，是不允许的。

```java
//Test.java
public class Test {
   int sum(int a ,int b){
       return a+b;
    }
    double sum(double a,double b){
       return a+b;
    }
}
//main.java
public class main {
    public static void main(String[] args) {
    Test t = new Test();
        double a = t.sum(1.3,2);
    System.out.println(a);
    }
}
```

当有很多种重写的方法，那么传入实参后，到底进了哪个方法呢？

```java
//Test.java
public class Test {
   void a(int i){
       System.out.println("调用int");
    }
    void a(float i){
       System.out.println("FLOAT");
    }
    void a(short i){
       System.out.println("SHORT");
    }
    void a(double i){
       System.out.println("Double");
    }
}
//main.java
import java.util.Scanner;

public class main {
    public static void main(String[] args) {
    Test t = new Test();
    t.a(1);
    t.a(1.3);

    short s = 2;
    t.a(s);
    t.a(1.0F);
    }
}

调用int
Double
SHORT
FLOAT

```

#### 构造方法

构造方法没有返回值，也可以理解为，返回的是当前对象的引用，每一个类都默认自带一个无参构造方法

```java
public class Student {
    public Student() {
    }//即使什么都不写，也自带一个无参构造方法，只是默认是隐藏的
}
```

反编译就是把我们编译好的class文件变回java源代码

```java
Test test = new Test();//实际上存在Test（）这个方法，new关键字就是用来创建并得到引用的
//new+ 你想要使用的构造方法
```

这种方法没有写明返回值，但是每个类都必须具有这个方法，只有调用类的构造方法，才能创建类的对象。类要在一开始准备的所有东西，都会在构造方法里面执行，王城构造方法的内容后，才能创建出对象！

一般最常用的就是给成员属性赋初始值：

我们可以手动指定有参构造，当遇到名称冲突时，需要用到关键字

```java
public class Student {
    String name;
    Student(String name){  //形参和类成员变量了，java会优先使用形式参数定义的变量
        this.name = name;  //通过this指代当前的对象属性，this就代表当前对象
    }
}
```

注意：this只能用于指代当前对象的内容，因此，只有属于对象拥有的部分才可以使用this,也就是说，只能在类的成员方法中使用this，不能在静态方法中使用this关键字。

在我们定义了新的有参构造之后，默认的无参构造会被覆盖！如果同时需要有参和无参构造，那么就需要用到方法的重载，手动再去定义一个无参构造。

成员变量的初始化时钟在构造方法之前：

```java
public class Student {
    String a = "aa"
    Student(){
        System.out.println(a);
    }
    public static void main(String[] args){
        Student s = new Student();
    }
}
```

