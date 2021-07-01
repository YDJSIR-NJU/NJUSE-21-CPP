# 面向对象编程十大问题

## 当类中未自主定义构造函数，compiler会提供默认构造函数，为什么，编译器会提供一个空类吗？

编译器只有在一定**需要**默认构造函数的时候，才去创建构造函数。

## 何时构造函数、析构函数应被定义为private？何时应在其中使用友元、static成员？

1. private的构造函数和析构函数常常用在某些设计模式下的情况；
2. 使用方法：通过友元类对象的方法来完成创建、使用static方法完成创建；
3. 构造函数的私有化的类的设计保证了其他类不能从这个类派生或者创建类的实例(单件模式)；
4. <a href = "https://blog.csdn.net/vivian187/article/details/93043070">参考</a>

## 为什么要引入成员初始化表？为什么初始化表执行次序只与类数据成员的定义次序相关？

+ 初始化列表中初始化的顺序与声明的顺序一致，与自己的声明顺序无关
+ 原则上的初始化顺序:**就地初始化 > 构造函数的初始化列表 >构造函数里的赋值(严格意义上不能成为初始化)**
+ <a href = "https://blog.csdn.net/qq_38243831/article/details/97814248">参考</a>

```c++
class CString{
    char *p;
    int size;
    public:
        CString(int x):size(x),p(new char[size]) {}    
    };
```

## 为什么引入Copy构造函数、=操作符重载？

1. copy()拷贝函数:相同类型的类对象是通过拷贝构造函数来完成整个复制过程的，拷贝函数的拷贝过程没有处理静态数据成员，详见下

## 什么是延迟绑定? C++是如何实现虚函数的？

```c++
class Shape {
    public:
        virtual void draw() const = 0;
        virtual void error(const string& msg);
        int objectID() const;
};
```



## 我们该在何时使用`virtual` ？



## `public`继承和`non-public`继承的含义是？

### `public`继承方式

+ 基类中所有public成员在派生类中为public属性；
+ 基类中所有protected成员在派生类中为protected属性；
+ 基类中所有private成员在派生类中不可访问。

### `protected`继承方式

+ 基类中的所有public成员在派生类中为protected属性；
+ 基类中的所有protected成员在派生类中为protected属性；
+ 基类中的所有private成员在派生类中仍然不可访问。

### `private`继承方式

+ 基类中的所有public成员在派生类中均为private属性；
+ 基类中的所有protected成员在派生类中均为private属性；
+ 基类中的所有private成员在派生类中均不可访问。

> 参考<a href = "https://blog.csdn.net/baowxz/article/details/51282395">公有、非公用继承的区别</a>

## 为什么` =  ()  []  -> `不能作为全局函数重载?

+ 大体上来讲，C++一个类本身对这几个运算符就已经有了相应的解释了。
+ 如果将这四种符号进行友元全局重载，则会出现一些冲突
+ <a href = "https://blog.csdn.net/weixin_30781107/article/details/98147938">参考</a>

## 何时成员函数能返回& ？



## 在何时应以何种方式重载new、delete？

+ 不允许重载:`void* operator new(size_t, void*); // 不允许重新定义这个版本`
+ <a href = "https://blog.csdn.net/fengbingchun/article/details/78991749">C++中重载new和delete的使用</a>