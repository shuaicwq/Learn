# 1.C++变量

​	数据类型区别：占据内存的大小

​	int	2^31~ -2^31(符号位占据1位)

​	unsigned int     0~2^32(无符号位)

​	flood   value  =  5.5f;(无f实际是double类型)

​        double vaule = 5.5;

​	bool  = ture /fasle (0/1)	位图

​	sizeof(求字节)

​	

#  2.C++函数

​	

```
#include<iostream>

int Multiply(int a,int b) {
	return a * b;
}

int main() {


	int variable = Multiply(5,8);

	std::cout <<variable << std::endl;

	int variable1 = Multiply(3, 8);

	std::cout << variable1<< std::endl;

	int variable2 = Multiply(4, 8);

	std::cout << variable2 << std::endl;

	std::cin.get();
}


```

 引入函数

```
#include<iostream>

int Multiply(int a,int b) {
	return a * b;
}

void MultiplyAndLog(int a, int b) {
	int variable = Multiply(a,b);

	std::cout << variable << std::endl;
}
int main() {

	MultiplyAndLog(5, 8);
	MultiplyAndLog(3, 8);
	MultiplyAndLog(4, 8);
	std::cin.get();
}

```

函数：防止代码重复     //不易多，压慢速度

# 3.C++头文件

​	#include   -----粘贴复制

​	#program once    ------一个翻译单元

```
#include<iostream>

#include"Log.h"  //无#program once ，重复定义    //多重嵌套出错，重复定义
#include"Log.h"
int main() {


}

严重性	代码	说明	项目	文件	行	禁止显示状态	详细信息
错误	C2011	“Hello”:“struct”类型重定义	C++	D:\C++\C++\Log.h	8		

```

另一种方法——头文件保护符

```
#ifdef _LOG_H

#define _LOG_H

void Log(const char* message);
void InitLog()
{
	Log("initlog log");
}

struct Hello {  };

#endif
```

<相对路径，会搜索>                      “  相同文件目录  ”

- `<>`用于包含系统头文件或标准库头文件，编译器会在系统默认的包含路径中查找。
- `""`用于包含用户自定义的头文件，编译器会先在当前源文件所在目录查找，若找不到，再到系统默认路径查找。

# 4.调试代码

​	**计算机永远是对的**

​        （难）再学习

<img src="C:\Users\34776\AppData\Roaming\Typora\typora-user-images\image-20250115145143408.png" alt="image-20250115145143408" style="zoom:33%;" />

# 5.条件语句

​	

```
00007FF75BFD0F9C  mov         dword ptr [x],6  
	bool comparisonResult = x == 5;

```

```
	int x = 6;
00007FF6273623CC  mov         dword ptr [x],6  
	bool comparisonResult = x == 5;
00007FF6273623D3  cmp         dword ptr [x],5  
00007FF6273623D7  jne         main+35h (07FF6273623E5h)  
00007FF6273623D9  mov         dword ptr [rbp+0F4h],1  
00007FF6273623E3  jmp         main+3Fh (07FF6273623EFh)  
00007FF6273623E5  mov         dword ptr [rbp+0F4h],0  
00007FF6273623EF  movzx       eax,byte ptr [rbp+0F4h]  
00007FF6273623F6  mov         byte ptr [comparisonResult],al  
	if (comparisonResult) {
00007FF6273623F9  movzx       eax,byte ptr [comparisonResult]  
00007FF6273623FD  test        eax,eax  
00007FF6273623FF  je          main+5Eh (07FF62736240Eh)  
		Log("Comparison was true");
00007FF627362401  lea         rcx,[string "Comparison was true" (07FF62736AC28h)]  
00007FF627362408  call        Log (07FF62736135Ch)  
00007FF62736240D  nop  
	}
	std::cin.get();
00007FF62736240E  mov         rcx,qword ptr [__imp_std::cin (07FF627371190h)]  
00007FF627362415  call        qword ptr [__imp_std::basic_istream<char,std::char_traits<char> >::get (07FF627371150h)]  
00007FF62736241B  nop  
}
```

else if

```
#include<iostream>
#include "Log.h"	

int main() {
	int x = 5;
	bool comparisonResult = x == 5;
	if (comparisonResult) {
		Log("Comparison was true");
	}
	else {
		if(x>5)
			Log("Comparison was false");
		else
			Log("Comparison was false");
	}‘、
	std::cin.get();
}
```

```
#include<iostream>
#include "Log.h"	

int main() {
	int x = 5;
	bool comparisonResult = x == 5;
	if (comparisonResult) 
		Log("Comparison was true");
	else if(x>5)
		Log("Comparison was false");
	else
		Log("Comparison was false");
	std::cin.get();
}
```

# 6.Visual Studio 2022设置

​	![image-20250115160104620](C:\Users\34776\AppData\Roaming\Typora\typora-user-images\image-20250115160104620.png)

1.过滤文件夹，是不存在与磁盘

2.显示所有文件----src

3.设置输出目录，项目文件更加简洁明了

![image-20250115162513110](C:\Users\34776\AppData\Roaming\Typora\typora-user-images\image-20250115162513110.png)

![image-20250115162537684](C:\Users\34776\AppData\Roaming\Typora\typora-user-images\image-20250115162537684.png)

# 7.循环

​	

```
#include<iostream>
int main()
{
	int i = 0;
	bool condition = true;

	for (; condition;)
	{
		std::cout << "Hello World!" << std::endl;
		i++;
		if (i == 5)
		{
			condition = false;
		}

	}
}
```

```
	int i = 0;
	while (i) {
		std::cout << "Hello World!" << std::endl;
		i++;
		if (i == 5)
		{
			break;
		}

		do {
			std::cout << "Hello World!" << std::endl;
		}
		while (condition);

```



# 8.C++控制语句

​	**break	continue 	return**

# 9.C++指针

​	**指针：存储内存地址的整数**



```
#include<iostream>
int main()
{
	int var = 8;
	int* ptr = &var;
	std::cin.get();
}
```

* 指针 ：取指针的值    &指针：取指针的地址

```
#include<iostream>
int main()
{
	char* bhffer = new char[10];
	memset(bhffer, 0, 10);
	std::cin.get();

}
```



```
0x000002591A7D5FA8  dd dd dd dd dd dd dd dd dd dd dd dd dd dd dd dd 29 04 b5 35 dd 05 00 80 dd dd dd dd dd dd dd dd dd dd dd dd dd dd dd dd dd dd dd dd dd dd dd dd dd dd dd dd dd dd dd dd 
```



```
#include<iostream>
int main()
{
	char* bhffer = new char[10];
	memset(bhffer, 0, 10);
	char** ptr = &bhffer;
	delete[] bhffer;
	std::cin.get();

}
```

# 10.C++的引用

​	int&------引用

```
#include<iostream>
int main()
{
	int a = 10;
	int& ref = a;
	ref = 2;
	std::cout << a << std::endl;

}

a=2
```

  形参  实参

```
#include<iostream>


void swap(int vlaue) {
		vlaue++;
}

int main(){
	int a = 10;
	swap(a);
	std::cout << a << std::endl;

}
```

```
//指针
void swap(int *vlaue) {
		(*vlaue)++;
}

int main(){
	int a = 10;
	swap(&a);
	std::cout << a << std::endl;

}
//引用
void swap(int& vlaue) {
		vlaue++;
}

int main(){
	int a = 10;
	swap(a);
	std::cout << a << std::endl;

}
```

```
int main(){
	int a = 10;
	int b = 20;
	int* ref = &a;
	*ref = 30;
	ref = &b;
	*ref = 40;
	std::cout << a << std::endl;
	std::cout << b << std::endl;
}
```

# 11.C++的类

​	**类：数据+功能**

```
class Player {
public:
	int x, y;
	int speed;
	void Move(int xa, int ya) {
		x += xa * speed;
		y += ya * speed;
	}
};

int main() {

	Player player;
	player.x = 5;
	player.y = 5;
	player.speed = 2;
	player.Move(1, 2);

	LOG(player.x);
	LOG(player.y);

	std::cin.get();
}
```

# 12.C++的类与结构体的对比

​	**类默认是私有的private	结构体默认情况下是共有的**

​	类处理很多东西			结构体只针对变量（类似数据库）

# 13.如何写一个C++的类

​	根据需求写类，先填写需要的东西，再回头填空补全类的功能

```
class Log {
public:
	const int LogLevelError = 0;
	const int LogLevelWarn = 1;
	const int LogLevelInfo = 2;
private:
	int Level=LogLevelInfo;

public:
	void Setlevel(int level) {
		Level = level;
	}
	void error(const char* message) {
		if (Level >= LogLevelError)
			std::cout << "[ERROR]: " << message << std::endl;
	}
	void warn(const char* message) {
		if (Level >= LogLevelWarn)
			std::cout << "[WARN]: " << message << std::endl;
	}
	void info(const char* message) {
		if (Level >= LogLevelInfo)
			std::cout << "[INFO]: " << message << std::endl;
	}
};

int main() {
	Log log;
	log.Setlevel(log.LogLevelInfo);
	log.error("Hello!");
	log.warn("Hello!");
	log.info("Hello!");
	std::cin.get();
}
```

# 14.C++中的静态（static）

​	**static只在一个翻译单元起作用**	（extern  linking）

​	全局变量不建议用

