# Beautiful C++ Code!

+ Int2Str, Str2Int, Float2Str, Str2Float 

```C++
#include <string>
#include <stringstream>
#include <fstream>
using std::string;
using std::stringstream;
using std::stoi;
using std::stod;
using std::ifstream;

//for boost
#include <boost/lexical_cast.hpp>
using boost::lexical_cast;

//----------------------string2double---------------------- 
double string2double(const string& stringNum) {
	return stod(stringNum);
}

//I  : use atof
double string2double(const string& stringNum) {
	double tmp;
	return atof(stringNum.c_str());
}
//II : use stringstream
double string2double(const string& stringNum) {
	double tmp;
	stringstream stream(stringNum);
	stream >> tmp;
	return tmp;
}
//III: use boost
double string2double(const string& stringNum) {
	return lexical_cast<double>(stringNum);
}
//IV : in C++ 11
double string2double(const string& stringNum) {
	return std::stod(stringNum);
}
//----------------------------------------------------------

//-------------------float2string---------------------------
//I : use stringstream, unless you're worried about performance
string float2string(float val) {
	std::stringstream ss;
	ss << val;
	string s(ss.str());
	return s;
}

//II : boost
string float2string(float val) {
	return lexical_cast<string>(val);
}

//III : C++ 11
string float2string(float val) {
	return to_string(val);
}

//-------------------------------------------------------------


//------------------string2int--------------------------------
//I : stoi
int string2int(const string& stringNum) {
	return stoi(stringNum);
}

//II : atoi
int string2int(const string& stringNum) {
	return atoi(stringNum.c_str());
}

//III : stringstream; same string2double

//---------------------------------------------------------------

//-------------------int2string--------------------------------
//best way
string int2string(int val) {
	string numStr = std::to_string(val);
	return numStr;
}

//I : use itoa (got some problems)
string int2string(int val) {
	//char* intStr = itoa(val);
	char* intStr;
	itoa(val, intStr, 10)
	return string(intStr);
}

//II : use stringstream; same as float2string
string int2string(int val) {
	stringstream ss;
	ss << val;
	return ss.str();
}

//III : boost lexical_cast; same as float2string
//IV  : C++ 11; to_string;
//--------------------------------------------------------------
```

+ Miscellany

```C++
//-------------------for i---------------------------
for (std::size_t i = 0; i < 10; i++) //instead of int i;

//------------------string::size_type----------------
string str;
string::size_type  fig_end = str.find_first_not_of(delims);

//----------------------动态生成数组------------------
int N;
int* array = new int[N];

//--------------------nth_element---------------------
vector<int> vals;
for (size_t i = 0; i < 10; i++)
	vals.push_back(i);
std::random_shuffle (vals.begin(), vals.end());
std::nth_element (vals.begin(), vals.begin() + 5, vals.end());

//-------------------file stream----------------------
string filename;
ifstream ifid;
ifid.open(filename.c_str());
//equal, but the latter used oftern,since there is no reason to separate construction and open//
string filename;
ifstream ifid(filename.c_str());
//-----------------------------------------------------

//----------------typename----------------------------
//refer to http://pages.cs.wisc.edu/~driscoll/typename.html
typename std::vector<T>::iterator it;
typedef typename std::vector<T>::iterator iterator_type;
//in the above two examples, we all need typename;

//------------c++ private-------------------------------------
//同Java一样，c++的private也是针对类而言，即同类之间可以互相访问私有变量
//如下例---------Item.h--------------
#ifndef ITEM_H
#define ITEM_H

class Item {
public:
	Item(int val = 0): val(val) {}
	int addVal(const Item& a, const Item& b) const;
private:
	int val;
};

#endif

//--------------Item.cpp---------------
#include "Item.h"

int Item::addVal(const Item& a, const Item& b) const {
	return a.val + b.val;	//这里访问a的私有变量val是合法的。
}

//--------------Another way initialize vector----------
static const int arr[] = {16,2,77,29};
vector<int> vec (arr, arr + sizeof(arr) / sizeof(arr[0]) );

//--------------Self-reference--------------
void f(Date &d) {
	//...
	d.add_day(1).add_month(1).add_year(1);
	//...
}

class Data {
	//...
	Data& add_day(int n) {
		//self-reference
		return *this;
	}

};

//-----------------Singleton-----------------
class Singleton {
public:
	static Singleton &GetInstance() {
		static Singleton instance;
		return instance;
	}
protected:
	Singleton();
	~Singleton();
};
Singleton& si = Singleton::GetInstance();

//--------------用于公共代码的私有函数-------------
//notice: 在普通的非const成员函数中，this的类型是一个指向类类型的const指针
//	  在const成员函数中，this的类型是一个指向const类类型的const指针
class Screen {
public:
	//display overloaded on whethere the object is const or not 
	Screen& display(std::ostream &os) { do_display(os);  return *this; }
	const Screen& display(std::ostream &os) const { do_display(os); return *this;}
private:
	void do_display(std::ostream &os) const { os << contents; }
};
```

+ About explicit

```C++
//-------------about explicit------------------
//Advice:除非有明显的理由想要定义隐式转换，否则，单形参构造函数应该为explicit.
class Sales_item {
public:
	explicit Sales_item(const std::string &book = "") : isbn(book), units_sold(0), revenue(0.0) { }
	explicit Sales_item(std::istream &is);
private:
	//...
};

//error: explicit allowed only on constructor declaration in class header
explicit Sales_item::Sales_item(istream& is) {
	is >> *this;
}

string null_book = "9-999-999";
item.same_isbn(null_book); 				//error: string constructor is explicit
item.same_isbn(Sales_item(null_book)); 	//right
```

+ About inline

```C++
//--------------about inline-------------------
//Three points: (1)inline函数必须要在头文件中定义
//				(2)在声明和定义中使用inline关键字均是合法的
//				(3)在类内部定义的成员函数，默认为inline.
class Screen {
public:
	typedef std::string::size_type index;
	//implicitly inline when defined inside the class declaration
	char get() const { return contents[cursor]; }
	//explicitly declared as inline; will be defined outside the class declaration
	inline char get(index ht, index wd) const;
	//inline not specified in class declarration, but can be defined inline later
	index get_cursor() const;
};

//inline declared in the class declaration; no need to repeat on the definition
char Screen::get(index r, index c) const {
	index row = r * width;
	return contents[row + c];
}

inline Screen::index Screen::get_cursor() const {
	return cursor;
}
```

+ About Overload

```C++
//--------------about iostream overload----------------
//Advice:   (1)所做的格式化尽量少；比如不要输出换行符
//			(2)IO操作符必须为非成员函数，一般设置为相关类的友元。（自己思考其中缘由）（非常经典的一个问题）
//general skeleton of the overloaded output operator
class Sales_item {
	friend std::istream& operator>>(std::istream&, Sales_item&);
	friend std::ostream& operator<<(std::ostream&, Sales_item&);
};

ostream& operator<<(ostream& os, const Sales_item &object) {
	//any special logic to prepare the logic
	
	//actual output of member
	os << s.isbn << "\t" << s.units_sold << "\t"

	//return ostream object
	return os;
}

istream& operator>>(istream& in, Sales_item& s) {
	double price;
	in >> s.isbn >> s.units_sold >> price;
	//check that the inputs succeeded 
	if (in) 
		s.revenue = s.units_sold * price;
	else
		s = Sales_item(); 					//input failed: reset object to default state;
	return in;
}

//===============================================================
//注意，为了和内置操作符保持一致，加法返回一个右值，而不是一个引用。

//================================================================
//赋值操作符和复合赋值操作符应返回左操作数的应用(*this).

//================================================================
//(1)下标操作符必须定义为成员函数
//(2)由于下标操作符既可以当做左值，又可以称为右值，所以返回值要是引用。
//(3)需要有const和非const两个版本
class Foo {
public:
	int &operator[] (const size_t);
	const int &operator[] (const size_t) const;
private:
	vector<int> data;
};

int& Foo::operator[] (const size_t index) {
	return data[index];								//no range checking on index
}

const int& Foo::operator[] (const size_t index) {
	return data[index];
}


//================================================================
//函数对象:定义了调用操作符的类

class GT_cls {
public:
	GT_cls(size_t val = 0): bound(val) { }
	bool operator() (const string &s) { return s.size() >= bound; }
private:
	std::string::size_type bound;
};

vector<string>::size_type wc = count_if(words.begin(), words.end(), GT_cls(6));
```


+ About Has Pointer 

```C++
//From C++ Primer page 419

//======================================================//
//!!!  Not Good Way  !!!
//class that has a pointer member that behaves like a plain pointer
class HasPtr {
public:
	HasPrt(int *p, int i): ptr(p), val(i) { }
	int *get_ptr() const { return ptr; }
	int  get_int() const { return val; }

	void set_ptr(int *p) { ptr = p; }
	void set_int(int  i) { val = i; }

	int get_prt_val() const { return *ptr; }
	void set_ptr_val(int val) const { *ptr = val; }
private:
	int *ptr;
	int  val;
};

//Advice: 具有指针成员且使用默认合成复制构造函数的类具有普通指针的所有缺陷，尤其是，类本身无法避免悬垂指针；

//========================================================//
//!!! Smart Pointer !!!
//private class for use by HasPtr only
//!!! Classical Way of Writing Pointer-used Counter Class  !!!
class U_Ptr {
	friend class HasPtr;
	int *ip;
	size_t use;
	U_Ptr(int *p): ip(p), use(1) { }
	~U_Ptr() { delete ip; }
};

/* smart point class: takes ownership of the dynamically allocated object to which it is bound
 * User code must dynamically allocate an object to initialize a HasPtr and must not delete that object; 
 * the HasPtr class will delete it
 */
class HasPtr {
public:
	HasPtr(int *p, int i): ptr(new U_Ptr(p)), val(i) { }
	HasPtr(const HasPtr &orig): ptr(orig.ptr), val(orig.val) { ++ptr->use; }
	HasPtr& operator=(const HasPtr&);
	~HasPtr() { if (--ptr->use == 0) delete ptr; }

	int *get_ptr() const { return ptr->ip; }
	int get_int() const { return val; }
	void set_ptr(int *p) { ptr->ip = p; }
	void set_int(int i) { val = i; }
	int get_ptr_val() const { return *ptr->ip; }
	void set_ptr_val(int i) { *ptr->ip = i; }

private:
	U_Ptr *ptr;
	int val;
};

HasPtr& HasPtr::operator=(const HasPtr &rhs) {
	++rhs.ptr->use;
	if (--ptr->use == 0)
		delete ptr;
	ptr = rhs.ptr;
	val = rhs.val;
	return *this;
}

//此种方法，副本和原对象仍指向同一基础对象，但是此时已经不用担心dangling pointer problem!!!

//Advice: 由上面阐述的问题可知：具有指针成员的对象一般需要定义复制控制成员，如果依赖合成版本，会有很多问题。

//========================================================//
// 定义值型类; //
/* Valuelike behavior even though HasPtr has a pointer member.
 * Each time we copy a HasPtr object, we make a new copy of the underlying int object to which ptr points.
 */
class HasPtr {
public:
	HasPtr(cosnt int &p, int i): ptr(new int(p)), val(i) { }
	HasPtr(const HasPtr &orig): ptr(new int (*orig.ptr)),  val(orig.val) { }
	HasPtr& operator=(const HasPtr&);
	~HasPtr() { delete ptr; }
private:
	int *ptr;
	int val;
};

HasPtr& HasPtr::operator=(const HasPtr &rhs) {
	*ptr = *rhs.ptr;	//copy the value pointed to
	val = rhs.val;
	return *this;
}
```


	

