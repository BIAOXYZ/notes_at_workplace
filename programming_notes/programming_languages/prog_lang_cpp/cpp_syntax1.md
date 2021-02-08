
# `++i` 与 `i++`

在C++中，为什么部分程序员喜欢在loop写‘++i’而不是‘i++’？ - 知乎 https://www.zhihu.com/question/316271945
- 在C++中，为什么部分程序员喜欢在loop写‘++i’而不是‘i++’？ - 土地测量员的回答 - 知乎 https://www.zhihu.com/question/316271945/answer/625417961
  * > `++i`和`i++`在效率上可能会有差别。对于内置的整型来说，编译器都会直接编译出inc之类的指令，++i和i++没有差别；但对于自定义的类型，++i和i++会调用两个不同的operator++重载函数，签名一般分别是`T& T::operator++()`， `T T::operator++(int)`。`++i`直接操作原对象，然后返回其引用；`i++`一般会先拷贝一个新的对象tmp，然后操作原对象，最后将tmp返回。后者明显多出了好几个操作(引起了若干次的不必要的构造和析构)，所以基本都会优先使用++i。更新一下，编译器开优化后可以做到让这两效率相同。

在程序开发中，++i 与 i++的区别在哪里？ - 知乎 https://www.zhihu.com/question/19811087
- 在程序开发中，++i 与 i++的区别在哪里？ - 叶王的回答 - 知乎 https://www.zhihu.com/question/19811087/answer/80210083
  * > i++ 与 ++i 的主要区别有两个：
    ```console
    1、 i++ 返回原来的值，++i 返回加1后的值。
    2、 i++ 不能作为左值，而++i 可以。
    ```
  * > 毫无疑问大家都知道第一点（不清楚的看下下面的实现代码就了然了），我们重点说下第二点。**首先解释下什么是左值**（以下两段引用自中文维基百科『右值引用』词条）。
    >> 左值是对应内存中有确定存储地址的对象的表达式的值，而右值是所有不是左值的表达式的值。
    >
    > 一般来说，**左值是可以放到赋值符号左边的变量**。但
    >> 能否被赋值不是区分左值与右值的依据。比如，C++的const左值是不可赋值的；而作为临时对象的右值可能允许被赋值。**左值与右值的根本区别在于是否允许取地址&运算符获得对应的内存地址**。
    >
    > 比如，
    ```cpp
    int i = 0;
    int *p1 = &(++i); //正确
    int *p2 = &(i++); //错误
    
    ++i = 1; //正确
    i++ = 5; //错误
    ```
  * > 那么为什么『i++ 不能作为左值，而++i 可以』？看它们各自的实现就一目了然了：以下代码来自博客：[为什么(i++)不能做左值，而(++i)可以](https://blog.csdn.net/zlhy_/article/details/8349300)
    ```cpp
    // 前缀形式：
    int& int::operator++() //这里返回的是一个引用形式，就是说函数返回值也可以作为一个左值使用
    {//函数本身无参，意味着是在自身空间内增加1的
      *this += 1;  // 增加
      return *this;  // 取回值
    }

    //后缀形式:
    const int int::operator++(int) //函数返回值是一个非左值型的，与前缀形式的差别所在。
    {//函数带参，说明有另外的空间开辟
      int oldValue = *this;  // 取回值
      ++(*this);  // 增加
      return oldValue;  // 返回被取回的值
    }
    ```
  * > 如上所示，i++ 最后返回的是一个临时变量，而**临时变量是右值**。
- 在程序开发中，++i 与 i++的区别在哪里？ - 空气的回答 - 知乎 https://www.zhihu.com/question/19811087/answer/13034165
  ```console
  根本区别是语义上的区别，这个书上有，一个返回+之后的值一个返回+之前的值。
  如果没有用到返回值的话，区别在于效率。 
    • 若i是内置的数值类型，两者完全一样 
    • 若i是一些自定义的类，如iterator，++i的效率 > = i++的效率 
  对于后者推荐都用++i；对于前者，用哪个是程序风格问题，i++的好处是更符合人类思维习惯，++i的好处是每次都用这种形式就不用考虑i的类型。
  ```

C: What is the difference between ++i and i++? https://stackoverflow.com/questions/24853/c-what-is-the-difference-between-i-and-i
- https://stackoverflow.com/questions/24853/c-what-is-the-difference-between-i-and-i/24858#24858

Is there a performance difference between i++ and ++i in C? https://stackoverflow.com/questions/24886/is-there-a-performance-difference-between-i-and-i-in-c
- https://stackoverflow.com/questions/24886/is-there-a-performance-difference-between-i-and-i-in-c/24887#24887