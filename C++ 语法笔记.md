# C++ 语法笔记

1 使用泛型定义函数模板：

```c++
template <typename T> // 或者 template <class T> 也行

inline T const& Max (T const& a, T const& b) 
{ 
    return a < b ? b:a; 
} 
```

2 使用泛型类模板

```c++
template <class T>
void Stack<T>::push (T const& elem) 
{ 
    // 追加传入元素的副本
    elems.push_back(elem);    
} 
```



3 #pragma error

4 extern "C"

5 __inline

6 C++ 结构体的构造函数和析构函数

> 在C++中除了类中可以有构造函数和析构函数外，结构体中也可以包含构造函数和析构函数，这是因为结构体和类基本雷同，唯一区别是，类中成员变量默认为私有，而结构体中则为公有。注意，C++中的结构体是可以有析构函数和构造函数，而C则不允许。至于联合体，它是不可能有析构函数和构造函数的。本质上，它是一种内存覆盖技术的体现，也就是说，同一块内存在不同的时刻存储不同的值（可能是不同类型的）。
> 

```c++
 struct NOTIFY_DATA
{
	DWORD param1;
	DWORD param2;

	NOTIFY_DATA()
		:param1(NULL)
		,param2(NULL)
	{};

};
```

注意构造函数中如需要初始化成员变量，则需要加 '` : `' 和初始化参数列表。初始化参数列表的执行顺序和成员变量的定义顺序有关。

7 reinterpret_cast:

C++里的强制类型转换符。