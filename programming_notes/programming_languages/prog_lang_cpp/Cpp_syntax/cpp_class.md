
# 重载

operator overloading https://en.cppreference.com/w/cpp/language/operators
- > Customizes the C++ operators for operands of user-defined types.

Overloading the `<<` Operator for Your Own Classes https://docs.microsoft.com/en-us/cpp/standard-library/overloading-the-output-operator-for-your-own-classes?view=msvc-160

13.4 — Overloading the I/O operators https://www.learncpp.com/cpp-tutorial/overloading-the-io-operators/
- > Of course, it makes more sense to do this as a reusable function. And in previous examples, you’ve seen us create `print()` functions that work like this:
  ```cpp
  #include <iostream>
  
  class Point
  {
  private:
      double m_x{};
      double m_y{};
      double m_z{};
  public:
      Point(double x=0.0, double y=0.0, double z=0.0)
        : m_x{x}, m_y{y}, m_z{z}
      {
      }
      double getX() const { return m_x; }
      double getY() const { return m_y; }
      double getZ() const { return m_z; }
      void print() const
      {
          std::cout << "Point(" << m_x << ", " << m_y << ", " << m_z << ')';
      }
  };
  
  int main()
  {
      const Point point{5.0, 6.0, 7.0};
      std::cout << "My point is: ";
      point.print();
      std::cout << " in Cartesian space.\n";
  }
  //////////////////////////////////////////////////
  My point is: Point(5, 6, 7) in Cartesian space.
  ```
  * > While this is much better, it still has some downsides. Because `print()` returns `void`, it can’t be called in the middle of an output statement.
- > **Overloading operator<<**
  ```cpp
  #include <iostream>
  
  class Point
  {
  private:
      double m_x{};
      double m_y{};
      double m_z{};
  public:
      Point(double x=0.0, double y=0.0, double z=0.0)
        : m_x{x}, m_y{y}, m_z{z}
      {
      }
      friend std::ostream& operator<< (std::ostream &out, const Point &point);
  };
  std::ostream& operator<< (std::ostream &out, const Point &point)
  {
      // Since operator<< is a friend of the Point class, we can access Point's members directly.
      out << "Point(" << point.m_x << ", " << point.m_y << ", " << point.m_z << ')'; // actual output done here
      return out; // return std::ostream so we can chain calls to operator<<
  }

  int main()
  {
      const Point point1{2.0, 3.0, 4.0};
      std::cout << point1 << '\n';
      return 0;
  }
  //////////////////////////////////////////////////
  Point(2, 3, 4)
  ```

Overloading stream insertion (<>) operators in C++ https://www.geeksforgeeks.org/overloading-stream-insertion-operators-c/

How to properly overload the << operator for an ostream? https://stackoverflow.com/questions/476272/how-to-properly-overload-the-operator-for-an-ostream

# 成员变量初始化

c++类的成员变量初始化 https://www.jianshu.com/p/497b4fc4a310
- > 普通成员变量的初始化可以在构造函数中进行赋值， 也可以在初始化列表中进行赋值。
- > 静态成员变量必须在类外进行初始化, 且初始化时不加static前缀。
- > const变量在初始化列表中进行初始化。
- > 引用成员变量也需要在初始化列表中进行初始化， 类似于const型。

类的成员变量初始化总结 https://blog.csdn.net/tham_/article/details/44938731
```console
首先把需要初始化的成员变量分为几类：
Ø  一般变量(int)
Ø  静态成员变量(static int)
Ø  常量(const int )
Ø  静态常量(static const int)

对应的初始化方式是：
Ÿ  一般变量可以在初始化列表里或者构造函数里初始化，不能直接初始化或者类外初始化
Ÿ  静态成员变量必须在类外初始化
Ÿ  常量必须在初始化列表里初始化
Ÿ  静态常量必须只能在定义的时候初始化(定义时直接初始化)
```

## 初始化列表

C++ 类构造函数初始化列表 https://www.runoob.com/w3cnote/cpp-construct-function-initial-list.html || https://www.cnblogs.com/BlueTzar/articles/1223169.html
- > 构造函数初始化列表以一个冒号开始，接着是以逗号分隔的数据成员列表，每个数据成员后面跟一个放在括号中的初始化式。例如：
  ```cpp
  class CExample {
  public:
      int a;
      float b;
      //构造函数初始化列表
      CExample(): a(0),b(8.8)
      {}
      //构造函数内部赋值
      CExample()
      {
          a=0;
          b=8.8;
      }
  };
  ```
- > 上面的例子中两个构造函数的结果是一样的。上面的构造函数（使用初始化列表的构造函数）显式的初始化类的成员；而没使用初始化列表的构造函数是对类的成员赋值，并没有进行显式的初始化。
- > 初始化和赋值对内置类型的成员没有什么大的区别，像上面的任一个构造函数都可以。对非内置类型成员变量，为了避免两次构造，推荐使用类构造函数初始化列表。但有的时候必须用带有初始化列表的构造函数：
  * > 1.成员类型是**没有默认构造函数的类**。若没有提供显示初始化式，则编译器隐式使用成员类型的默认构造函数，若类没有默认构造函数，则编译器尝试使用默认构造函数将会失败。
  * > 2.**const 成员**或**引用类型**的成员。因为 const 对象或引用类型只能初始化，不能对他们赋值。
- > **初始化数据成员与对数据成员赋值的含义是什么？有什么区别？**
- > 首先把数据成员按类型分类并分情况说明:
  * > 1.**内置数据类型，复合类型（指针，引用）**- 在成员初始化列表和构造函数体内进行，在性能和结果上都是一样的
  * > 2.**用户定义类型（类类型）**- 结果上相同，但是性能上存在很大的差别。因为类类型的数据成员对象在进入函数体前已经构造完成，也就是说在成员初始化列表处进行构造对象的工作，调用构造函数，在进入函数体之后，进行的是对已经构造好的类对象的赋值，又调用个拷贝赋值操作符才能完成（如果并未提供，则使用编译器提供的默认按成员赋值行为）
- > **注意点**：
  * > 初始化列表的成员初始化顺序: C++ 初始化类成员时，是按照声明的顺序初始化的，而不是按照出现在初始化列表中的顺序。

C++ 初始化列表 https://www.cnblogs.com/graphics/archive/2010/07/04/1770900.html

C++初始化列表，知道这些就够了 - 小豆君的干货铺的文章 - 知乎 https://zhuanlan.zhihu.com/p/33004628

# 其他

c++　在函数后加const的意义 https://blog.csdn.net/qq_32739503/article/details/83341222
```console
c++ 函数前面和后面 使用const 的作用：
  · 前面使用const 表示返回值为const
  · 后面加 const表示函数不可以修改class的成员
```
