---
title: cpp2
date: 2025-08-29 09:13:26
tags: teach-cpp
comments: true
excerpt: C++第二课
categories: teach-cpp
---

# 欢迎来到我的C++小课程

## 第二课

上节课我们完成了C++环境搭建，今天开始学习**核心编程概念**  
`C++`的变量和数据类型是**所有程序的基础**，特点是**严格高效**

### 一、变量与赋值

1. **变量定义**  
   变量是存储数据的容器，需要声明类型：  
   ```cpp
   #include <string>
   using namespace std;
   
   int main() {
       string name = "小明";  // 字符串
       int age = 18;         // 整数
       double height = 1.75; // 浮点数 
       char grade = 'A';     // 字符
       return 0;
   }
   ```
2. **静态类型**
   变量类型不可改变：
   ```cpp
   int main() {
       int x = 1;    //x是整数
       // x = "py"; //错误：类型不匹配
       return 0;
   }
   ```
   
### 二、基础数据类型

| 类型      | 示例              | 说明                |
|-----------|-------------------|---------------------|
| `int`     | `3`, `-7`         | 整数                |
| `double`  | `3.14`, `-0.01`   | 浮点数              |
| `string`  | `"hello"`         | 字符串（双引号）    |
| `char`    | `'A'`, `'1'`      | 字符（单引号）      |
| `bool`    | `true`, `false`   | 布尔值              |

```cpp
// 类型查看
#include <iostream>
#include <typeinfo>
using namespace std;

int main() {
    int age = 18;
    cout << typeid(age).name() << endl;  // 输出：int
    return 0;
}
```

### 三、输入

1. 用`cin`来接受,如：
   ```cpp
   #include <iostream>
   #include <string>
   using namespace std;
   
   int main() {
       string a;
       cin >> a;  //输入了一个字符串a
       return 0;
   }
   ```
   
### 四、类型转换

1. 用`static_cast<类型名>变量名`来转换,如：
   ```cpp
   #include <iostream>
   #include <string>
   using namespace std;
   
   int main() {
       int a;
       cin >> a;              //输入了一个整数a
       double d = static_cast<double>(a); //整数转浮点数
       char c = static_cast<char>(a);  //整数转字符
	   return 0;
   }
   ```
   
### 五、作业
1. **作业**
   定义三个变量存储`你的名字`,`你的年龄`,`你的体重`
   再输入
   再输出,空格分隔
   
   **提交方式**
   将作业代码文件发送至**手机-微信:18372735812**
   
**谢谢大家的观看**
有问题可联系**手机-微信:18372735812**