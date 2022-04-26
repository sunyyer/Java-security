### 0x01 基本概念
Java反射机制是在运行状态时，对于任意的一个类，都能够获取到这个类的所有属性和方法，对于任意一个对象，都能够调用它的任意一个方法和属性（包括私有方法和属性），这种动态获取信息以及动态调用对象的方法的功能就称为java语言的反射机制。
Java反射机制是JAVA漏洞的重要一点。
### 0x02 如何实现
java中有几个类分别为`Class,Constructor,Method,Field`,一个类一般是抽象出了某一事物的特征，如果我们定义一个person类，实现一些写操作这些特征的方法：

```
class Person{
    private String name;
    private int age;
    private  double  height;
    private double  weight;

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public int getAge() {
        return age;
    }

    public void setAge(int age) {
        this.age = age;
    }

    public double getHeight() {
        return height;
    }

    public void setHeight(double height) {
        this.height = height;
    }

    public double getWeight() {
        return weight;
    }

    public void setWeight(double weight) {
        this.weight = weight;
    }

    public void show(){
        System.out.println("xxxxxx");
    }
}
```
上面那几个和反射相关的类同样是这样的——Class类抽象出了java中类的特征并提供了一些方法，Constructor抽象出了java中所有的构造函数的特性以及提供一些方法（和别的语言不同）。

那么如何实现*调用一个任意方法*呢？分为三步走：
1. 首先获得这个对象对应的Class类的实例
2. 因为Class这个类存储着一个类的所有信息：属性、方法、构造函数....所以可以通过Class类的实例来获取你想要调用的那个方法
3. 拿到了对应的方法后，我们可以给这个方法传入对应的参数来调用它。

用代码如何实现这三个流程
