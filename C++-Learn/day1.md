

# 1.visual assist

# 2.helloworld

```
#include<iostream>   //预处理

int main() {
	std::cout << "Hello World!" << std::endl;
	std::cin.get();
	return 0;
}
```

# 3.C++如何工作：

​	<<   重定向函数

1. **预处理**：源文件、预处理指令、头文件插入、宏替换、预处理后文件
2. **编译**：源文件（经预处理）、词法分析、语法分析、语义分析、汇编代码、生成汇编文件
3. **汇编**：汇编文件、汇编代码、转换机器码、目标文件
4. **链接**：目标文件、解决符号引用、合并目标文件、可执行程序

# 4.声明

```
#include<iostream>

void Log(const char* message);

int main() {
	Log("hellworld");
	std::cin.get();
}
```

链接--知道log函数的地方-连接函数（不知道地方）

每次.c——每次.obj——链接一起.exe

# 5..cpp——翻译单元——.obj

# 6.预处理

预编译只是把头文件内容黏贴到你写的文本中

```
#include<iostream>


void Log(const char* message);

int main() {
	Log("hellworld");
	std::cin.get();
#include"Eenbrush.h"
```

```
"Eenbrush.h"
}
```

```
#if 1

int Multiply(int a, int b) {
	int  result = a * b;
	return result;
}
#endif 


#line 1 "D:\\C++\\C++\\Multiply.cpp"




int Multiply(int a, int b) {
	int  result = a * b;
	return result;
}
#line 10 "D:\\C++\\C++\\Multiply.cpp"

```

```
#if 0

int Multiply(int a, int b) {
	int  result = a * b;
	return result;
}
#endif 

#line 1 "D:\\C++\\C++\\Multiply.cpp"








#line 10 "D:\\C++\\C++\\Multiply.cpp"

```

加了#inlcude<iostream>    ++源码预编译很长

编译出*.asm文件查看汇编指令

优化-----根据汇编执行速度优化代码------属性优化点

```
_TEXT	SEGMENT
a$ = 48
b$ = 56
?Multiply@@YAHHH@Z PROC					; Multiply, COMDAT
; File D:\C++\C++\Multiply.cpp
; Line 2
$LN4:
	mov	QWORD PTR [rsp+8], rbx
	push	rdi
	sub	rsp, 32					; 00000020H
	mov	edi, ecx
	mov	ebx, edx
	lea	rcx, OFFSET FLAT:__88E728D6_Multiply@cpp
	call	__CheckForDebuggerJustMyCode
	imul	edi, ebx
	mov	rbx, QWORD PTR [rsp+48]
	mov	eax, edi
; Line 5
	add	rsp, 32					; 00000020H
	pop	rdi
	ret	0
?Multiply@@YAHHH@Z ENDP					; Multiply
_TEXT	ENDS
END
```

# 7.链接

​	链接器

```
严重性	代码	说明	项目	文件	行	禁止显示状态	详细信息
错误	C4716	“Log”: 必须返回一个值	C++	D:\C++\C++\Multiply.cpp	7		

```

C---编译阶段

```
严重性	代码	说明	项目	文件	行	禁止显示状态	详细信息
错误	LNK2019	无法解析的外部符号 main，函数 "int __cdecl invoke_main(void)" (?invoke_main@@YAHXZ) 中引用了该符号	C++	D:\C++\C++\MSVCRTD.lib(exe_main.obj)	1		

```

L--链接阶段

<img src="D:\C++-Learn\image-20250114233748447.png" alt="image-20250114233748447" style="zoom: 50%;" />

入口点不一定是main,可以自己自定义入口点

链接错误

<img src="D:\C++-Learn\image-20250114234914630.png" alt="image-20250114234914630" style="zoom:50%;" />

重复定义函数



​    1.

```
#include<iostream>
#include"Log..h"

void Log(const char* message);


static int Multiply(int a, int b) {
	Log("Multiply");
	return a * b;
}
int main() {
	std::cout << Multiply(5, 8) << std::endl;
	std::cin.get();
}
```

```
#include<iostream>
void Log(const char* message) {
	std::cout << message << std::endl;
}

void InitLog()
{
	Log("initlog log");
}



static int Multiply(int a, int b) {
	Log("Multiply");
	return a * b;
}
int main() {
	std::cout << Multiply(5, 8) << std::endl;
	std::cin.get();
}
```

解决方法

```
static void InitLog()
{
	Log("initlog log");
}
```

```
inline void InitLog()
{
	Log("initlog log");
}
```

```
将定义转一到同一个翻译单元
Log.h

void Log(const char* message);

InitLog.h

#include<iostream>
#include"Log.h"

void InitLog()
{
	Log("initlog log");
}
void Log(const char* message) {
	std::cout << message << std::endl;
}

```

**链接器会带走所有的文件并将他们链接在一起**