# 1.C++类和结构体中的静态（static)

​	多个末影箱之间共享存储空间，无论在何处打开，内容都相同。

​	静态不接受非静态

```
struct MyStruct
{
	static int x, y;
	static void Print()
	{
		std::cout << x << ", " << y << std::endl;
	}
};
int MyStruct::x;
int MyStruct::y;
int main() {
	MyStruct::x = 2;
	MyStruct::y = 3;
	MyStruct::Print();
	std::cin.get();
}
```

# 2.C++中的局部变量（Local Static）

​	变量的生存期：内存中存活的时间

​	变量的作用域：访问变量的范围

```
#include<iostream>
void Function()
{
	static int x;
	x++;
	std::cout << x << std::endl;
};

int main() {
	Function();
	Function();
	Function();
	int x = 10;
	Function();
	Function();
}
//x=1 2 3 4 5 
```

​	单例实例：确保在整个程序运行过程中，某个类只有一个实例对象存在

​	有一个神奇的盒子，你第一次打开它，它会给你一个物品，之后你再打开它，它给你的还是之前的那个物品，不会给你新的。

```
#include<iostream>

class Singleton {
public:
    // Get 函数是获取单例实例的静态函数
    static Singleton& Get()
    {
        // 使用静态局部变量存储单例实例
        static Singleton instance;
        return instance;
    }
    // Hello 函数是单例类中的一个成员函数，这里暂时未实现具体功能
    void Hello(){ }
};

int main() {
    // 通过 Get 函数获取单例实例，并调用其 Hello 函数
    Singleton::Get().Hello();
}
```

