# Note
+ 对父类的同名函数的访问：
	* baseclassnaeme::访问基类同名函数或属性（*而Java中可以用super,C#中可以用base*）
+ 继承:
	* 实现机理：内存中包含了父类的所有内容（*除了虚函数*）
+ C++空类中自动创建的函数：
  * 缺省构造函数、拷贝构造函数、赋值运算符、析构函数、取址运算符
+ default constructor: consts and references must be initialized, so a class including them cannot be default-constructed unless explicitly supply constructor.

  ```C++
  struct X
  {
  const int a;
  const int& r;
  }
  X x; //error
  ```
+ More



