### Pointer Misuse ###
```cpp
void f(int n, int x) {
	Gadget* p = new Gadget{n}; 							// look I'm a java programmer!
	//...
	if (x < 100) throw std::runtime_error{"Weird!"};	// leak
	if (x < 200) return;								// leak
	//...
	delete p;											// I want my garbage collector
```
 + garbage collection would not release non-memory resources

### Resource Handles and Pointers ###
+ A `std::shared_ptr` releases its object at when the last shared_ptr to it is destoryed
```cpp
void f(int n, int x) {
	auto p = make_shared<Gadget>(n);					// manage that pointer!
	//...
	if (x < 100) throw std::runtime_error{"Wierd!"};	// no leak
	if (x < 200) return; 								// no leak
	//...
}
```
+ `shared_ptr` provides a form of garbage collection
	* But I'm not sharing anything!


+ A `std::unique_ptr` releases its object at when it goes out of scope
```cpp
void f(int n, int x) {
	auto p = make_unique<Gadget>(n);
	//...
	if (x < 100) throw std::runtime_error("Wierd!");
	if (x < 200) return;
	//...
}
```
+ This is simple and cheap
	* No more expensive than a "plain old pointer"


+ But why use a pointer at all?
	* if you can, just use a scoped variable
```cpp
void f(int n, int x) {
	Gadget g{n};
	//...
	if (x < 100) throw std::runtime_error{"Weird!"};
	if (x < 200) return;
	//...
}
```
+ No explicit resource management
	* Code not littered with (easy to forget) try-catch
	* No spurious allocations/deallocations
	* No pointers

### Error Handling and Resources ###
+ "Resource Acquisition is Initialization" (RAII)
	* Acquire during construction
	* Release in destructor
+ Throw Exception in case of failure
	* In particular, throw is a constructor cannot construct and object
+ Never throw while holding a resource not owned by a handle
+ In general
	* Leave established invariants intact when leaving a scope


### Why do we use pointers? ###
+ references, iterators, etc

+ To represent ownership
	* **Don't! Stop!** Instead, use handles
+ To reference resources
	* from within a handle
+ To represent positions
	* Be careful
+ To pass large amounts of data(into a function)
	* pass by const reference
+ To return large amount of data(out of a function)
	* **Don't!** Instead use move operations.


### How to get a lot of data cheaply out of a function? ###
+ Consider 
	* factory functions
	* functions returning lots of objects
+ Return a pointer to a **new**'d object?
```cpp
M* operator+(const M&, const M&);
M* pm = m1 + m2;	// ugly: and who does the delete;
M* q  = *pm + m3;	// ugly: and who does the delete;
```
+ Return a reference to a **new**'d object?
```cpp
M& operator+(const M&, const M&);
M m = m1 + m2;		// looks　OK: but who does the delete? Delete what?
```
+ Pass a target object?
```cpp
void operator+(const M&, const M&, M& res);
M m;
operator+(m1, m2, m);	// ugly: We are regressing towards assembly code
```
+ Return an object!
	* `M operator+(const M&, const M&)`
	* How?
		+ Copies are expensive
	* Tricks to avoid copying are brittle
	* Tricks to avoid copying are not general
+ **Return a handle**
	* Simple and cheap!

### Move Semantics ###
+ Return a Matrix
```cpp
Matrix operator+(const Matrix& a, const Matrix& b) {
	Matrix r;
	// copy a[i] + b[i] into r[i] for each i
	return r;
} 
Matrix res = a + b;
```
+ Define move a construtor for Matrix
	+ don't copy, "steal the representation"

+ Direct support in C++ 11: **Move Constructor** *To devel into*
```cpp
class Matrix {
	Representation rep;
	//...
	Matrix(Matrix&& a) {		// move constructor
		rep = a.rep;		// *this gets a's element
		a.rep = { }		// a becomes the empty Matrix
	}
};
Matrix res = a + b;
```

+ Often, you can avoid writing copy and move operations	
	* Easily avoid
```cpp
class Matrix {
	vector<double> elem; 	// elements here
	//... matrix access ...
};
```

+ Matrix just "inherit" resource management from vector
+ Copy and a move operations can often be implicitly generate from members
	* Good copy and move operations
	* from the standard library

### Garbage Collection ###
+ GC is neither general nor ideal
+ Apply these techniques in order:
	* Store data in containers
		+ The semantics of the fundemental abstraction is reflected in the interface
	* Manage all resources with resource handles
		+ RAII
		+ Not just memory: all resources
	* Use "Smart pointers"
		+ But they are still pointers
	* Plug in a garbage collector
		+ For "litter collection"
		+ C++11 specifies a GC interface
		+ Can still leak non-memory resources


### Range-for, auto, and move ###
+ As ever, what matters is how features work in combination
```cpp
template<typename C, typename V>
vector<Value_type<C>* > find_all(C& c, V v) 	//find all occurrences of v in c
{
	vector<Value_type<C>*> res;
	for (auto& x : c)
		if (x == v)
			res.push_back(&x);
	return res;
}

string m{"Mary had a little lamb"};
for (const auto p : find_all(m, 'a')) 		// p is a char*
	if (*p != 'a')
		cerr << "string bug!\n";
```		

### 50:00 ###
