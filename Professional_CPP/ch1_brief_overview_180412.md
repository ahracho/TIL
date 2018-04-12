# Profession C++ (by Marc Gregoire)

#### 블록체인 코어 개발 스터디 1주차 (4/6)


# Chapter 1 : A Crash Course in C++ and the STL

## WHAT’S IN THIS CHAPTER?
- C++에서 가장 중요한 문법과 STL을 훑어본다.
- Smart Pointer에 대해 알아본다.
---  


# The Basics of C++

## Hello, World
~~~c++
// helloworld.cpp
#include <iostream>

int main() {
    std::cout << "Hello, World" << std::endl;
    return 0;
}
~~~

굉장히 간단한 Hello, world 출력문이지만
- 주석 : // 한 줄, /* */ 여러 줄
- 전처리 : C++ 프로그램은 전처리 --> 컴파일 --> 링킹 순으로 동작한다.
- main 함수
- 입출력이 포함되어 있다.

## Namespaces
Namespace는 함수나 변수 등의 이름이 중복되는 문제를 해결하기 위해 사용된다. 예를 들어, 내가 foo()라는 함수를 정의해서 사용하고 있었는데 include한 외부 라이브러리에 동일한 이름의 함수가 있다면 컴파일러는 내가 어떤 foo() 함수를 사용하고 싶은지 알 수 없다. 이런 경우에 Namespace가 유용하게 사용되는데, 내가 어떤 context의 foo()를 사용할 건지 명확히 할 수 있기 때문이다.

namespace 정의와 구현은 아래와 같이 하면 된다.  
~~~c++
// namespaces.h
namespace mycode {
    void foo();
}
~~~   

~~~c++
#include <namespaces.h>
#include <iostream>
namespace mycode {
    void foo() {
        std::cout << "foo() from mycode namespace" << std::endl;
    }
}
~~~  

해당 함수를 호출할 때는 namespace::함수이름() 이렇게 사용한다. 하지만 매번 namespace를 명시해주는 게 귀찮다면 using을 사용하면 된다. 다만 너무 과하게 사용하여 namespace를 사용하지 않았을 때와 같은 문제가 발생하지 않도록 주의한다(동일한 이름의 함수를 구분할 수 없게 되는 문제).  

~~~c++
#include <iostream>
using namespace mycode

int main() {
    foo(); // mycode::foo()로 인식
    return 0;
}
~~~  

namespace 내의 특정 함수/변수에만 using을 사용할 수도 있다.  
~~~c++
// using namespace std;
using std::cout;
cout << "Hello, World!" << std::endl;
~~~  

**WARNING: 헤더 파일은 다른 사람들도 가져다 쓸 수 있기 때문에 using문을 절대 헤더 파일에 넣지 않도록 주의한다.**  


## Variables
변수는 C와 거의 비슷하다.

### casting
~~~c++
float myFloat = 3.14f;
int i1 = (int)myFloat;                      // method 1
int i2 = int(myFloat);                      // method 2
int i3 = static_cast<int>(myFloat); // method 3
~~~  

첫번째 방법은 C에서처럼 사용한 건데 추천하지 않는 방법, 두번째 방법은 첫번째보다는 낫지만 거의 사용하지 않는다. 세번째 방법이 가장 안전하고 추천하는 방법이다 (10장에서 캐스팅에 대해서 더 자세히 다룰 예정).

## Arrays
### std::array
C++에서도 C 스타일 배열을 사용할 수 있지만, array 라이브러리에 있는 std::array를 사용하는 것이 크기를 쉽게 구할 수 있고, iteration을 쉽게 할 수 있다는 것 이외에도 많은 이점이 있다.  

~~~C++
#include <iostream>
#include <array>
using namespace std;

int main()
{
    array<int, 3> arr = {9, 8, 7};
    cout << "Array size = " << arr.size() << endl;
    cout << "Element 2 = " << arr[1] << endl;
    return 0;
}
~~~

**NOTE: std::array도 C 스타일 배열과 마찬가지로 크기는 선언될 때 정해지고, 크기를 늘리거나 줄일 수 없다. 동적인 배열을 사용하고 싶다면 std::vector를 사용하면 된다.**  

## Loops
### The Range-Based for Loop
C 스타일 배열을 포함해서, begin()과 end() 함수를 사용할 수 있는 배열에는 모두 사용할 수 있는 loop 방식이다.  

~~~ c++
std::array<int, 4> arr = {1, 2, 3, 4};
for (int i : arr) {
    std::cout << i << std::endl;
}
~~~

## Function
### Alternative Function Syntax
C++ 11 이후로, 함수를 정의할 때 return 타입을 제일 앞에 적는 대신 아래와 같이 화살표 뒤에 적어도 된다. 보통의 경우에는 그렇게 효용성이 없지만 template 함수(11장, 21장에서 다룸)의 리턴 타입을 적을 때 유용하다. 
_The auto keyword in this context has the meaning of starting a function prototype using the alternative function syntax._
~~~c++
auto func(int i) -> int
{
    return i + 2;
}
~~~  

### Function Return Type Deduction
C++ 14 이후로, 아래와 같이 아예 리턴 타입을 auto로 적고 생략해도 된다.  
~~~c++
auto divideNumbers(double numerator, double denominator)
{
    if (denominator == 0) { /* ... */ }
        return numerator / denominator;
}
~~~

## Type Inference Part 1
Type inference는 컴파일러에게 변수 타입을 명확히 알려주지 않고 컴파일러가 상황에 따라 해석하도록 하는 기능으로, **auto**와 **decltype** 두가지 키워드로 구현할 수 있다.

### The auto Keyword
auto 키워드는 네가지 의미로 사용된다.
- 컴파일 타임에 컴파일러에게 변수 타입을 추론하라고 시킴
~~~c++
auto x = 123;
auto result = getFoo();
~~~
- Alternative Function Syntax를 사용한 함수 프로토타입의 시작을 가리킴
~~~c++
auto func(int i) -> int
{
    return i + 2;
}
~~~  
- 함수의 리턴 타입을 함축
- lambda 문법에서 사용(17장에서 다룸)

### The decltype Keyword
decltype은 아래와 같이 문장을 argument로 받아서 해당 문장의 타입을 알아낸다. decltype도 간단한 문장에서는 효용성이 드러나지 않지만, template과 함께 사용되면 굉장히 유용하다.
~~~c++
int x = 32;
decltype(x) y = 44;
~~~

---

# Diving Deeper into C++

## Pointers and Dynamic Memory
### The Stack and the Heap
동적 메모리는 크게 Stack과 Heap으로 구분할 수 있는데, stack은 함수나 지역변수의 값이 저장되는 영역이고, heap은  stack이나 현재 실행되고 있는 함수와 독립적으로 메모리를 할당하여 값을 저장할 수 있는 영역이다. stack은 LIFO 방식으로 운영되고 함수 실행이 종료되면 자동적으로 사용했던 스택 영역이 해제되기 때문에 메모리 해제를 신경쓰지 않아도 된다. 그에 반해 heap은 사용자가 직접 할당하고, 해제까지 신경써야한다.  

### Working with Pointers
new 키워드로도 힙 영역에 메모리 할당 가능하다.
~~~C++
int* myIntegerPointer = nullptr; // 포인터 변수만 만들었지 메모리 할당은 아직 안됨
myIntegerPointer = new int; // int만큼 메모리 할당
*myIntegerPointer = 8;

// 다 쓰고 메모리 해제해야
delete myIntegerPointer;
myIntegerPointer = nullptr;
~~~   

### Dynamically Allocated Arrays
new[] 연산을 사용하면 heap 영역에 배열을 할당할 수 있다.  
~~~c++
int arraySize = 8;
int* myVariableSizedArray = new int[arraySize]; // 메모리 할당
myVariableSizedArray[3] = 2;
delete[] myVariableSizedArray; // 메모리 해제 중요!!
~~~  
위의 코드에서 myVariableSizedArray 변수 자체는 stack에 저장되지만 이 변수가 가리키는 int 8 배열은 heap에 할당된다.  

**NOTE : C에서처럼 malloc()과 free()를 사용하지 말고, new / delete나 new[] / delete[]를 사용하도록 한다.**  
**WARNING : 메모리 누수를 방지하기 위해서 반드시 new / delete 쌍을 맞추도록 한다.**  

### Null Pointer Constant
C++ 11 이전에는 0이 정수 0이기도 하면서 null pointer를 나타내기도 했는데, 이렇게 사용하면 0이 integer인지 null pointer인지 판단해야 하는 상황에서 오류가 발생할 수 있기 때문에 앞으로는 null pointer로서의 0 대신 **nullptr**을 사용하도록 한다.  

### Smart Pointers
C 스타일 포인터를 사용할 때 자주 발생하는 메모리 문제를 해결하기 위해서 대신 스마트포인트를 사용하도록 한다. 스마트포인터는 해당 메모리를 사용하지 않을 때 자동으로 해제해준다.  

세 가지 종류의 스마트포인터가 있는데, 모두 <memory> 헤더에 정의되어 있다.
**1. std::unique_ptr**  
필요없을 때 자동으로 메모리를 해제한다는 것을 제외하면 보통의 포인터와 거의 유사하다. 포인터가 가리키는 object를 유일하게 제어할 수 있다(has sole ownership of the object pointed to).  
~~~C++
Employee* anEmployee = new Employee; // 지양
auto anEmployee = std::make_unique<>(Employee); // C++ 14 이상
std::unique_ptr<Employee> anEmployee(new Employee); // C++ 14 미만
~~~  

**2. std::shared_ptr**  
가리키는 데이터의 오너십을 여럿이서 가질 수 있다. 다른 포인터 변수가 해당 데이터를 가리킬 때마다 reference counter가 하나씩 증가한다. RC가 0이 되면 메모리는 해제된다. 다만, array는 shared_ptr에 저장할 수 없다. 사용할 때는 std::make_shared<>()를 사용한다.  

**3. std::weak_ptr**
weak_ptr은 RC를 증가시키지 않고 shared_ptr을 바라볼 수 있게 한다.

**NOTE : 포인터를 사용해야 한다면 std::unique_ptr을 기본으로, 여럿이 사용해야 할 때는 std::shared_ptr을 사용하도록 한다. auto_ptr은 C++ 표준에서 deprecated 되었으니 주의한다.**  


## Type Inference Part 2
auto를 사용하면 간편하지만 auto는 references와 const에 대한 정보를 담지 않는다.
~~~c++
const string message = "TEST";

const string& foo() {
    return message;
}

auto f1 = foo(); // f1의 타입은 string이 되어 "TEST" 문장이 복사된다(not reference).
const string& f2 = foo(); // 다 적기 너무 귀찮아
decltype(foo()) f3 = foo(); // foo()를 두 번 적어야 해서 번거로움

decltype(auto) f4 = foo(); // 이렇게 하면 f4의 타입은 const string&를 그대로 유지한다.
~~~

---

# C++ As an Object-Orient Language

## Defining a Class
Instance를 만들 때 Stack에 만들 수도 있고, Heap에 만들 수도 있다!  
~~~c++
// Stack-based AirlineTicket
AirlineTicket myTicket; 
myTicket.setPassengerName("Sherman T. Socketwrench");
myTicket.setNumberOfMiles(700);
int cost = myTicket.calculatePriceInDollars();
cout << "This other ticket will cost $" << cost2 << endl;

// Heap-based AirlineTicket with Smart Pointer
auto myTicket = std::unique_ptr<AirlineTicket>();
myTicket2->setPassengerName("Laudimore M. Hallidue");
myTicket2->setNumberOfMiles(2000);
myTicket2->setHasEliteSuperRewardsStatus(true);
int cost2 = myTicket2->calculatePriceInDollars();
cout << "This other ticket will cost $" << cost2 << endl;
~~~

