
const 只修饰两种类型 int 和 int*
const只对它左边的东西起作用， 唯一的例外就是const本身就是最左边的修饰符，那么它才会对右边的东西起作用

> 指向const 对象的指针可以 被赋 以 一个非const 对象的地址 
> const 对象的地址只能赋值给指向const 对象的指针 不应该通过指针来修改一个被声明为const的对象
> 指向const 的指针常被用作函数的形式参数，保证被传递给函数的实际对象在函数得实际对象在函数中不会被修改 
> 常量在定义后就不能被修改,所以它必须被初始化。未初始化的常量定义将导致编译错误

```
#include <iostream>

int main(){

        int a = 10;
        int b = 20;

        const int *pa = &a;
        int const *pb = &a;
        int* const pc = &a;
        *pa = 11;  // 错误：向只读位置‘* pa’赋值
        *pb = 11;  // 错误：向只读位置‘* pb’赋值
        *pc = 11;

        pa = &b;
        pb = &b;
        pc = &b; // 错误：向只读变量‘pc’赋值
}
```



# 1. const 修饰变量

语法：const 数据类型 常量名 = 常量值;

## 基本数据类型

在变量定义前加关键字const，修饰该变量为常量，不可修改

```
#include <iostream>
using namespace std;
int main(){
        const int i = 100;
        i = 200;            // 错误：向只读变量‘i’赋值
        return 0;
}
```

# 2. const 修饰指针

## const修饰指针 --- 常量指针

语法：const 数据类型 * 变量名；

const修饰的是指针，指针可以指向别的对象，指针指向的值不可以更改

### 基本数据类型的指针
```
#include <iostream>
using namespace std;
int main() {
        int i = 100;
        int k = 200;

        const int *pi = &i;
        int *pk = &k;

        *pi = 101;  // 错误：向只读位置‘* pi’赋值
        *pk = 201;

        cout << "i: " << i << " ,k: " << k << endl;

        return 0;
}
```

### 对象的指针

```
#include <iostream>
using namespace std;

class Person{
public:
        int age;
        Person(int age){
                this-> age = age;
        }
        void show() const {
                cout << "age: " << age << endl;
        }
};

int main(){
        Person p1(10);
        Person p2(20);

        const Person* pp1 = &p1;
        Person* pp2 = &p2;

        // pp1->age = 11;  // 错误：assignment of member ‘Person::age’ in read-only object
        pp2->age = 21;

        pp1->show();
        pp2->show();

        pp1 = &p2;  // 指针指向可以改，指针指向的值不可以更改

        pp1->show();
        pp2->show();

        return 0;
}

```

## const修饰常量 --- 指针常量

引用的本质

const修饰的是常量，指针指向不可以改，指针指向的值可以更改

```
#include <iostream>
using namespace std;

class Person{
public:
        int age;
        Person(int age){
                this-> age = age;
        }
        void show() const {
                cout << "age: " << age << endl;
        }
};

int main(){
        Person p1(10);
        Person p2(10);

        Person* const pp = &p1;
        pp -> age = 20;

        pp = &p2; // 错误：向只读变量‘pp’赋值

        pp->show();
        return 0;
}
```

## const即修饰指针，又修饰常量

语法：const 数据类型 * const 变量名；

```
#include <iostream>
using namespace std;：
int main(){
        int i = 10;
        int k = 20;

        const int* const p = &i;
        *p = 20; // 错误：向只读位置‘*(const int*)p’赋值
        p = &k; // 错误：向只读变量‘p’赋值

        return 0;
}
```

# 3. const修饰函数形参

const修饰形参（也叫常量引用修饰形参），防止形参改变实参

```
#include <iostream>
using namespace std;

class Person{
public:
        int age;
        Person(int age){
                this-> age = age;
        }
        void show() const {
                cout << "age: " << age << endl;
        }
};

void fun(const int* p){
        *p = 10; // 错误：向只读位置‘* p’赋值
}

void fun(const Person* p) {
        p -> age = 20; // 错误：assignment of member ‘Person::age’ in read-only object
}

int main() {
        int i = 1;
        fun(&i);
        Person p(1);
        fun(&p);
        p.show();
        return 0;
}
```

# 4. const修饰函数返回值

## 基本数据类型

当函数返回基本数据类型（如 int、float 等）时，使用 const 修饰返回值通常没有太大意义。因为基本类型的返回值通常是按值返回，即返回的是一个副本。修改这个副本并不会影响原始值

```
const int getValue() {
    return 5;
}
```

## 返回对象或复合类型的常量引用

当函数返回对象或复合类型（如自定义类、结构体等）时，使用 const 修饰返回值可以防止返回的对象或复合类型被修改。这是一种常见且有用的做法，特别是在返回类的成员变量时

```
#include <iostream>
using namespace std;

class Person{
public:
        int age;
        Person(int age){
                this-> age = age;
        }
        void show() const {
                cout << "age: " << age << endl;
        }
};

const Person* fun() {
        Person* p = new Person(15);
        return p;
}

int main() {
        const Person* p = fun();
        p -> age = 20; // 错误：assignment of member ‘Person::age’ in read-only object
        p -> show();
        return 0;
}
```

# 5. const修饰成员函数：常函数

* 成员函数后加const后我们称为这个函数为常函数
* 常函数内不可以修改成员属性
* 成员属性声明时加关键字mutable后，在常函数中依然可以修改

```
#include <iostream>
using namespace std;

class Person{
public:
        int age;
        Person(int age){
                this-> age = age;
        }
        void show() const {
                this -> age = 10; // assignment of member ‘Person::age’ in read-only object
                cout << "age: " << age << endl;
        }
};

int main() {
        Person p(5);

        p.show();
        return 0;
}

```

# 6. const修饰类对象：常对象

* 声明对象前加const称该对象为常对象
* 常对象只能调用常函数

语法：const 类名 对象名; 


常对象只能调用const修饰的成员函数，常对象可以访问const或者非const数据成员，但不能修改，除非成员用mutable修饰

```
#include <iostream>
using namespace std;

class Person{
public:
        int age;
        Person(int age){
                this-> age = age;
        }
        void show() const {
                cout << "age: " << age << endl;
        }
};

int main(){
        const Person p(10);
        p.show();
        cout << "p.age: " << p.age << endl;
        return 0;
}
```


# 7. const和constexpr
constexpr 和 const 都是 C++ 中用于声明常量的关键字，但它们在使用上有一些重要的区别：

## const

* const 用于声明一个常量，表示变量的值不可修改。
* const 可以用于各种类型的变量，包括基本数据类型、对象、指针等。
* const 变量的值可以在运行时确定。这意味着它可以被初始化为在编译时未知的值，比如函数返回值或者用户输入。
* const 更加通用，适用于任何需要防止修改的场景。

## constexpr

* constexpr 用于声明表达式为编译时常量，意味着它的值必须在编译时就已知。
* constexpr 常量可以用在需要编译时常量表达式的上下文中，如数组大小、整数模板参数等。
* constexpr 函数能在编译时对其输入进行计算，只要所有输入也都是编译时已知的常量。
* 使用 constexpr 声明的变量或函数表示你希望编译器验证它们能够在编译时求值。
* constexpr 要求其初始化表达式必须是一个编译时常量表达式。

## 主要区别

* 编译时 vs. 运行时：constexpr 确保变量或函数的值能在编译时被确定，而 const 变量的值可以在运行时确定。
* 使用场景：constexpr 适用于需要在编译时进行计算的场景，比如作为模板参数或数组大小。const 更适用于程序运行中不需要修改的值。


