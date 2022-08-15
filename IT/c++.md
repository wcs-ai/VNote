# 1、环境配置：
- 环境安装：linux系统自带c++，win上可以安装vs直接开发。到vs官网下载社区免费版，登录可免费试用。
- 创建：用vs创建一个c++工程。主入口文件放在：**源文件**下，默认为：`源.cpp`。
- 头部文件：一般放置定义的常量、类型（用`.h`或`.hpp`做扩展名）。也可以是一些图片、xml等资源文件。
- 引入其它自定义模块：
```c++
/*<>：该符号包含的头文件表示：让编译器在（编译器的预设标准路径下）去搜索相应的头文件*/
#include <iostream>            //导入自带的模块
#include "module/line.cpp"     //导入自己写的cpp文件。不能含有main()函数。
using namespace std;           //*******告诉编译器使用 std 命名空间，(不然一些头文件方法无法使用)***********
#define TYPE true             //定义一个常量。【注意：后面不加分号，不然使用时报错】
// 变量声明（外部声明过的则是全局变量）
extern float f;                //extern通常用于当有两个或多个文件共享相同的全局变量或函数
i++; //先引用后增加，先在i所在的表达式中使用i的当前值，后让i加1
++i; //先增加后引用，让i先加1，然后在i所在的表达式中使用i的新值
// main为主入口函数。只能在主入口文件使用。
int main(){
    hello();                   //hello()是：line.cpp文件中定义的，可直接掉用。
    // 条件编译
    #ifdef TYPE                //只要值TYPE有声明，被#ifdef和#endif包围的代码块会被加入编译。
    cout << "值TYPE存在";
    #endif

    return 0;                  // 非void修饰的函数，需要返回值来中断函数运行
}
```
# 2、数据类型
## a、数值
```c++
/**************数值************/
int x = 10;
float a = 2.5;
int ig;
// 对计算的浮点数化为整型（下舍的处理）
```
- 整数与整数计算得到整数：`1 / 2 = 0; 3 / 2 = 1`（有小数时也会被下舍处理）
- 浮点数与**整数**计算得到浮点数：`3.0 / 2 = 1.5`;
- 浮点与浮点计算也可得到整型：`1.5 + 2.5 = 4`;
- 浮点转整型：`(int)(2.5 + 2.4); // = 4`
- 取整：`abs(-10)=10;abs(-2.7)=2.7;`
**输入&输出**：

```c++
/*==============
    输入：cin,scanf
================*/
char name[5];
cin >> name;                  //输入的值，赋给name。
cin.getline();                //接受一个字符串的输入包括空格，遇到回车停止。
cin.clear();                  //清除异常
scanf("%s",aa);               //也可以调用输入，赋值给aa。
/*===============
    输出：cout,clog,cerr
=================*/
clog << "Error message:" << endl;        // clog用于打印日志
cerr << "Error message:" << endl;        // cerr打印错误流
cout << "result" << endl;                // 输出。endl表示结束
system("exit");               //退出命令框
```

## b、字符&字符串
字符的长度都是1，没有字符串的数据类型，不过c++库中有实现string可使用；
```c++
// 字符串存储为char数组
char sc[] = "abcd"; // ['a','b','c','d']
char cc = 'h'; //使用与char类型相关的必须用【单引号】如：if(cha=='h'){}
/******************数组*****************/
const int vv = 10;
char hh[vv];	//vv必须是一个常量
// 得出数组长度
sizeof(arr);
```
**string头文件常用方法**：string类型的实现

```c++
#include <string>
using namespace std;
int main(){
	string s1 = "hello";
    string s2 = "wordk";
    s1.insert(4, "\s");// 第1个参数位置插入第二个参数
    s2.erase(4, 1); // 第4个位置删除第2个参数指定长度的字符
    s1.find("o", 0); // 指定从第2个参数位置，在s1中查找第1个参数出现的位置
    std::cout << s1.length() << s1+s2 << s2.substr(0,2);
    return 0;
}
```

**字符串的简单实现**：

string头文件实现的字符串类型与基本数据类型相似，这实现上较困难，简单点的用结构体实现方式如下：

```c++
// *********字符串的实现**********
typedef struct {
	char* ch;
	int length;
} Str;

int strassign(Str &str,char* ch){
	// 释放ch
	if (str.ch) free(str.ch);
	// ch的指针
	char* c = ch;
	int len = 0;
	// *c是取其值
	while (*c) {
		++len;
		// 地址位+1
		++c;
	}
	if (len == 0) {
		str.ch = NULL;
		str.length = 0;
		return 1;
	}
	else {
		// malloc （memory allocation动态内存分配）申请一块连续指定大小的内存区域，以void形式返回分配的地址;
		str.ch = (char*)malloc(sizeof(char) * (len + 1));
		// 申请空间失败时会返回NULL指针
		if (str.ch == NULL) return 0;
		else {
			c = ch;
			for (int i = 0;i < len; ++i, ++c) {
				// 每位字符存到字符地址数组中
				str.ch[i] = *c;
			}
			str.length = len;
			return 1;
		}
	}
}
char s2[] = "fdsfdsf";Str s3;
strassign(s3, s2);
std::cout << s3.length;
```

## c、字符数值互转

法1：使用stringstream
```c++
#include <iostream>
#include <string>
#include <sstream>
int main(){
    int i = 1;
    float f = 1.2;
    double d = 1.23;
    stringstream ss1;
    // ****数值转字符*****：拼接赋值给ss1,
    ss1 << i << " " << f << d << endl;
    string result = ss1.str();
    std::cout << result;
    // ****字符转数值*****
    string stc = "12.3";
    stringstream ss2(stc);

    ss2 >> i >> f;
    std::cout << "\ni=" << i << "\nf=" << f;
}
```
法2：使用函数方法直接转换
```c++
string str = "123.56";
int i = stoi(str);
float f = stof(str);
double d = stof(str);
```

## d、字符数值类型判断

```c++
#include <cctype>
using namespace std;
int main(){
    char a = 'a';
    bool ig = isalpha(a); // 判断是否是字符，类似的方法还有如下：
    /*isalnum(): 是否为数值；isblank(): 是否空白符；incntrl(): 是否是控制符；issupper(): 是否大写；
    * isgraph(): 是否带有图形的；islower(): 是否小写；isprint(): 是否可打印；ispunct(): 是否标点符；
    * tolower(): 转为小写；toupper(): 转为大写；
    */
    return 0;
}
```
## e、其它
```c++
unsigned a;        //表示可能是任何类型的变量。
auto c = 10.25;    //auto：然编译器自动适应类型。
/************typedef*****************/
// 为现有类型创建一个新的名字。
typedef int Pop[3];
Pop cx = {1,2,3};  //直接用Pop作为一个类型。特别在结构体较常用！
void sc = 89;      //void修饰的可为任意类型，但数组、函数的参数，不能是void类型。

/**************** 结构体(struct)******************/
// 是由一系列具有相同类型或不同类型的数据构成的数据集合，叫做结构。

struct Book {
	string title;
	int pages;
	bool isFree;
  struct Book *next;  //结构体内指针。
} *Bpoint;            //后面可以顺便定义1个该结构体的指针。

Book book;            //用声明好的Book结构，来定义一个该格式的结构体。
book.title = "title";
Bpoint bot = &book;   //指针bot指向book地址。
cout << bot->next;    //用箭头符号来获取指针。
/***************new的使用************/
//new用于动态存储，申请一个存储空间，返回一个地址指针。
auto s = new Book;    

qee.front = qee.rear = new QNode;       //这种赋值会公用一个节点空间。
qee.rear->data = 10;
cout << "val:" << qee.front->data;     //10
auto cc = (s*)malloc(sizeof(Book));    //malloc()函数分配指定长字节的存储空间。
/***********函数***********/
int acc(int p){return 0;}                //return表示结束函数，值类型要与函数类型一致
/*
    第一个参数为普通形参，修改形参值不改变外面实际传入数据。
    第二个参数为指针传参，指向实际数据地址。
    第三个参数为引用传参，修改其值也会修改外面的实际值。
*/
void ahh(string k,int *cc,int &op){     //void类型可以不用返回任何值。
    op = 799;
    cc = &op;
}
```
# 3、符号

## a、普通运算符
`&`：**返回变量的地址**，如&a表示给出变量a的实际地址。
`*`：将指向一个变量，如`*a`，`LNODE* p`表示指向p，但`a * b`表示两数相乘。
`<<=`：左移且赋值运算符，C <<= 2 等同于 C = C << 2
`<<`：二进制左移运算符。将一个运算对象的各二进制位全部左移若干位。

%：取模运算符；

## b、作用域运算符::

```c++
// *****输入输出时有用
int ff = 24;s
int main(){
    std::cout << "hello world";
    std::cin >> a;
    // 使用全局变量时，前面加::
    ::ff = 30;
}
// *****类外部定义成员，引用时
// ---Box.h文件：
class Box {
public:
	// 这个Box就是该类的构造函数（名称与类名一致）每次调用类时会执行
	Box(double lengthValue, double widthValue, double heightValue);
	// 多个构造函数时，参数一定不能相同
	Box();
	double volume();
};
#endif
// ---Box.cpp文件：
#include <iostream>
#include "box.h"
// ::号引用头文件定义的函数
Box::Box(double lengthValue, double widthValue, double heightValue) {
	std::cout << "first counstruct";
}
Box::Box() { std::cout << "second construct"; }
double Box::volume() { return length * width * height; }
```
# 4、指针
指针是一个变量，其值为另一个变量的地址。(变量地址也必须赋值给指针！)。**引用**：引用变量是一个别名，也就是说，它是某个已存在变量的另一个名字。

```c++

typedef struct LNode {
	int data;
	struct LNode* next;
}LNode,*LinkList;

int main(){
    string a = "hello";
    // *表示该变量是一个指针（指针用于指向一个存储地址【十六进制数】）
    int *point = &a;
    /*****注意使用时，point是变量地址，*point则是直接取变量值*********/
    std::cout << point << "\t" << *point; // 90SF3240K	hello
    // 变量前使用&符号，可以获取其在主存中的位置！
    cout << "a 的地址：" << point;
    double &s = a;                    // 引用变量a，相当于指向a的地址。用&表示引用。
    a = "world";                      // a改变，s也会改变。
    /*****指针地址可循环******/
    char s2 = '6';
    char* z = &s2;
    int i = 0;
    while(*z){
        std::cout << ++i << "\n";//1,2,..,24 最后一次数即是该地址的长度
        ++z;// 变量地址+1，取到的变量值*z随之改变
    }
    LNode na1,na2;
    na1.data = 10;na2.data = 11;      // 两个节点。
    LinkList la,lb;                   // 两个LinkList类型指针。
    la = &na1;
    la->next = &na2;                  // 节点1指针指向节点2.
    return 0;
}
/**============
    new操作符：
动态的申请一个存储空间，数值，字符，数组等都可以用new，返回数据所处的地址，用指针来接收他们；
=============*/
int *y = new int(10);
float *x = new float[5]; //x[0]; 可用序号来使用
```
# 5、泛型模板

```c++
/*********类的泛型********
用于泛型编程，其定义的T，作为泛型（T声明的类型可以任意）
*/
template <class T>
struct chainNode {
   // T定义了“element”可以是任意类型的
	T element;
	chainNode<T>* next;
	chainNode() {}
    // mutable指定的变量，即使外面用了const，【该变量总是可以被修改】
    mutable string name;
    /*
    &定义参数“element”为引用类型
    T定义参数“element”为任意类型
    *******const********
    定义“element”为一个常量，所以“element”失去了引用类型的作用，
    不过这里结合使用可启到【不copy“element”】的作用（即：不会多请求内存空间）
    */
	chainNode(const T& element) { this->element = element; }
};
/*******const******
用在函数后表示【该函数不会修改所属成员变量】否则编译错误
用在函数前表示【该函数的返回值不可改变】
*/
bool empty() const { return listSize == 0; }
const int cc(){return 10;}
```
# 6、类
```c++
// *****在头文件定义类
// ---Box.h文件：【头文件定义类的变量，修饰符（公私有）、函数名等】
class Box {
public:
	// 这个Box就是该类的构造函数（名称与类名一致）每次调用类时会执行
	Box(double lengthValue, double widthValue, double heightValue);
	// 多个构造函数时，参数一定不能相同
	Box();
	double volume();
Box* setWidth(double wv);
// *****析构函数【创建类对象的块末尾会释放对象】释放对象时会执行此函数；
~Box();
/* 重载运算符：允许把+-等标准运算符应用于类对象（由关键字operator和一个运算符组成）
* 让自定义的类型，更像基本数据类型，通过运算符重载编写函数成员，可以让基本运算符操作类对象
* */
bool operator<(Box& aBox);
};

// ---Box.cpp文件：【cpp文件引入，这里就负责函数的具体内容，当类比较庞大时便于维护】
#include <iostream>
#include "Box.h"
// ::号引用头文件定义的函数
Box::Box(double lengthValue, double widthValue, double heightValue) {
	std::cout << "first counstruct";
}
Box::Box() { std::cout << "second construct"; }
//【前面都要加Box::表示属于该类】
double Box::volume() { return length * width * height; }
// this表示包含当前作用域的地址；返回this可实现链式调用；
Box* setWidth(double wv){return this;};
Box::~Box() { --objectCount; };
bool Box::operator<(Box& aBox) {
	return volume() < aBox.volume();
}
// 运算符重载（让类更像一个平常的数据类型，可以让基本运算符操作类对象）
// *****使用类
// ---main.cpp文件
#include "resource/Box.cpp"
int main(){
    //【创建一个Box类】（依照传入的参数值来决定选择哪个构造函数运行）
    Box firstBox {8.0,5.0,4.0};
    Box secondBox {5.0,8.9,2.4};
    // 使用firstBox的方法
    firstBox.volume();
    // 使用重载运算符【直接用定义了的符号比较即可】
    if(firstBox < secondBox){std::cout << "small";}

    return 0;
}
```
# 7、文件IO

```c++
#include <iostream>
#include <fstream>
#include <sstream>

int main(){
    // 定义文件名，文件存在的话会打开该文件，不存在则创建该文件
    std::string filename{ "f:\\primes.txt" };
    /********第二个参数是打开模式********
    - ios::out (打开文件，写入)
    - ios::in (打开文件，读取)
    - ios::trunc (把已有文件的长度变为0)
    - ios::app (在文件末尾进行写入)
    - ios::binary (二进制模式)
    */
    std::ofstream outFile{ filename,std::ios::out|std::ios::app };
    /******第二种写法*******
    std::ofstream outFile;
    outFile.open(filename,std::ios::out|std::ios::app);
    ********/
    // 向文件写入数据 std::setw()是设置写入宽度【这里hello为5个字符，会左侧设置5个空格字符对其到10】
    outFile << std::setw(10) << "hello" << endl;
    // endl 为写入结束
    outFile.close();
    return 0;
}
/********读取文件逻辑*********/
int openMyFile() {
    std::string filename{ "f:\\primes.txt" };
    std::ifstream inFile{ filename };
    /******第二种写法*******
    std::ifstream inFile;
    inFile.open(filename);
    ******/
    // 检测文件是否正确读取
    if(!inFile){
        std::cout << filename+"读取失败";
        return 1;
    }
    string aprime;
    while (true) {
        // 将读取的内容赋值给aprime,每次读取1行
        inFile >> aprime;
        if (inFile.eof()) break;
        std::cout << std::setw(10) << aprime;
    }
    return 0;
}
```
# 8、命名空间

使用namespace，划分命名空间
```c++
using namespace std;
// 第一个命名空间
namespace first_space{
   void func(){
      cout << "Inside first_space" << endl;
   }
}
// 第二个命名空间
namespace second_space{
   void func(){
      cout << "Inside second_space" << endl;
   }
}
// 使用
int main (){
   // 调用第一个命名空间中的函数
   first_space::func();
   // 调用第二个命名空间中的函数
   second_space::func(); 
   return 0;
}
```
using namespace 指令，指定使用哪个空间
```c++
// 直接指定下方代码使用的空间
using namespace first_space;
int main ()
{
   // 调用第一个命名空间中的函数
   func();
   return 0;
}
```
# 9、多线程

```c++
#include <iostream>
// 必须的头文件
#include <pthread.h>
 
using namespace std;
#define NUM_THREADS 5
 
// 线程的运行函数
void* say_hello(void* args)
{
    cout << "Hello Runoob！" << endl;
    return 0;
}
 
int main()
{
    // 定义线程的 id 变量，多个变量使用数组
    pthread_t tids[NUM_THREADS];
    for(int i = 0; i < NUM_THREADS; ++i)
    {
        //参数依次是：创建的线程id，线程参数，调用的函数，传入的函数参数
        int ret = pthread_create(&tids[i], NULL, say_hello, NULL);
        if (ret != 0)
        {
           cout << "pthread_create error: error_code=" << ret << endl;
        }
    }
    //等各个线程退出后，进程才结束，否则进程强制结束了，线程可能还没反应过来；
    pthread_exit(NULL);
}
```

# 10、gui编程

[win上QT库的安装](https://blog.csdn.net/weixin_47734949/article/details/124389243)

# 20、坑点
- 报错“常量中的字符太多”：`std::cout << 'hello world';`改为`std::cout << "hello world";`(单引号改为双引号)