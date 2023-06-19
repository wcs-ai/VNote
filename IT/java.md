

# 一、java语言

## a0、基础概念

**简介**Java 是一门面向对象编程语言，不仅吸收了 C++语言的各种优点，还摒弃了 C++里难以理解的多继承、指针等概念，因此 Java 语言具有功能强大和简单易用两个特征。Java 可以编写桌面应用程序、Web 应用程序、分布式系统和嵌入式系统应用程序等。
**运行原理**：java 并非纯粹的解释性或编译型语言，java 代码以`.java`为后缀名，运行时需要结果两次翻译；
第一次是编译，经过自带的`javac`程序将源码编译为字节码，同目录下生成`.class`文件。
第二次是经过 jvm 虚拟机对.class 文件进行解释性翻译（可以控制为编译）。

**JDK**：(java development kit)，java最小**开发环境**，主要有3部分，如下：
（1）第一部分就是Java运行时环境，`JVM`。
（2）第二部分就是Java的基础类库，这个类库的数量还是非常可观的。
（3）第三部分就是Java的开发工具，它们都是辅助你更好的使用Java的利器。

**JRE**：(java runtime environment) ， java**运行时环境**

**JVM**：java virtuak machine （java虚拟机）JAVA的程序也就是我们编译的代码都会**编译为Class文件**，Class文件就是在JVM上运行的文件
**jar包**：是一种归档文件，以[ZIP格式](https://baike.baidu.com/item/ZIP格式?fromModule=lemma_inlink)构建，以.jar为[文件扩展名](https://baike.baidu.com/item/文件扩展名?fromModule=lemma_inlink)。一个可执行的jar 文件是一个自包含的 Java 应用程序，它存储在特别配置的JAR 文件中，可以由 JVM 直接执行它而无需事先提取文件或者设置类路径

注：项目

## a1、数据类型：

基本数据类型：数值、字符串、布尔、数组、字典。
Java 支持的变量类型有：

- **类变量**：独立于方法之外的变量，用 static 修饰。类之内，方法、构造方法之外，使用 static 修饰，也称静态变量，一般为常量，且用常 publick 修饰。
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

1、字符串：

```java
String str = "con";
str.length();
str.charAt(1);	// 返回指定位置字符
/*******获取指定范围的字符串******/
str.substring(开始位置,结束位置);
String s1 = str.concat("new");// 链接两个字符，返回结果
String s2 = str.toUpperCase();// 返回大写
String s3 = str.toLowerCase();// 返回小写
String s4 = str.trim(); // 去掉两侧空格字符
s1.equal(s2); // 比较s1和s2
s1.contains(s2); // 检测s1是否包含s2
// 检测是否以指定字符串开头/结尾
s1.startWith("pre");
s1.endWith("tail");
// 获取子字符串位置
s1.indexOf("c",开始位置);
s2.lastIndexOf("b",开始位置);

```

​		**正则匹配**：

```java
/********正则匹配********/
str.matches("^[c]"); // 返回布尔值
str.replaceAll("c","bbv"); // 替换全部匹配到的
str.replaceFirst("c","aaf"); // 替换第1个匹配的
str.split("o",匹配次数); // 字符串分割
/*****创建正则表达式*****/
Pattern p = Pattern.compile("^jav");
Matcher m = p.matcher(s1);
if(m.find()){
	System.out.println(m.groupCount()); // 匹配到的组数
    System.out.println(m.group(0)); // 读取第1组匹配值
    System.out.println(m.matches());// 布尔值
    System.out.println(m.start());// 开始位置
    System.out.println(m.end());// 结束位置
}
```

​		**stringBuffer**：

```java
// 方便字符串拼接处理
StringBuffer buffer = new StringBuffer();
buffer.append("{"); // 向后拼接字符
buffer.length(); // 长度
buffer.deleteCharAt(3); // 删除指定位置的字符
buffer.toString(); // 转为string类型
```

2、Map

类做Map使用：

```java
import java.util.Arrays;
import java.util.List;

public class Word {
    private final String type = "word";

    // 单词的最后一个字母
    public String word;
    // 词性
    public String property;
    // 词意
    public String definition = "";
    // 父节点位置
    public int pre;
}
```

使用util.Map

```java
import java.util.Map;

Map<String,Integer> nexts;
// TreeMap是以搜索树类型创建
Map<String,Integer> mps = new TreeMap<>();
// 散列表方法实现的map
Map<String,Integer> mps2 = new HashMap<>();
mps2.size(); //大小
mps.put("key","val"); // 存值
mps.get("key"); // 获取值
mps.getOrDefault("bbc","default value");
mps.remove("key"); // 移除key
/*****Map遍历*****/
Set<Map.Entry<String,String>> entrySet = mps.entrySet();
for(Map.Entry<String,String> entry:entrySet){
    System.out.println(entry.getKey()+entry.getValue());
}
// 或者
for(String key:jsonMap.keySet()){
	System.out.println(key);
}
```

**Map转json**：一般使用第3方库；实现思路：遍历Map，拼接为json字符串；

```java
public class MapToJson {
    public static String map2json(Map<String,String> jsonMap){
        StringBuffer buffer = new StringBuffer();
        buffer.append("{");
        if(jsonMap.size()>0){
            for(String key:jsonMap.keySet()){
                buffer.append('"'+key+'"'+":"+'"'+jsonMap.get(key)+'"'+',');
                //System.out.println(key);
            }
            // 去掉最后1个，号
            buffer.deleteCharAt(buffer.length()-1);
        }
        buffer.append("}");
        return buffer.toString();
    }
}
```



## a2、修饰符：

有访问控制修饰符：public、default、private、protected。
非访问控制修饰符：static、final、abstract、synchronized、transient、volatile

- default (即默认，什么也不写）: 在同一包内可见，不使用任何修饰符。使用对象：类、接口、变量、方法。
- private : 在同一类内可见。使用对象：变量、方法。 注意：不能修饰类（外部类）
- public : 对所有类可见。使用对象：类、接口、变量、方法
- protected : 对同一包内的类和所有子类可见。使用对象：变量、方法。 注意：不能修饰类（外部类）。
- static：静态方法**不能使用类的非静态变量**。静态方法从参数列表得到数据，然后计算这些数据。声明独立于对象的静态变量，无论一个类实例化多少对象，它的静态变量**只有一份拷贝**（即：被多个子类继承后也只有一份数据）。
- final：修饰的变量赋值后不能再更改，与 static 一样用于构建类变量。可以被继承，但不能被重写。
- void 的使用：

```java
public class Wcs{
    public static String name = "name";
    // 不使用void修饰符的函数需要定义类型，并返回值。
    private String vv(){
        return "vv";
    }
    public static void main(String[] args){
        name = "aa"; // staic类型可互相直接调用
        // 不需要返回值。
    }
}
// 外部可直接调用static修饰部分
Wcs.name;
```

## a3、文件IO

1、读取文件

```java
import java.io.*;
import java.util.*;

public class App {
    private static String FINE_PATH = "F:\\webPritice\\test.txt";

    public static void main(String[] args) {
        File file = new File(FINE_PATH);
        System.out.println("文件存在？"+file.exists());
        System.out.println("文件长-"+file.length());

        // 对文件的操作必须使用，异常捕获包裹
        try{
            /*****第1种方法*******/
            FileInputStream inputStream = new FileInputStream(file);
            List<Byte> bs = new ArrayList<>();
            int b;
            
            while((b=inputStream.read())!=-1){
                bs.add((byte) b);
            }
            byte[] bytes = new byte[bs.size()];
            for(int i=0;i<bs.size();i++){
                bytes[i] = bs.get(i);
            }
            // print
            System.out.println(new String(bytes));

            /*****第2种读取方式*****/
            Scanner input = new Scanner(file);
            while(input.hasNext()){
                System.out.println(input.next());
            }
            
            /******覆盖的方式写入文件******/
            FileOutputStream outputStream = new FileOutputStream(file);
            String str = "hello world";
            outputStream.write(str.getBytes());
        }catch(IOException e){
            throw new RuntimeException(e);
        }

    }
}

```

# 二、包管理工具

## 1、maven 仓库

安装：[maven 下载安装](http://mvnbook.com/maven-download.html)

- 下载maven包后，环境变量配置`MAVEN_HOME`，path变量中放置`%MAVEN_HOME%\bin`。项目依赖可放在 targed/dependency

- 查看本地 mvn 仓库位置：`mvn help:effective-settings`

- 按 pom.xml 文件下载依赖：pom.xml 所在目录 cmd 命令：`mvn dependency:copy-dependencies`

- `pom.xml`用于管理：源代码、配置文件、开发者的信息和角色、问题追踪系统、组织信息、项目授权、项目的url、项目的依赖关系等等；结构：

  ```xml
  <?xml version="1.0" encoding="UTF-8"?>
  <!--根元素-->
  <project xmlns="http://maven.apache.org/POM/4.0.0"
           xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
           xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
      <modelVersion>4.0.0</modelVersion><!--当前POM模型的版本-->
      <groupId>org.example</groupId><!--项目组的标识-->
      <artifactId>English</artifactId><!--工程的名称-->
      <version>1.0-SNAPSHOT</version><!--区分同一个artifact的不同版本-->
      <properties>
          <maven.compiler.source>8</maven.compiler.source>
          <maven.compiler.target>8</maven.compiler.target>
      </properties>
  </project>
  ```

**创建一个 maven 项目**：使用idea先传一个maven项目，`file/setting/Build/Tool`下配置maven路径，如下：
（1）maven home director：放置maven包的路径（如`D:/maven`）；
（2）setting file：配置文件：`maven/conf/setting.xml`；
（3）local repository：本地放置maven依赖的仓库；（勾选overide）

javaFx：
[javaFx 下载地址](https://gluonhq.com/products/javafx/)
[javaFx 文档](http://www.javafxchina.net/blog/docs/)、[3d 模型文件导入](https://blog.csdn.net/weixin_38581615/article/details/70946391)

## 2、gradle

**简介**：Gradle是一种以Groovy语言为基础的自动化构建工具。

**安装**：[graddle下载地址](https://services.gradle.org/distributions/)、[参考地址](https://blog.csdn.net/Leoon123/article/details/125717416)
**环境变量配置**：配置`GRADLE_USER_HOME`指定（gradle没有可指定仓库位置的配置）`gradle目录/bin`放到`Path`变量中。
gradle包下载配置：构建的gradle项目中都会有指定下载gradle的版本包地址，一般如下：

```properties
#一般是在gradle-wrapper.properties下
#distributionUrl=https\://services.gradle.org/distributions/gradle-7.6.1-bin.zip
#将其修改为本地已存在的包地址即可跳过下载步骤
distributionUrl=file:///D:/gradle7/gradle-7.5.1-all.zip
```

`build.gradle`文件：包含项目构建所使用的脚本，指定的依赖等。默认的构建脚本，当我们在执行 gradle 命令时，会首先到当前目录下寻找该文件

```groovy
//构建脚本（给脚本用的脚本）
buildscript {
    //存储一个属于gradle的变量，整个工程都能用，可通过gradle.ext.springBootVersion使用
    ext {
        springBootVersion = '2.1.2.RELEASE'
    }
    /*配置仓库地址，从而找到外部依赖
    按照你在文件中(build.gradle)仓库的顺序寻找所需依赖(如jar文件)，如果在某个仓库中找到了，那么将不再其它仓库中寻找
    */
    repositories {
        //mavenLocal()本地库，local repository(${user.home}/.m2/repository)
        mavenCentral()//maven的中央仓库
        //阿里云Maven远程仓库
        maven { url "http://maven.aliyun.com/nexus/content/groups/public/" }
    }
    /*配置springboot插件加载*/
    dependencies {
        // classpath 声明说明了在执行其余的脚本时，ClassLoader 可以使用这些依赖项
        classpath("org.springframework.boot:spring-boot-gradle-plugin:${springBootVersion}")
    }
}
//使用以下插件
apply plugin: 'java'
apply plugin: 'org.springframework.boot'
apply plugin: 'io.spring.dependency-management'
 
group = 'com.example'
version = '0.0.1-SNAPSHOT'
sourceCompatibility = '1.8'//jvm版本要求
// 定义仓库
repositories {
    maven{url 'http://maven.aliyun.com/nexus/content/groups/public/'}
    maven{url 'https://mvnrepository.com/'}
    mavenCentral()
}
// 定义依赖:声明项目中需要哪些依赖
dependencies {
    compile  'org.springframework.boot:spring-boot-starter'
    compile('org.springframework.boot:spring-boot-starter-web')//引入web模块，springmvc
    compile  'org.springframework.boot:spring-boot-starter-test'
}
```

`setting.gradle`： 用来告诉 gradle 这个项目包含了那些**子项目**。

**安装依赖**：到项目目录下（`build.gradle`目录）用`gradlew downloadjars`下载其指定的依赖。

**注**：各项目**指定的gradle版本号不一样**，需要先下载相应版本的gradle才行（idea使用处查看）

# 三、框架

**Spring 框架**：是一个[开放源代码](https://baike.baidu.com/item/开放源代码/114160?fromModule=lemma_inlink)的[J2EE](https://baike.baidu.com/item/J2EE/110838?fromModule=lemma_inlink)应用程序框架，是针对bean的生命周期进行管理的轻量级容器，提供了功能强大IOC、[AOP](https://baike.baidu.com/item/AOP/1332219?fromModule=lemma_inlink)及Web MVC等功能。
Spring可以单独应用于构筑应用程序，也可以和Struts、Webwork、Tapestry等众多Web框架组合使用。

**Spring Boot** ：并不是 Spring 的精简版本，而是为使用 Spring 做好各种产品级准备。

**Spring MVC** ：实现了 We 项目中的 MVC 模式 如果 Spring Boot Web 项目，就可以选择采用 Spring MVC MVC 模式 当然也可以选择 似的框架来实现。

**Spring Cloud** ：该框架可以实现一整套分布式系统的解决方案（当然其中也包括微服务架构的方案），包括服务注册 服务发现 监控等， Spring Boot 作为开发单 服务的框架的基础

## a、spring boot

**安装**：下载spring boot cli包后，将其`/bin`路径放置到环境变量的path中，`spring --version`成功即可

**创建sprint boot项目**：使用`idea`
（1）**安装sprint assistant插件**：setting/plugins搜索安装该插件，**用于创建sprint boot项目**
（2）重启ide后：`file/new/project`中选择sprint assistant创建，选default》next》选jdk版本好，项目名》选依赖

[sprint boot教程](https://www.yiibai.com/spring-boot/installing-spring-boot.html)

# 四、idea使用

**设置jdk环境**：`setting/Build/Build Tools/Maver`或Gradle（根据自己项目用哪个决定）下选择指定的jdk版本，位置配置即可。
**安装gradle/maven**：最右侧栏有`gradle/maven`按钮，点击展开，然后点刷新，idea会下载配置指定的`maven/gradle`版本。
`.idea目录`：配置

**操作集**：

- 单文件搜索：`ctrl+F`搜搜即可。
- 全项目搜索：双击`shift`，上方切换搜索的类型。

**问题集**：

- idea右键新建文件没有java class选项：文件有`java file outside of source`提示，`file/project structure/modules`选择要支持的目录，点击source按钮，点击应用。