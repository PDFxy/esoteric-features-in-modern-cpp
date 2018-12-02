# 1.1 `_has_include`预处理条件
如果`A.h`文件存在则`__has_include("A.h")`会求值出1，否则0。再配合上`#if`系列宏就可以完成一个预处理阶段的文件存在性检查：
```cpp
#include <iostream>

#if __has_include(<hello>)//__has_include("hello")搜索用户当前路径，不过这些都是实现定义
#  define have_hello 1
#else
#  define have_hello 0
#endif

int main() {
    std::cout << have_hello << std::endl;
    return 0;
}
```

# 1.2 `[[maybe_unused]]`属性
如果开了`-Wunused-variable`,遇到定义但是未使用的变量编译器就会
` warning: unused variable xxx [-Wunused-variable]`，这个属性就是用来压制编译器的抱怨的：
```cpp
union [[maybe_unused]] B{};

class [[maybe_unused]] A{
    [[maybe_unused]] int v1;
    [[maybe_unused]] static int v2;
    [[maybe_unused]] typedef int Int;
    using UInt [[maybe_unused]] = unsigned int;
};

[[maybe_unused]] void Func([[maybe_unused]] int arg){
    [[maybe_unused]] int a;
}
enum { 
    OP_ADD [[maybe_unused]],
    OP_SUB [[maybe_unused]] = 42 
};
```
但不同的编译器都有不同程度的支持：`g++8.2`会warning非静态成员`v1`不适用`[[maybe_unused]]`，`clang7.0`和`msvc2017`则不会报任何warning。

# 1.3 `[[nodiscard]]`属性
nodiscard顾名思义，不建议抛弃。如果一个函数返回一个标注了`[[nodiscard]]`的enum/类，或者函数本身就是`[[nodiscard]]`,那么编译器就会对返回值有没有用到的调用发出warning：
```cpp
struct [[nodiscard]] A { };
enum class[[nodiscard]]  B{};

A returnA(){return A();}
B returnB(){return B{};}
[[nodiscard]] int returnInt(){return 1;}

void miss() {
    returnA();
    returnB();
    returnInt();
}

```
亲爱的clang warning道:
```shell
prog.cc:9:5: warning: ignoring return value of function declared with 'nodiscard' attribute [-Wunused-result]
    returnA();
    ^~~~~~~
...
```
g++不但warning还note：
```shell
prog.cc: In function 'void miss()':
prog.cc:9:13: warning: ignoring returned value of type 'A', declared with attribute nodiscard [-Wunused-result]
     returnA();
             ^
prog.cc:4:3: note: in call to 'A returnA()', declared here
 A returnA(){return A();}
   ^~~~~~~
prog.cc:1:22: note: 'A' declared here
 struct [[nodiscard]] A { };
                      ^
...
```
# 1.4 内联变量(inline variable)
函数可以内联，命名空间可以内联，好了，现在变量也可以内联了。内联变量类似于内联函数，他告诉链接器即使有多个编译单元使用这个变量，也保证只有一份定义，而不是抛出重定义异常。
举个例子，我们有三个文件：

`A.h`:
```cpp
#ifndef _A
#define _A

int k = 7;

#endif
```
`B.cpp`:
```cpp
#include "A.h"
void fun(){}
```
`C.cpp`:
```cpp
#include "A.h"

int main(){
    return 0;
}
```
然后我们编译它:
```bash
$ clang++ B.cpp C.pp -c
$ clang++ B.o C.o
```
然后理所当然我们收到k重定义的错误：
```bash
C.o : error LNK2005: "int k" (?k@@3HA) 已经在 B.o 中定义
a.exe : fatal error LNK1169: 找到一个或多个多重定义的符号
clang++.exe: error: linker command failed with exit code 1169 (use -v to see invocation)
```

现在`A.h`使用内联变量：
```cpp
#ifndef _A
#define _A

inline int k = 7;

#endif
```
再进行编译，天空晴朗，了无异常。k的重定义不复存在。

# 1.5 保证式拷贝消除

# 1.6 折叠表达式

# 1.7  继承构造函数(inheriting constructors)
其实C++11已有继承构造函数，C++17只是做了些reword的工作。考虑下面这个例子：
```cpp
#include <iostream>

struct Base{
  int k;double d;char c;
  Base(int k, double d, char c):k(k),d(d),c(d){
    std::cout<<"k="<<k<<",d="<<d<<",c="<<c<<"\n";
  }
};
struct Derive : Base{
  Derive(int k, double d, char c):Base(k,d,c){}
};

int main(){
  Derive d(400820,3.14,'f');
  return 0;
}
```
Derive的那个**非常非常长**的构造函数只是把参数传递给Base的构造函数，别无其他。而这个工作已经在Base构造函数体现过，我们有理由也完全可以复用它。基于此考虑，就有了继承构造函数:
```cpp
struct Derive : Base{
  //Derive(int k, double d, char c):Base(k,d,c){}
  using Base::Base;
};
```

# 1.9 if/switch中的过初始化语句
先定义变量再判断变量值是个常用的语句,在C++17z之前，我们需要这样写:
```cpp
Expr* k = evalBinaryExpr(lhs,rhs,op);
if(typeof(k)==typeof(IntExpr)){
  ...
}
```
现代的语言如Golang运行在if中完成这两个逻辑关联的操作，C++17对此提供了直接的支持，我们也能像golang一样：
```cpp
if(Expr* k = evalBinaryExpr(lhs,rhs,op);typeof(k)==typeof(IntExpr)){
  ...
}
```

# 2.0 `constexpr` lambda表达式

# 2.1 `std::string_view`
一句话概括，`std::string_view`用于代替`const std::string&`或`const std::string`。

它不持有字符串，只是一个字符串的视图。也就是说这个对象可以用来观察字符串，但是不能基于这个对象改变字符串；它观察的字符串可以被改变，这个改变也能被观察到：
```cpp
    std::string s = "aaa";
    std::string_view p = s; //观察s
    std::cout << p;         //aaa
    s = "bbb";              //改变它观察的字符串值
    std::cout << p;         //bbb
```

# 2.2 结构化绑定

# 2.3 constexpr if语句

# 2.4 std::any
`std::any`类似于其他标准库的variant，它可以容纳任何类型值，然后通过`std::any_cast<Type>()`来获取值：
```cpp
#include <any>
#include <iostream>
struct F {
    int k = 1024;
};

int main() {
    std::any obj = F();
    std::cout << std::any_cast<F>(obj).k;
    obj = 1;
    obj = 3.14;
    obj = true;
    obj = 'c';
    std::cout << obj.has_value();
    obj.reset();
    std::cout << obj.has_value();
    return 0;
}
```
注意如果转换失败，即类型不匹配就会抛出`std::bad_any_cast`异常：

# 2.5 std::apply