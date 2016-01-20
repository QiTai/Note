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
```
