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

