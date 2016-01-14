# Note
```C++
//-----------------------------------------------------------
//--------------NOTE for beautiful cpp code!!----------------
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

```
