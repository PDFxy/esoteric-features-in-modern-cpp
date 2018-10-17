# esoteric-features-in-modern-cpp
本文探讨现代C++(11,14,17,20)中那些**鲜为人知甚至未曾实现过**的一些特性，资料来源于cppref的编译器支持一览表。由于本文对**鲜为人知**的定义是根据个人的判断，主观性极强，所以如果您觉得某些条目不适用，请在Issue中讨论，也欢迎贡献那些本文未曾提到的无人问津之地。看看我们地表最复杂语言已经进化到何种程度了:smile:。

本地编译器使用`MSVC2017(19.x)`,`g++ 7.1`,`clang++5.0`。为了支持一些新特性，也会使用线上编译器：`g++ 8.2`,`clang++7.0`。

## C++ 17
| 特性 | 提案 | 示例和说明 |
| :------: | ------: | ------: |
| `_has_include_`预处理条件 | [P0061R](http://www.open-std.org/jtc1/sc22/wg21/docs/papers/2015/p0061r1.html) | to write |
| `[[maybe_unused]]`属性| [P0212R1](http://www.open-std.org/jtc1/sc22/wg21/docs/papers/2016/p0212r1.pdf)| to write |
| 内联变量 | [P0386R2](http://www.open-std.org/jtc1/sc22/wg21/docs/papers/2016/p0386r2.pdf) | to write |
| 保证式拷贝消除 | [P0135R1](http://www.open-std.org/jtc1/sc22/wg21/docs/papers/2016/p0135r1.html) | to write |
| [折叠表达式](https://en.cppreference.com/w/cpp/language/fold) | [N4295](http://www.open-std.org/jtc1/sc22/wg21/docs/papers/2014/n4295.html) | to write |
| 构造函数继承 | [P0136R1](http://www.open-std.org/jtc1/sc22/wg21/docs/papers/2015/p0136r1.html) | to write |
| `nan()`,`nearbyint()`,`nextafter()`等数学函数| [P0226R1](http://www.open-std.org/jtc1/sc22/wg21/docs/papers/2016/p0226r1.pdf) | to write |
| if/switch中的初始化语句 | [P0305R1](http://www.open-std.org/jtc1/sc22/wg21/docs/papers/2016/p0305r1.html) | to write |


## C++ 14
| 特性 | 提案 | 示例和说明 |
| :------: | ------: | ------: |
| [`std::quoted`](https://en.cppreference.com/w/cpp/io/manip/quoted) | [N3654](http://www.open-std.org/jtc1/sc22/wg21/docs/papers/2013/n3654.html) | to write |

## C++ 11
| 特性 | 提案 | 示例和说明 |
| :------: | ------: | ------: |
| 最小化垃圾回收接口(**未曾实现**) | [N2670](http://www.open-std.org/jtc1/sc22/wg21/docs/papers/2008/n2670.htm) | to write |
| 外部模板实例化 | [N1987](http://www.open-std.org/jtc1/sc22/wg21/docs/papers/2006/n1987.htm) | to write |

# 参考
> https://en.cppreference.com/w/cpp/compiler_support

> https://isocpp.org/

> https://en.wikipedia.org/wiki/C%2B%2B17 and https://en.wikipedia.org/wiki/C%2B%2B20

> https://wandbox.org/

> https://gcc.godbolt.org/
