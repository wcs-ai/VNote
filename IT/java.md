## 一、java介绍：
::: alert-info
**简介**Java是一门面向对象编程语言，不仅吸收了C++语言的各种优点，还摒弃了C++里难以理解的多继承、指针等概念，因此Java语言具有功能强大和简单易用两个特征。Java可以编写桌面应用程序、Web应用程序、分布式系统和嵌入式系统应用程序等。
**运行原理**：java并非纯粹的解释性或编译型语言，java代码以`.java`为后缀名，运行时需要结果两次翻译，第一次是编译，经过自带的`javac`程序将源码编译为字节码，同目录下生成`.class`文件。第二次是经过jvm虚拟机对.class文件进行解释性翻译（可以控制为编译）。
:::
### a1、数据类型：
基本数据类型：数值、字符串、布尔、数组、字典。
Java支持的变量类型有：
- **类变量**：独立于方法之外的变量，用 static 修饰。类之内，方法、构造方法之外，使用static修饰，也称静态变量，一般为常量，且用常publick修饰。
- **实例变量**：独立于方法之外的变量，不过没有 static 修饰。在类中，但在方法、构造方法，语句块之外，随所在对象创建销毁。
- **局部变量**：类的方法中的变量。执行时创建、执行完成后销毁、不能用修饰符
```java
// 最外层的类，文件名需要与其一致，test.java
public class test{
    private static short age = 90;    // 类变量
    // 实例变量。
    public String name = "wcs";
    public Em(){
        name = "xsww";    //可访问上一层的变量。
    }
    // 主入口，必须，可这这里定义参数。
    publick static void main(){
        // 内置数据类型，局部变量。！！静态上下文中，无法访问外部的非静态变量。
        int y1,y2,y3;    // 声明。
        
        byte a = 10;    //(-128,127)
        short b = -110;    //(-32768,32767)
        int c = 15478;    //(-2,147,483,648  ,   2,147,483,647)
        long d = 90324930;    //(（-2^63）,（2^63-1）)
        float e =  234.532432f;    //浮点型最后要加个f。最多32位
        double t = 890.3243214321;    //最多64位。
        boolean g = true;
        char h = 'v'; //char类型，长度只能是1.
        String i = "this is a boy";
        
        System.out.print("Hello World");
    }
}
/*
>javac test.java    //第一次编译
>java test    //第二次翻译并运行。
*/
```
### a2、修饰符：
有访问控制修饰符：public、default、private、protected。
非访问控制修饰符：static、final、abstract、synchronized、transient、volatile
- default (即默认，什么也不写）: 在同一包内可见，不使用任何修饰符。使用对象：类、接口、变量、方法。
- private : 在同一类内可见。使用对象：变量、方法。 注意：不能修饰类（外部类）
- public : 对所有类可见。使用对象：类、接口、变量、方法
- protected : 对同一包内的类和所有子类可见。使用对象：变量、方法。 注意：不能修饰类（外部类）。
- static：静态方法**不能使用类的非静态变量**。静态方法从参数列表得到数据，然后计算这些数据。声明独立于对象的静态变量，无论一个类实例化多少对象，它的静态变量**只有一份拷贝**（即：被多个子类继承后也只有一份数据）。
- final：修饰的变量赋值后不能再更改，与static一样用于构建类变量。可以被继承，但不能被重写。
- void的使用：
```java
public class wcs{
    // 不使用void修饰符的函数需要定义类型，并返回值。
    private String vv(){
        return "vv";
    }
    public static void main(String[] args){
        name = "aa";
        // 不需要返回值。
    }
}
```
### a3、类内部变量的访问：
```java
public class xsww{
    public int a = 10;
    public static void change(){
        // 静态方法访问非静态变量需要继承的方式使用。
        b = new xsww();
        System.out.println(b.a);
    }
    public static void main(){
        ak = 5;
        cv = vv(ak);    //同时静态类方法可直接调用。
        System.out.print(cv);
    }
    public static String vv(short val){
        return val + 1;
    }
}
```