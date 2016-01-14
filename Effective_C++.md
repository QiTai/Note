#Note
```C++
//-----------------------------------------------------------------------------------
//Item 6: Explicitly disallow the use of compiler-generated functions you don't want.
//Two ways: (1)将相应的成员函数声明为private,并且不予实现
//          (2)使用像Uncopyable这样的基类，如下

class Uncopyable {
protected:
	Uncopyable() { }
	~Uncopyable() { }
private:
	Uncopyable(const Uncopyable&);
	Uncopyable& operator=(const Uncopyable&);
};

class HomeForSale: private Uncopyable {

};


```
