## Compile Time And Runtime
- **Compile Time**: Occurs during compilation, where source code is translated into machine code.
- **Runtime**: Occurs during program execution, where machine code is executed by the computer.

### Compile Time Errors
**Syntax Errors**:

Syntax errors occur when the code violates the rules of the programming language syntax.

```cpp
int x = 10;
std::cout << "The value of x is: " << x  // Missing semicolon
```

**Type Errors**:

Type errors occur when there is a mismatch between the types of operands in an expression.

```cpp
int x = 10;
std::cout << "The value of x is: " << x << std::endl; // '<<' expects two operands
```

**Undefined Symbols**:

Undefined symbol errors occur when the compiler cannot find a definition for a symbol used in the code.

```cpp

    int main() {
        foo(); // 'foo' is not defined
        return 0;
    }
```

### Runtime Errors:
Runtime errors occur during the execution of the program and are detected by the runtime environment. These errors occur when the program encounters unexpected conditions or behavior that cannot be handled.

**Division by Zero**:
Division by zero occurs when attempting to divide a number by zero, which is undefined.

```cpp

int numerator = 10;
int denominator = 0;
int result = numerator / denominator; // Division by zero
```

**Null Pointer Dereference:**

Null pointer dereference occurs when attempting to access or modify the value pointed to by a null pointer.

```cpp
int* ptr = nullptr;
*ptr = 10; // Null pointer dereference
```

**Out of Bounds Access**:

Out of bounds access occurs when attempting to access elements of an array or container beyond its valid index range.


```cpp
int arr[5] = {1, 2, 3, 4, 5};
int value = arr[10]; // Out of bounds access
```

**Memory Allocation Failures**:

Memory allocation failures occur when the program fails to allocate memory dynamically using operators like new or malloc.

```cpp
int* ptr = new int[1000000000000]; // Memory allocation failure
```

## Upcasting
- It involves treating a derived class object as a base class object.
- This means that you're casting a pointer or reference to a derived class object to a pointer or reference of one of its base classes.

```cpp
Derived derived_obj;
Base* base_ptr = &derived_obj;
```

- An object of the `Derived` class named `derived_obj` is created.
- A pointer `base_ptr` of type `Base*` is assigned the address of `derived_obj`. This is possible because a derived class object can be treated as a base class object due to inheritance.
- Using `base_ptr`, we can only access members that are part of the `Base` class.
- `Derived` class member cannot be accessed through `base_ptr`.

## Accessing Derived class member using Base type pointer - Downcasting
- You can access derived class members in an upcasted pointer or reference by explicitly downcasting it back to the derived class type.
- Downcasting involves casting a pointer or reference of a base class type to a pointer or reference of a derived class type.

```cpp
Derived derived_obj;
Base* base_ptr = &derived_obj;

/* Downcasting */
Derived* derived_ptr = dynamic_cast<Derived*>(base_ptr);
```
## Virtual Function And Upcasting

- If you have a virtual function in the base class and you override it in the derived class, then using upcasting, the overridden function from the derived class will be accessible, not the base class function.
- Otherwise, the base class virtual function will be called.

## Compiler-Generated Constructors in C++

If we don't provide any constructors for a class, the compiler generates several constructors for you. These are commonly referred to as the **"compiler-generated constructors"** or **"default constructors"**. The constructors generated by the compiler include:


- Default Constructor
- Copy Constructor
- Copy Assignment Operator
- Move Constructor
- Move Assignment Operator

## Function Stack Frame

- A function's stack frame:
  - Represents a segment of memory.
  - Allocated on the call stack.
  - Stores information pertaining to the function's invocation and execution.
- Upon function invocation:
  - A new stack frame is created.
  - Positioned atop the call stack.
- Crucial details stored within the stack frame include:
  - Function parameters.
  - Local variables.
  - Return address.
  - Occasionally, supplementary bookkeeping data.

## Constructors in C++

- **Parameter Constructor**: Initializes an object with specified parameters. (Pre C++11)
- **Default Constructor**: Initializes an object without any arguments. (Pre C++11)
- **Copy Constructor**: Creates a new object as a copy of an existing object. (Pre C++11)
- **Conversion Constructor**: Implicitly converts one type to another during object initialization. (Pre C++11)
- **Explicit Constructor**: Prevents implicit conversions and requires explicit use during object initialization. (C++11)
- **Move Constructor**: Transfers resources from a temporary object to another object. (C++11)
- **Forwarding Constructor**: Forwards arguments to another constructor within the same class. (C++11)
- **Initializer List Constructor**: Initializes member variables using initializer lists. (C++11)
- **Constructor Delegation**: Invokes another constructor within the same class to perform initialization. (C++11)

## Default Constructor

If a default constructor is not explicitly provided by the programmer, the compiler does not automatically generate one. However, the compiler generates a default constructor when it's needed.

1. If a class doesn't have any constructors and it's based on another class that does have a default constructor, then the compiler has to make a default constructor for the new class.

2. When a class doesn't have any constructors, but it includes an object from another class that does have a default constructor, the compiler has to make a default constructor for the first class.

3. If a class has virtual functions but no default constructor, the compiler creates one to set up virtual pointer (VPtr).

4. ?? Class with virtual base class ??

## Constructor Call Order
Order of calls in the prologue (before the constructor body begins execution) and epilogue (after the constructor body completes execution) of a default constructor in C++ is typically as follows:

**Prologue**

1. Memory allocation for the object (e.g., stack allocation for local variables or heap allocation using `new` for dynamically allocated objects).

- Is memory allocation done from prologue?

2. Initialization of member variables with initializers.
3. Call to the constructor of the base class (if the class inherits from a base class).

**Epilogue**

1. Call to destructors for initialized member variables (if any) or deallocation of dynamically allocated memory.
2. Call to the destructor of the base class for cleanup.

## Memory Segments
- **Stack**:
  - Used for storing local variables, function parameters, and return addresses.
  - Automatically allocated and deallocated as functions are called and return.
  - Fixed-size memory region that grows and shrinks during program execution.

- **Heap**:
  - Used for dynamic memory allocation.
  - Large pool of memory for allocating memory blocks of varying sizes.
  - Memory management is the programmer's responsibility.
  - Memory allocated on the heap isn't automatically deallocated.

- **Data Segment**:
  - Used for storing initialized global and static variables.
  - Contains variables with fixed sizes and explicit initializers.
  - Allocated before program execution and remains constant in size during runtime.

- **Code Segment**:
  - Used for storing executable code instructions.
  - Mapped into memory when the program is loaded for execution.
  - Remains constant throughout program execution.

## Construction of a Class Object in C++

- **Memory Allocation**:
  - When an object of a class is created, memory is allocated for that object. The size of the memory allocated depends on the size of the class and its members.

- **Constructor Call**:
  - After memory allocation, the constructor of the class is called. The constructor is a special member function of the class responsible for initializing the object's state. It can initialize member variables, allocate resources, and perform any other necessary setup.

- **Initialization**:
  - Inside the constructor, member variables can be initialized either with default values or with values provided by the constructor's parameters.

- **Execution of Constructor Body**:
  - The constructor's body contains any additional initialization logic or code that needs to be executed during object creation. This could include initializing base class subobjects, calling other member functions, or performing any necessary setup.

- **Completion of Object Construction**:
  - Once the constructor has finished execution, the object is considered fully constructed and ready for use.

- **Object Destruction**:
  - When the object goes out of scope or is explicitly deleted using the `delete` operator, the destructor of the class is called. The destructor is responsible for releasing any resources acquired by the object during its lifetime and performing cleanup operations.

## Object Creation vs Constructor

- **Object Creation**:
  - Refers to the process of instantiating an object of a class.
  - Involves allocating memory for the object and initializing its state.
  - Occurs when you declare a variable of a class type or dynamically allocate memory for an object using operators like `new` (in C++).

- **Constructor**:
  - A special member function of a class that is automatically called when an object of that class is created.
  - Responsible for initializing the newly created object's state.
  - Can initialize member variables, allocate resources, and perform any other necessary setup.
  - Used to ensure that objects are properly initialized before they are used.

In summary:
- Object creation is the process of creating an instance of a class.
- A constructor is a method within a class that is invoked during the object creation process to initialize the object's state.

```cpp
#include<iostream>

using namespace std; /* Bad practice */

#define line(msg) cout<<"----------"#msg"----------\n";

class Animal {
public:
    Animal() {

    }
    void fun() {

    }
};

class Tiger : public Animal {
public:
    Tiger()
    /* Animal::Animal */
    { 

    }
};

int main() {
    Tiger tiger; /* Tiger::Tiger */

    return 0;
}
```
&nbsp;

If the derived class does not have a constructor, the constructor of the base class will only be called from the prologue of the derived class constructor. In such cases, the compiler will generate its own default constructor.
```cpp
class Animal{

    public:
    Animal(){

    }
    void fun(){

    }
};

class Tiger : public Animal{

    public:


};

int main(){

    Tiger tiger; /* Tiger::Tiger */

    return 0;
}
```
```cpp
class Eye{
    public:
    Eye(){

    }
    void fun(){

    }
};

class Lion{

    Eye eyes; 
    public:
    Lion()
    /* Eye :: Eye */
    { 

    }
};

int main(){

    Lion lion; /* Lion :: Lion */
}
```

## Virtual Functions

## Smart Pointer
Smart pointer is a class template that behaves like a pointer but provides automatic memory management, helping to avoid memory leaks and other memory-related errors common in manual memory management.

```cpp
#include<iostream>
using namespace std; /* Bad practice */
#define line(msg) cout<<"----------"#msg"----------\n";

class CA{

    public:
    CA()
    {
        cout << "CA Ctor\n";
    }

    void fun()
    {
        cout << "CA fun\n";
    }

    ~CA()
    {
        cout << "CA D-tor\n";
    }
};

class Smart_ptr
{   
    static void* operator new(size_t) = delete;
    static void* operator new[](size_t) = delete;
    static void operator delete(void*) = delete;
    static void operator delete[](void*) = delete;

    CA* pt;
    public:
    Smart_ptr(CA* pt = NULL) : pt(pt)
    {

    }

    CA* operator->()
    {
        return pt;
    }

    CA& operator*()
    {
        return *pt;
    }

    operator CA*()
    {
        return pt;
    }

    ~Smart_ptr()
    {
        delete pt;
    }

};
int main()
{

    Smart_ptr sm1 = new CA();
    sm1->fun();
    (*sm1).fun();
    return 0;
}
```

### Why Allocating Smart_ptr Objects on the Heap Is Not Recommended:

- Purpose of Smart_ptr: Designed to manage memory of another object, such as a CA object.

- Automated Memory Management: Smart pointers automate memory management, reducing risk of leaks and dangling pointers.

- Manual Management Burden: Allocating Smart_ptr on heap introduces manual memory management for Smart_ptr itself, negating its purpose.

- Potential for Memory Leaks: Manual management of Smart_ptr on heap can lead to memory leaks if not handled properly.

### operator-> and operator*
These two overloaded operators (operator-> and operator*) in the Smart_ptr class provide syntactic sugar to access members of the CA object pointed to by the Smart_ptr. Here's an explanation of each operator along with a dry run:

#### operator->()

- **Description:** This operator allows you to access the members of the CA object as if you were directly accessing them through a pointer to CA.
- **Usage:** When you use the arrow (->) notation with an object of type Smart_ptr, it automatically calls this operator and returns the pointer pt to the CA object.
- **Functionality:** This enables you to access the members of the CA object through the Smart_ptr object directly.
- **Example:** `sm1->fun();`
- **Dry Run:** Assuming sm1 points to a valid CA object, operator->() returns pt, which is a pointer to the CA object. Then, fun() is called on the CA object using the returned pointer.

#### operator*()

- **Description:** This operator allows you to dereference the Smart_ptr object as if it were a pointer to CA.
- **Usage:** When you use the asterisk (*) notation with an object of type Smart_ptr, it automatically calls this operator and returns a reference to the CA object itself.
- **Functionality:** This enables you to access the CA object itself through the Smart_ptr object directly.
- **Example:** `(*sm1).fun();`
- **Dry Run:** Assuming sm1 points to a valid CA object, operator*() returns a reference to the CA object. Then, fun() is called on the referenced CA object.

#### operator CA*()
Defines a type conversion operator in the Smart_ptr class. Specifically, it is a conversion operator to convert the Smart_ptr object to a raw pointer to CA 

(* sm1).fun(); is resolved by both the operator*() and operator CA*().

- CA& operator*(): This overloaded operator dereferences the Smart_ptr object, returning a reference to the CA object itself. Therefore, (*sm1) results in obtaining a reference to the CA object.

- operator CA*(): This conversion operator allows the Smart_ptr object to be implicitly converted to a raw pointer to CA. Therefore, (* sm1) can also be implicitly converted to a CA*.

Given that both operator*() and operator CA*() can be applied to (* sm1), the expression (* sm1).fun(); can be resolved using either of them. However, the compiler prefers the more specific option, which is operator*(), as it directly returns a reference to the CA object.

```cpp
CA& operator*()
{
    return *pt;
}

operator CA*()
{
    return pt;
}
```
#### Copy Constructor With Ownership Transfer
```cpp
Smart_ptr(const Smart_ptr& object) : pt(object.pt)
{
    Smart_ptr& refSP = const_cast<Smart_ptr&>(object);
    refSP.pt = NULL;

}
```
#### Assignment Operator With Swap & Copy
```cpp
void Swap(Smart_ptr& object)
{
    std::swap(this->pt,object.pt);
}

Smart_ptr& operator=(const Smart_ptr& object)
{   
    if(this == &object) return *this;

    Smart_ptr temp(object);
    Swap(temp); 
    /* temp.swap(*this)*/
    return *this;

}
```

This syntax invokes a member function named Swap on the current object (*this), passing temp as an argument.
```cpp
Swap(temp);
```
This syntax calls a member function named swap on the temp object, passing *this (the current object) as an argument.
```cpp
temp.swap(*this)
```
## Lvalue And Rvalue
- Lvalue:
  - An lvalue (locator value) refers to an object that occupies some identifiable location in memory (i.e., it has an address).
  - Lvalues often correspond to named variables or objects that persist beyond a single expression.
  - You can take the address of an lvalue using the address-of operator (&).
  - Examples of lvalues include variables, references, and dereferenced pointers.

- Rvalue:
  - An rvalue (right value) refers to an object that does not necessarily have an identifiable memory location.
  - Rvalues are typically temporary and short-lived, often used as temporary values during expressions or as the result of expressions.
  - You cannot take the address of an rvalue.
  - Examples of rvalues include literal constants, temporary objects created during expression evaluation, and the result of certain functions (like overloaded operators).

## Move Constructor

- Rvalue References:
  - Rvalue references, denoted by `&&`,type of reference that can bind to temporary objects and non-const rvalues.
  - They are used to distinguish between lvalues and rvalues, allowing functions and constructors to behave differently based on whether they are passed an lvalue or an rvalue.

- Move Semantics:
  - Move semantics work by enabling the efficient transfer of resources (such as memory allocations) from one object to another, rather than making expensive copies.

- Move Constructors:
  - Move constructors are special member functions that take an rvalue reference as a parameter.
  - They are used to implement move semantics, allowing objects to efficiently transfer resources from temporary objects or objects about to be destroyed.
  - Move constructors are invoked automatically when an object is constructed from an rvalue or when an object is passed to a function by value.
  - Avoids Deep Copy

```cpp
CA(CA&& par) noexcept : a(par.a) 
{
  par.a = NULL;
  cout << "Move Constructor [" << this << "] a = [ " << a << " ]\n";
}
```
```cpp
#include<iostream>
using namespace std; /* Bad practice */
#define line(msg) cout<<"----------"#msg"----------\n";

class CA
{
    int* a;

    public:
    CA() : a(new int(1000))
    {
        cout << "Constructor [" << this << "] \n";
    }

    CA(const CA& o) : a(new int(*o.a))
    {
        cout << "Deep Copy [" << this << "] a = [ "<< a << " ]\n";
    }

    CA(CA&& par) noexcept : a(par.a) 
    {

        par.a = NULL;
        cout << "Move Constructor [" << this << "] a = [ " << a << " ]\n";
    }

    ~CA() noexcept
    {   
        cout << "Destructor [" << this << "] \n";
        delete a;
    }
};

/*
-fno-elide-constructor
*/
CA Factory()
{
    line(In factory fun);
    CA temp;
    cout << "Do Business\n";

    line();
    return temp;
}

void fun(CA obj)
{
    cout << "Start Business\n";
}
int main()
{   
    
  CA obj = Factory();
  line(main);

  return 0;
}
```
```plaintext
----------In factory fun----------
Constructor [0x7fffaf4b2700] 
Do Business
--------------------
Move Constructor [0x7fffaf4b2740] a = [ 0x562f842fc2c0 ]
Destructor [0x7fffaf4b2700] 
Move Constructor [0x7fffaf4b2738] a = [ 0x562f842fc2c0 ]
Destructor [0x7fffaf4b2740] 
----------main----------
Destructor [0x7fffaf4b2738] 
```

## noexcept
- `noexcept` is a specifier used to declare that a function will not throw any exceptions.
- It is used to provide information to the compiler and to help with code optimization, as well as to convey the exception safety guarantees of functions.

```cpp
void myFunction() noexcept {
  
}
```
## std::move()
- `std::move()` is a utility function provided by the C++ Standard Library that facilitates the use of move semantics. 
- It is used to convert an lvalue into an rvalue reference, enabling the efficient transfer of resources (such as dynamically allocated memory) from one object to another.
- It allows you to explicitly indicate that you are willing to "move" the resources from one object to another, rather than making a copy.
- `std::move()` is commonly used in conjunction with move constructors, move assignment operators, and functions that accept rvalue references as parameters.

### How it Works:

- When you pass an object to `std::move()`, it casts the object to an rvalue reference, effectively indicating that you are willing to transfer ownership of its resources.
- This allows move constructors or move assignment operators to be invoked, rather than copy constructors or copy assignment operators, when passing the object to functions or assigning it to other objects.
- It does not move any resources itself; it simply enables move operations by casting the object to an rvalue reference.

### Usage:

- `std::move()` is commonly used in scenarios where you have a temporary object or an object that you no longer need and want to transfer its resources to another object efficiently.
- It is often used when passing objects to functions that expect rvalue references, such as move constructors or move assignment operators.
- `std::move()` should be used with caution to avoid dangling references or undefined behavior, as it does not perform any safety checks.

```cpp
MyClass(MyClass&& other) noexcept {
    // Move resources from 'other' to 'this'
}

int main() {
MyClass obj1;
MyClass obj2 = std::move(obj1); // Move 'obj1' resources to 'obj2'
return 0;
}
```

```cpp
#include<iostream>
using namespace std; /* Bad practice */
#define line(msg) cout<<"----------"#msg"----------\n";

class CA
{
    int* a;

    public:
    CA() : a(new int(1000))
    {
        cout << "Constructor [" << this << "] \n";
    }

    CA(const CA& o) : a(new int(*o.a))
    {
        cout << "Deep Copy [" << this << "] a = [ "<< a << " ]\n";
    }

    
    CA(CA&& par) noexcept : a(par.a) 

    {

        par.a = NULL;
        cout << "Move Constructor [" << this << "] a = [ " << a << " ]\n";
    }

    ~CA() noexcept
    {   
        cout << "Destructor [" << this << "] \n";
        delete a;
    }
};

void f1(CA obj)
{
    cout << "Apple\n";
}

void f2(CA& obj)
{
    cout << "Apple\n";
}

void f3(CA&& obj)
{
    cout << "Apple\n";
}

int main()
{   

    CA obj;
    line();
    //f1(obj);
    line();

    f1(std::move(obj)); 
    /*
    move - priotizes the move constructor over copy constructor if mover constructor exist.

    */

    // f2(std::move(obj));
    /*error -  Sending lvaue in rvalue*/

    f3(std::move(obj)); /* rvalue reference is passed */
    return 0;
}
```

- std::move(): prioritizes the move constructor over the copy constructor if the move constructor exists.

## std::forward<>()
- `std::forward()` is used to forward arguments passed to a function to another function, typically within a template context.
- It allows you to preserve the value category (lvalue or rvalue) of the forwarded arguments, enabling efficient forwarding of both lvalues and rvalues.

### Perfect Forwarding:
- Perfect forwarding refers to forwarding function arguments in a way that preserves their original value category (lvalue or rvalue).
- It allows you to forward arguments to other functions or constructors without unnecessary copying or moving, optimizing performance.

```cpp
#include <iostream>

void anotherFunction(int&& value) {
    std::cout << "Received rvalue: " << value << std::endl;
}

void anotherFunction(int& value) {
    std::cout << "Received lvalue: " << value << std::endl;
}

template<typename T>
void process(T&& arg) {
    anotherFunction(std::forward<T>(arg));
}

int main() {
    int x = 42;
    process(x); /* lvalue */
    process(std::move(x)); /* rvalue */
    return 0;
}
```

### Universal Reference And RValue Reference

- **Universal Reference**:
  - Universal references are declared using the syntax `T&&`, where `T` is a template parameter.
  - They are typically used in function templates to accept any type of argument, preserving its original value category (lvalue or rvalue).
  - Universal references are used in perfect forwarding scenarios, where you want to forward arguments to other functions while preserving their original value category.
```cpp
void process(T&& arg)
```

- **Rvalue Reference**:
  - Rvalue references are declared using the syntax `T&&`, where `T` is a **type (not a template parameter)**.
  - They are used to bind to temporary objects or expressions that can be safely moved from.
  - Rvalue references are commonly used in move semantics, allowing efficient transfer of resources from one object to another.
  - They bind only to rvalues; they cannot bind to lvalues. This restriction ensures that they are used primarily for temporary objects.
```cpp
void process(int&& arg)
```
### Wrapper


