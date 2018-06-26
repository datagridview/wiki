---
title: "C++"
date: 2018-06-25 14:19
updated: 2018-06-25 14:19
log: "第一次编辑"
---

[TOC]

## C++基础

包含一些c++的基本概念和规则，与C语言的一部分需要注意的点结合叙述。

### 变量和基本类型

在C++中，变量的初始化和赋值是两个完全不同的操作。

#### 列表初始化
用花括号来初始化变量得到了全面应用，如下：

```C++
int unit = {0};
int unit = 0;
int unit{0};
int unit(0);
```

#### 默认初始化

对于内置类型变量：若在函数外部，则被初始化为0；在函数内部，将不被初始化，即未被定义，将引发错误。

#### 变量声明和定义的关系

声明：让变量为程序所知。

定义：为变量创建与名字相关的实体。

```C++
extern int i; //声明
int j; //定义并定义
extern int i = 3; //定义
```

#### 复合类型：引用和指针

引用：给对象其另外一个名字，且必须被初始化。与别名等同。

```
int ival = 1024;
int &refVal = ival; //refVal引用ival
int &refVal4 = 10; //错误：引用只能绑定在对象上
```

指针：指向另外一个类型的复合类型。
空指针三种方式：`int *p1=nullptr;``int *p2=0;``int *p3=NULL;`

依照修饰符和变量名在一起的原则定义变量。`int *p = 1;`

#### 定义常量

多个文件共享const对象：`extern const int a = 1;`

对常量的引用一定要是相同类型的引用对象。

```
const int a = 1;
const int &1 = a;
```
不过，对const的引用可能引用一个并非const的对象，如下

```
int i  = 43;
int &a = i;
const int &r2 = i;
r1 = 0;
r2 = 0; //这个是错误的 无法改变
```
顶层const表示指针本身就是一个常量，底层const表示指针所指对象是一个常量。

#### 常量表达式和constexpr

常量表达式指值不会改变并且在编译过程中就能得到计算结果的表达式。

如果你认定一个变量是常量表达式，那么就把它声明为constexpr类型。

#### 自定义数据类型

```
struct sales_data { /* */ };
sales_data accum, trans, *salesptr;
```

### 字符串、向量、数组

使用using声明无需专门的前缀即可使用相关的方法，例如：using _namespace::name_;

```
using std::cin;
```

#### 有关string

以下示例包含以下前提代码：

```
#include <string>
using std::string;
```

##### 初始化string

```
string s1; //初始化为空
string s2 = s1;
string s3 = "lalala"; //拷贝初始化
string s4(10, 'a') //十个a转换成的字符串

string s2 = s1; <=> string s2(s1);
string s2 = "aa"; <=> string s2("aa"); //拷贝初始化与直接初始化
```

##### 如何使用getline读取一整行

```
int main () {
	string line;
	while(getline(cin, line))
		cout << line << endl;
	return 0; 
}
```

触发getline函数返回的那个换行符实际上被丢弃了，返回的line中没有那个换行符。

`line.empty()`反应字符串是否为空；`line.size()`返回字符的个数。

注意：size()函数返回值的类型是string::size_type，很神秘，是一个无符号类型的值。所以如果一条表达式中有size()函数，就不要再使用int了，避免错误的产生。使用decltype定义size()的返回值。或者使用`string::size_type n;`

##### 如何字符串相加

```
string s1 = "ee",s2 = "aa";
string a = s1 + s2;
string b = s1 + "aa";
string c = "vv" + "bb"; //错误，字面量不能直接相加
```
综上所说，要实现string的加减，必须要有一方为string类型，而不能染字面量直接相加。

##### 如何遍历字符串
```
for ( declaration : expression(对象))
	statement
```

注意：如果想要改变字符串中的值，一定要将declaration改成引用类型。