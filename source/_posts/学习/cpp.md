---
title: C++学习记录
tags: [学习, C++]
categories: [学习]
---
# 输入输出

## cin函数

一、
正常情况下，cin遇到空格结束读取，写个小例子：
举例：

```cpp
int main()
{
    string a;
    cin>>a;
    cout<<a<<endl;
}
```

二、cin.get()

该函数有三种格式：无参，一参数，二参数
即cin.get(), cin.get(char ch), cin.get(array_name, Arsize)读取字符的情况：
输入结束条件：Enter键
对结束符处理：**不丢弃缓冲区中的Enter**
cin.get() 与 cin.get(char ch)用于读取字符，他们的使用是相似的，
即：ch=cin.get() 与 cin.get(ch)是等价的。
举例：

```cpp
#include <iostream>
#include <string.h>
using namespace std;
int main()
{
       char c1, c2;
       cin.get(c1);
       cin.get(c2);
       cout<<c1<<" "<<c2<<endl;             // 打印两个字符
       cout<<(int)c1<<" "<<(int)c2<<endl;   // 打印这两个字符的ASCII值
       return 0;
}
 
```


读取字符串的情况：
cin.get(array_name, Arsize)是用来读取字符串的，
可以接受空格字符，遇到Enter结束输入，按照长度(Arsize)读取字符, 会丢弃最后的Enter字符,但是enter算一个字符 。
举例：

```cpp
#include <iostream>
#include <string.h>
using namespace std;
int main ()
{
    char a[20];
    cin.get(a, 10);
    cout<<a<<endl;
    return 0;
}
```

 


三、cin.getline()
举例：//两个参数


```cpp
#include <iostream>
using namespace std;
 
int main(){
    char ch[10];
    cin.getline(ch,5);
    cout<<ch<<endl;
    //和cin.gets()原理和工作是一样的
}
```



```cpp
//三个参数
#include <iostream>
using namespace std;
 
 
 
int main(void){
    char ch[10];
    cin.getline(ch,8,'e');
    cout<<ch<<endl;
    //遇到'e'读取结束
    return 0;
}
```


 

```cobol
//二维数组
#include <iostream>
#include <string.h>
using namespace std;
      
int main(void){
    char ch[5][10];
    for(int i=0;i<5;i++){
        cin.getline(ch[i],10);
    }
    cout<<"the result: "<<endl;
	for(int j=0;j<5;j++){
        cout<<ch[j]<<endl;
    }
}
```

解析：cin.getline() 与 cin.get(array_name, Arsize)的读取方式差不多，以Enter结束，可以接受空格字符。按照长度(Arsize)读取字符, 会丢弃最后的Enter字符。
但是这两个函数是有区别的：
cin.get(array_name, Arsize)当输入的字符串超长时，不会引起cin函数的错误，后面的cin操作会继续执行，
只是直接从缓冲区中取数据。但是cin.getline()当输入超长时，会引起cin函数的错误，后面的cin操作将不再执行。

四、getline()
举例：

```cpp
#include <iostream>
#include <string.h>
using namespace std;

int main(){
    string str；
    getline(cin,str);
    cout<<str<<endl;
    return 0;
}
```

注意：cin.getline()和getline()类似，但是cin.getline()属于istream流，而getline()属于string流

## cin.get()和cin.getline()的区别

cin.get和cin.getline都是C++中用于从输入流中读取数据的函数，但它们之间存在一些重要的区别。

1. 读取方式：cin.get()函数每次读取一个字符，而cin.getline()函数每次读取一行。
2. 换行符处理：cin.get()函数会将由Enter键生成的换行符留在输入队列中，而cin.getline()函数则会丢弃由Enter键生成的换行符。
3. 读取长度：cin.get()函数没有指定读取长度的参数，因此无法控制读取的字符数。而cin.getline()函数可以指定要读取的最大字符数。
4. 缓冲区：cin.get()函数不会自动添加空字符，也不会设置失效位。而cin.getline()函数会自动添加空字符，并且在输入的字符长度大于数组长度时，会设置失效位。

总的来说，cin.get()和cin.getline()都是C++中用于从输入流中读取数据的函数，但它们在读取方式、换行符处理、读取长度和缓冲区等方面存在一些区别。根据实际需求选择合适的函数进行数据读取。





# 面向对象编程

## 类和对象的创建与使用

在定义一个类的时候，要定义公共部分和私有部分。公共部分一般多为函数，私有部分一般多为类的对象。

```cpp
#define _CRT_SECURE_NO_WARNINGS
#include <iostream>
using namespace std;

/********* Begin *********/
//在此处实现一个汽车类
class Car
{
    public:
        void opencdoor(){cdoor = 1;}
        void closecdoor(){cdoor = 0;}
        void openclamp(){clamp = 1;}
        void closeclamp(){clamp = 0;}
        void sspeed(){cspeed += 10;}
        void lspeed(){cspeed -= 10;}
        void initcspeed(){cspeed = 0;}
        void show();
    private:
        int cdoor;
        int clamp;
        int cspeed;
};
/********* End *********/
 
void Car::show()
{
    if (cdoor == 1)
        cout << "车门 ON" << endl;
    else
        cout << "车门 OFF" << endl;
    if (clamp == 1)
        cout << "车灯 ON" << endl;
    else
        cout << "车灯 OFF" << endl;
    cout << "速度 " << cspeed << endl;
}

int main()
{
    /********* Begin *********/
    //在此处解析执行输出汽车的整体状态
    char cmds[25];
    cin >> cmds;
    Car a;
    int i = 0, m;
    a.initcspeed();
    while (cmds[i] != '\0')
    {
        m = cmds[i] - '0';
        switch (m)
        {
        case 1:
            a.opencdoor();break;
        case 2:
            a.closecdoor(); break;
        case 3:
            a.openclamp(); break;
        case 4:
            a.closeclamp(); break;
        case 5:
            a.sspeed(); break;
        case 6:
            a.lspeed(); break;
        }
        i++;
    }
    a.show();
    return 0;
    /********* End *********/
}
```

在类里面定义的函数，如果要写函数的内容，尽量简短一些，不要出现循环、判断等内容。

一般来说，定义的函数要访问私有变量的对象时，而且函数内容可能较为复杂的话，最好是在类里面声明，类外面撰写函数的内容。

但是在类的外面写函数的内容的时候，在函数头必须加上这个函数属于的类，不然无法访问类内部的私有变量。



## 构造函数、析构函数

构造函数、析构函数与赋值函数是每个类最基本的函数。他们太普通以致让人容易麻痹大意，其实这些貌似简单的函数在使用时要特别注意以免造成不必要资源浪费和产生意想不到的错误。

每个类只有一个析构函数和一个赋值函数，但是可以有多个构造函数（包含一个拷贝构造函数，其他的成为普通构造函数）。

下面我们就一起来学习构造函数和析构函数的基本使用。

### 构造函数

所谓构造函数，就是在对象构造的时候调用的函数。构造函数是一种特殊的成员函数，它主要用于为对象分配空间，进行初始化。

构造函数在定义类对象时自动调用，不需用户调用，也不能被用户调用。在对象使用前调用。如果类中没有定义构造函数，系统则会自动给出一个无参构造函数。

构造函数**没有返回值**，函数名必须与**类名一致**，一个类可以有多个构造函数，但是参数必须有差别（也就是所谓的**重载**）。

例如：

```cpp
class Test
{
    public:
        Test();     // 无参数的构造函数
        Test(int a);     // 有一个 int 参数的构造函数
    private:
        Test(int a,int b);     // 私有的两个参数的构造函数
};
Test::Test()
{ /* 此处省略一些初始化的工作 */}
Test::Test(int a)
{ /* …… */}
Test::Test(int a,int b)
{ /* …… */}
```

构造函数也会受**访问性**影响，在不同的作用范围，能调用的构造函数也会不同。

### 初始化成员

构造函数的一个重要任务就是给成员初始化，初始化成员有两种办法，一种是手动给成员赋值，另一种是使用**初始化列表**。这里介绍第二种，格式为：

```cpp
类名::构造函数名(参数表): (成员初始化表){ 构造函数体 }
```

构造函数中的初始化列表只需要在参数列表的后面加一个**冒号**（`:`），然后将要初始化的成员按照`成员名(参数)`的格式排列在后面，个成员之间用逗号隔开。

例如：

```cpp
class Test
{
public:
    int A;
    int B;
    Test(int a);
};
Test::Test(int a)
    :A(a),B(10)     //给成员变量 A、B 初始化，不一定要和参数列表写在一行
{ /* …… */ }
```

其中成员的初始化顺序不是按照初始化列表中的顺序来的，而是按照成员声明的顺序来的，例如：

```cpp
/* Test类的声明同上 */

Test::Test(int a)
    :B(10),A(a)     // 虽然 B 在前面，但还是 A 先初始化
{/* …… */}

Test::Test(int a)
    :B(a),A(B)     //此处 A 的初始化依赖了 B，然而是 A 先初始化，这就导致 A 得到了 B 中还没初始化的错误内容
{/* …… */}
```

### 析构函数

析构函数是一种特殊的成员函数，它会在每次删除所创建的对象时执行。它执行与构造函数相反的操作，通常用于撤消对象时的一些清理任务，有助于在跳出程序（比如关闭文件、释放内存等）前释放资源。

析构函数的名称与类的名称是完全相同的，只是在前面加了个波浪号（~）作为前缀，它不会返回任何值，也不能带有任何参数。格式如下：

```cpp
类名::~析构函数名(){}
```



# 内联函数

如果在类的外面定义的函数，内容不是太大的时候（可以写在类的里面的时候），可以使用内联函数

```cpp
class Car
{
    public:
        void show();
    private:
        int cdoor;
        int clamp;
        int cspeed;
};
inline void Car::show()   //内联函数
{
    cout<<...;
}
```

# 友元函数

友元函数
在C++编程语言中，友元函数（Friend Function）是一种特殊的函数，**具有访问类中私有成员的权限**，尽管它不是类的成员函数。友元函数的存在使得类的设计更加灵活，能够在需要时授予外部函数访问类的私有成员的能力。本文将详细介绍C++中的友元函数，包括其定义、使用场景、优缺点以及示例。

一、定义
友元函数是在一个类中声明的一个非成员函数，但在类的内部声明该函数为友元。这意味着该函数可以访问该类的私有成员，包括私有变量和私有函数。友元函数的声明通常位于类的声明中，但**其实现则位于类外部**。

1、友元函数：通过friend+普通函数
友元函数是在一个类中声明的非成员函数，但在类的内部声明该函数为友元。这使得该函数可以访问该类的私有成员。

语法：

```cpp
 friend void friendFunction(const MyClass& obj);
```

1
案例：

```cpp
#include <iostream>
using namespace std;
class MyClass {
   private:
    int privateData;

   public:
    MyClass(int data) : privateData(data) {}

    // 声明友元函数
    friend void friendFunction(const MyClass& obj);

    // Getter函数
    int getPrivateData() const { return privateData; }
};

// 友元函数实现
void friendFunction(const MyClass& obj) {
    cout << "Friend function accessing private data: " << obj.privateData
         << endl;
}

int main() {
    MyClass myObj(42);
    friendFunction(myObj);  // 调用友元函数
    cout << "Private data accessed via getter: " << myObj.getPrivateData()
         << endl;

    return 0;
}

```

如果需要将普通函数声明为某个类的友元函数，只需要在该类中进行友元声明即可，不管public或private中进行声明都可以。

2、友元类： 通过friend+类
友元类是一个类，在另一个类中声明为友元。这意味着被声明为友元的类可以访问另一个类的私有成员，类似于友元函数的概念，但是是对整个类的授权。友元类通常用于需要多个类之间紧密协作的情况，允许这些类访问彼此的私有成员。

语法：

```cpp
 friend class FriendClass;
```

1
案例：

```cpp
#include <iostream>
using namespace std;
class MyClass;

class FriendClass {
   public:
    void accessPrivateData(const MyClass& obj);
};

class MyClass {
   private:
    int privateData;

   public:
    MyClass(int data) : privateData(data) {}

    // 声明友元类
    friend class FriendClass;

    int getPrivateData() const { return privateData; }
};

// 友元类成员函数实现
void FriendClass::accessPrivateData(const MyClass& obj) {
    cout << "Friend class accessing private data: " << obj.privateData << endl;
}

int main() {
    MyClass myObj(42);

    FriendClass friendObj;
    friendObj.accessPrivateData(myObj);  // 调用友元类的成员函数

    return 0;
}
```

# 继承和派生

## 共有继承
- 共有继承，派生类的对象仅可以访问派生类的公有成员
- 派生类的成员函数可以访问从基类继承过来的的公有成员和保护成员（也就是继承后的派生类的共有成员）和派生类的私有成员
- 但是不好访问基类的私有成员

## 私有继承
私有继承，派生类的对象仅可以访问派生类的公有成员

## 保护继承
保护继承，派生类的对象仅可以访问派生类的公有成员，不能直接访问基类的任何成员

- 其和私有继承的区别在于：
  - 1.私有继承是类似于买断性质，仅可以使用一代，派生类的派生类（第三代）就无法继承到基类（第一代)的成员
  - 2.保护继承，因为派生类的成员可以访问基类的公有和保护成员，所以第三代是可以继承到基类的成员

## 类型兼容规则

**类型兼容规则**是指在需要基类对象的任何地方，都可以使用公有派生类的对象来替代。通过公有继承，派生类得到了基类中除**构造函数、[析构函数](https://so.csdn.net/so/search?q=析构函数&spm=1001.2101.3001.7020)**之外的所有成员。这样，公有派生类实际就具备了基类的所有功能，***凡是基类能解决的问题，公有派生类都可以解决***。类型兼容规则所指的替代包括以下情况：

- 1.子类对象可以当作父类对象使用
- 2.子类对象可以直接赋值给父类对象
- 3.子类对象可以直接初始化父类对象
- 4.父类指针可以直接指向子类对象
- 5.父类引用可以直接引用子类对象
类型兼容规则，通过基类对象名、指针只能使用从基类继承的成员
