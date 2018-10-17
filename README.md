# esoteric-features-in-modern-cpp
本文探讨现代C++(17,20)中那些**鲜为人知甚至未曾实现过**的一些特性，资料来源于cppref的编译器支持一览表，也欢迎贡献那些本文未曾提到的无人问津之地。看看我们地表最复杂语言已经进化到何种程度了:smile:。

本地编译器使用`MSVC2017(19.x)`,`g++ 7.1`,`clang++5.0`。为了支持一些新特性，也会使用线上编译器：`g++ 8.2`,`clang++7.0`。

# C++ 17
| 特性 | 提案 | 说明 |
| :------: | ------: | ------: |
| `_has_include_`预处理条件 | [P0061R](http://www.open-std.org/jtc1/sc22/wg21/docs/papers/2015/p0061r1.html) | to write |
| `[[maybe_unused]]` 属性| [P0212R1](http://www.open-std.org/jtc1/sc22/wg21/docs/papers/2016/p0212r1.pdf)| to write |


# 参考
> https://en.cppreference.com/w/cpp/compiler_support

> https://isocpp.org/

> https://en.wikipedia.org/wiki/C%2B%2B17 and https://en.wikipedia.org/wiki/C%2B%2B20

> https://wandbox.org/

> https://gcc.godbolt.org/
