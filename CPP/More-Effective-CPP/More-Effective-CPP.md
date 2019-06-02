# Basics

### Item1: distinguish between pointers with references 
+ reference一定要指向某个对象,C++要求reference必须有初值
+ refernce总是指向它最初获得那个对象
+ 像`operator[]`返回的应该是reference

### Item2: prefer C++-style casts

### Item3: Never treat arrays polymorphically

### Item4: Avoid gratuitous default constructors(非必要不要提供default constructors)


# Operators

### Item5: Be wary of user-defined conversion functions

### Item6: Distinguish between prefix and postfix forms of increment and decrement operators

### Item7: Never overload "&&", "||", or ","

### Item8: Understand the difference meanings of new and delete


# Exceptions

### Item9: Use destructors to prevent resource leaks

### Item10: Prevent resource leaks in constructors

### Item11: Prevent exceptions from leaving destructors

### Item12: Understand how throwing an exception differs from passing a parameter or calling a virtual function

### Item13: Catch expections by reference

### Item14: Use exception specifications judiciously

### Item15: Understand the costs of exception handling


# Efficiency

### Item16: Remember the 80-20 rule

### Item17: Consider using lazy evaluation

### Item18: Amortize the cost of expected computations

### Item19: Understand the origin of temporary objects

### Item20: Facilitate the return value optimization 

### Item21: Overload to avoid implicit type conversion

### Item22: Consider using op= instead of stand-alone op.

### Item23: Consider alternative libraries

### Item24: Understand the costs of virtual functions, multiple inheritance, virtual base classes, and RTTI


# Techniques, Idioms, Patterns

### Item25: Virtualizing constructors and non-member functions

### Item26: Limiting the number of objects of a class

### Item27: Requiring or prohibiting heap-based objects

### Item28: Smart Pointers

### Item29: Reference Counting

### Item30: Proxy Classes

### Item31: Making functions virtual with respect to more than one object


# Miscellany

### Item32: Program in the future tense

### Item33: Make non-leaf classes abstract

### Item34: Understand how to combine C++ and C in the same program

### Item35: Familiarize yourself with the language standard