# esoteric-features-in-modern-cpp
本文探讨现代C++(11,14,17,20后续会补上)中那些鲜为人知甚至未曾实现过的一些特性。资料来源于cppref的编译器支持一览表,添加原则是**鲜为人知**或者**少有人知但是用处极大的**，也欢迎贡献本文未曾提到的无人问津之地。让我们看看地表最复杂的语言已经进化到什么程度了:smile:。

编译器使用`MSVC2017(19.15.x)`,`g++ 8.2`,`clang++7.0`。

## C++ 17
| 特性 | 提案 | 示例和说明 |
| :------: | ------: | ------: |
| `_has_include`预处理条件 | [P0061R](http://www.open-std.org/jtc1/sc22/wg21/docs/papers/2015/p0061r1.html) | [std17.md](std17.md) |
| `[[maybe_unused]]`属性 | [P0212R1](http://www.open-std.org/jtc1/sc22/wg21/docs/papers/2016/p0212r1.pdf) | [std17.md](std17.md) |
| `[[nodiscard]]`属性 | [P0189R1](http://www.open-std.org/jtc1/sc22/wg21/docs/papers/2016/p0189r1.pdf) | to write |
| 内联变量 | [P0386R2](http://www.open-std.org/jtc1/sc22/wg21/docs/papers/2016/p0386r2.pdf) | to write |
| 保证式拷贝消除 | [P0135R1](http://www.open-std.org/jtc1/sc22/wg21/docs/papers/2016/p0135r1.html) | to write |
| 折叠表达式 | [N4295](http://www.open-std.org/jtc1/sc22/wg21/docs/papers/2014/n4295.html) | to write |
| 构造函数继承 | [P0136R1](http://www.open-std.org/jtc1/sc22/wg21/docs/papers/2015/p0136r1.html) | to write |
| `nan()`,`nearbyint()`,`nextafter()`等数学函数| [P0226R1](http://www.open-std.org/jtc1/sc22/wg21/docs/papers/2016/p0226r1.pdf) | to write |
| if/switch中的初始化语句 | [P0305R1](http://www.open-std.org/jtc1/sc22/wg21/docs/papers/2016/p0305r1.html) | to write |
| `constexpr` lambda表达式 | [P0170R1](http://www.open-std.org/jtc1/sc22/wg21/docs/papers/2016/p0170r1.pdf) | to write |
| [`std::string_view`](https://en.cppreference.com/w/cpp/string/basic_string_view) | [N3921](http://www.open-std.org/jtc1/sc22/wg21/docs/papers/2014/n3921.html) | to write |
| 结构化绑定 | [P0217R3](http://www.open-std.org/jtc1/sc22/wg21/docs/papers/2016/p0217r3.html) | to write |
| `constexpr` if语句 | [P0292R2](http://www.open-std.org/jtc1/sc22/wg21/docs/papers/2016/p0292r2.html) | to write |

## C++ 14
| 特性 | 提案 | 示例和说明 |
| :------: | ------: | ------: |
| `std::quoted` | [N3654](http://www.open-std.org/jtc1/sc22/wg21/docs/papers/2013/n3654.html) | to write |
| `0b/0B`二进制字面值 | [N3472](http://www.open-std.org/jtc1/sc22/wg21/docs/papers/2012/n3472.pdf) | to write |
| 变量模板(variable template) |  [N3651](http://www.open-std.org/jtc1/sc22/wg21/docs/papers/2013/n3651.pdf) | to write |

## C++ 11
| 特性 | 提案 | 示例和说明 |
| :------: | ------: | ------: |
| 最小化垃圾回收接口(**未曾实现**) | [N2670](http://www.open-std.org/jtc1/sc22/wg21/docs/papers/2008/n2670.htm) | to write |
| 外部模板实例化 | [N1987](http://www.open-std.org/jtc1/sc22/wg21/docs/papers/2006/n1987.htm) | to write |
| 泛型(多态)lambda表达式 | [N3649](http://www.open-std.org/jtc1/sc22/wg21/docs/papers/2013/n3649.html) | to write |
| 单引号分隔数字字面值 | [N3781](http://www.open-std.org/jtc1/sc22/wg21/docs/papers/2013/n3781.pdf) | to write |

# 参考
> https://en.cppreference.com/w/cpp/compiler_support

> https://isocpp.org/

> https://en.wikipedia.org/wiki/C%2B%2B17 and https://en.wikipedia.org/wiki/C%2B%2B20

> https://wandbox.org/

> https://gcc.godbolt.org/

## 许可协议
<a rel="license" href="http://creativecommons.org/licenses/by/4.0/"><img alt="知识共享许可协议" style="border-width:0" src="https://i.creativecommons.org/l/by/4.0/88x31.png" /></a><br />本作品采用<a rel="license" href="http://creativecommons.org/licenses/by/4.0/">知识共享署名 4.0 国际许可协议</a>进行许可。