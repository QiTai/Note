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


	
