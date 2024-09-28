---
title: C
date: 2022-11-23
category: Code
---
<!--more-->



# C++
## C
- {}中定义变量只在{}中存在


## 1. 面对对象
1. Object = Entity  对象等于实例，在程序语言中就是变量
2. Class（类）定义了 Object（对象）的属性，对象是一个类的实例

## 2. 头文件
- ::区域解析符
- .h 头文件，声明类
- .cpp 
- declarations 声明  extern、函数的原型、类、结构都是声明
- definitions 定义  变量的称为定义，
- \#include 编译预处理，直接将要导入的类文本插入到目标文件中
    - \#include "xx.h" 在当前目录中寻找
    - \#include <xx.h> 在系统目录中寻找
    - \#include <xx> 与 \#include <xx.h> 一致
- .h文件中只声明不定义，是为了避免重复定义
  - 标准头文件结构
  - \#ifndef HEADER_FLAG
  - \#define HEADER_FLAG
  - \#endif 
  - 一个头文件中只放一个类的声明，对应的源代码文件用相同的前缀，后缀cpp
  - 只能include .h文件，不能是 .cpp 文件

## 3. 成员变量
- 成员变量（field），参数（parameter），本地变量（local variables）
- 在.h中的成员变量并不真实存在，只是进行了声明
- 类是抽象的不存在实体，成员变量（属性）属于对象不是属于类的，函数（方法）是属于类的不属于对象
- 类的函数只存在于一个，不同的对象调用的是同一个函数，调用的时候相当于把对象的地址传入到函数当中
- 不同的对象调用一个函数时，该函数知道是哪一个对象在调用自己，实际上是通过隐藏变量 this 指向当前的对象，this->i

## 4. 构造和析构
- 构造函数
  - 函数名字和类的名字相同
  - ```c++
    class Tree{
        int height;
    public:
        Tree(int initialHeight)l;
        ~Tree();
        void grow(int years);
        void printsize( )
    }
    Tree::Tree(int initialHeight){
        height = initialHeight
    }
    Tree t(12)
    ```
  - 没有参数的构造函数称为 default constructor
  - ```c++
    struct Y {
        float f;
        int i;
        Y(int a);
    }
    Y y1[] = {Y(1), Y(2), Y(3)} //可以
    Y y2[2] = {Y(1)}; // 错误，缺失构造函数的参数
    ```

## 5. 动态内存
- 之前都是本地变量，还可以动态申请内存
- new，delete 

### 1.for 循环内定义的变量的生命周期
for中定义的变量，编译器编译后，是存放在栈空间上的一个临时内存地址
每单次循环结束程序都会跳出循环体的作用域，循环体内的局部变量都被释放；下一次循环重新进入循环体，里边的每个局部变量和对象都重新构造。

每次定义的 n，其 生命周期只有一次循环的时间（比如 i=0的那次循环过后，Listnode的内存空间就被回收了，也就不妨碍 i=1时对Listnode的定义了）
```c++
for (int i= 0; i < 5; i++) {
   Listnode n;
  }
```

### 2.内存的四种分区
- 栈区（stack）：编译器自动分配和释放的，主要存储的是函数的参数值，局部变量等值。发生函数调用时就为函数运行时用到的数据分配内存，函数调用结束后就将之前分配的内存全部销毁。所以局部变量、参数只在当前函数中有效，不能传递到函数外部。栈内存的大小和编译器有关，编译器会为栈内存指定一个最大值，在 VC/VS 下，默认是 1M。
- 堆区（heap）：动态分配。一般由程序员分配和释放（动态内存申请malloc与释放free），需要手动free。否则会一直存在，若程序员不释放，程序结束时可能由操作系统回收。
- 全局区（静态区）（static）：静态分配。全局变量和静态变量的存储是放在一块的，该区域在程序结束后由操作系统释放。
- 代码区：通常用来存放程序执行代码（包含类成员函数和全局函数及其他函数代码），这部分区域的大小在程序运行前就已经确定，也有可能包含一些只读的常数变量，例如字符串变量。

### new的作用
在实际的编程中，实际要处理的数据数量在编程时无法确定，所需的内存空间大小无法确定时，除了定义“尽可能大的空间”的方法，还有就是动态内存分配。此种内存分配是在程序运行中进行的，而不是在编译时就确定的，因此称为“动态内存分配”。

在 C++ 中，通过 new 运算符来实现动态内存分配。
new开辟的空间在堆上。
当在局部函数中new出一段新的空间，该段空间在局部函数调用结束后仍然能够使用，可以用来向主函数传递参数。
new的使用格式，new出来的是一段空间的首地址。所以一般需要用指针来存放这段地址。


## 6. 访问限制
- public
- private 类的所有成员函数可以访问，直接使用变量名例如x即可访问。私有是对类来说的，而不是对象，同一个类的对象之间可以互相访问私有的成员变量。
    ```c++
    class A{
    private:
            int i;
            int *p;
    public:
            A(){p=0}
            ~A()(if (p) delete p;)
            void set(int ii){i = ii;}
            void f(){p = new int;}
            void g(A* q){cout << q->i <<endl;}
    };
    int main(){
        A* p = new A[10];
        for (int i=0; i <10; i++)
            p[i].set(i);
        A b;
        b.set(100);
        p[0].g(&b);
        delete[] p
    }
  ```
- protected

## 7. 初始化列表
- 除了在构造函数中初始化成员变量，还可以用初始化列表（initialization list）
    ```c++
    class A{
    private:
            int i;
            int *p;
    public:
            A(){p=0}
    };
    ```

    ```c++
    class A{
    public:
            A():p(0)
    };
    ```
- 初始化列表是早于构造函数的，构造函数的初始化相当于先初始化得到成员变量p再赋值
    ```c++
    class Point{
    private:
        const float x, y;
        Point(float xa = 0.0, float ya = 0.0)
            : y(ya), x(xa) {}
    }
    ```

## 8. 继承（inheritance）

- 继承可以共享父类的成员变量和函数和接口（interface）
- 父类（parent class），子类（child class）
    ```c++
    class A {
    public:
        A():i(0) {}
    private:
        int i;
    }
    class B: public A{}    
    ```
- 子类无法访问父类的private，但可以访问protected

## 9. 函数重载
- 默认参数 int harpo(int n, int m = 4, int j = 5); 
- 默认参数写在.h里的，.cpp里不能写