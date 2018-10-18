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