### 0x01 基本概念
Java反射机制是在运行状态时，对于任意的一个类，都能够获取到这个类的所有属性和方法，对于任意一个对象，都能够调用它的任意一个方法和属性（包括私有方法和属性），这种动态获取信息以及动态调用对象的方法的功能就称为java语言的反射机制。
Java反射机制是JAVA漏洞的重要一点。
### 0x02 如何实现
java中有几个类分别为`Class,Constructor,Method,Field`,一个类一般是抽象出了某一事物的特征，如果我们定义一个person类，实现一写操作这些特征的方法：

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
