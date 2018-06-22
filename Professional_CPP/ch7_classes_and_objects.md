# Profession C++ (by Marc Gregoire)

#### 블록체인 코어 개발 스터디 7주차 (5/18)

# Chapter 7 : Gaining Proficiency with Classes and Objects

## WHAT’S IN THIS CHAPTER?

---

# Object Life Cycles
객체의 생명 주기는 세가지로 구분된다 : 생성, 소멸, 값 할당. 

## Object Creation
객체는 선언하거나 new, new[]를 통해서 메모리를 할당할 때 생성된다. 객체가 생성될 때 안에 속해있는 객체들도 같이 생성된다. 

~~~c++
#include <string>
class MyClass {
    private :
        std::string mName;
};

int main() {
    MyClass obj;
    return 0;
}
~~~

MyClass 객체가 생성될 때 멤버 변수로 사용되는 string 객체도 같이 생성된다. 

멤버 변수의 초기값을 설정해주는 것이 필요할 때가 있는데 이 때 사용하는 것이 생성자(Constructor)이다.  

### Writing Constructors
생성자의 이름은 클래스의 이름과 동일해야 한다. 생성자는 리턴이 없고 파라미터가 있을 수도, 없을 수도 있다. 파라미터가 없는 생성자는 디폴트 생성자라고 부른다. 

~~~C++
// SpreadSheetCell.h
class SpreadSheetCell {
    public :
        SpreadSheetCell (double initialValue);
};  

// SpreadSheetCell.cpp
SpreadSheetCell::SpreadSheetCell(double initialValue) {
    setValue(initialValue)
}
~~~

### Using Constructors
생성자를 사용하면 객체가 생성됨과 동시에 멤버 변수 값들이 초기화 된다. 생성자는 선언될 때 불린다는 것을 기억해야 한다. 디폴트 생성자를 사용하는 경우가 아니라면, 선언할 때 초기값을 반드시 주어야 한다는 의미이다. 

~~~C++
// stack에 만들어졌을 때
SpreadSheetCell myCell(5), anotherCell(4);

// heap에 만들어졌을 때
auto smartCellp = make_unique<SpreadSheetCell>(4);
SpreadSheetCell* myCellp = new SpreadSheetCell(5);
~~~

### Providing Multiple Constructors
생성자를 하나 이상 설정할 수도 있는데, 모든 생성자는 당연히 같은 이름(클래스 이름)을 사용해야 한다. 여러 생성자가 있다면 컴파일러는 초기값의 타입을 보고 어떤 것을 호출할지 결정한다(Overloading). 

~~~C++
class SpreadSheetCell {
    public:
        SpreadSheetCell(double initialValue);
        SpreadSheetCell(const std::string& initialValue);
}
~~~

### Default Constructors
생성자가 따로 정의되어 있지 않다면, 컴파일러는 자동으로 디폴트 생성자를 실행한다. 파라미터는 따로 받지 않지만 생성자가 실행될 때 초기값을 설정하고 싶은 경우가 있을텐데 이런 경우에는 디폴트 생성자를 정의하고 생성자 내부에서 값을 할당하면 된다. 스택에서 디폴트 생성자를 사용할 때는 객체 생성 시에 () 없이 선언하면 된다. 

~~~c++
SpreadSheetCell::SpreadSheetCell() {
    mValue = 0;
}

SpreadSheetCell myCell(); // error
SpreadSheetCell myCell; // right
~~~

만약 디폴트 생성자가 아닌 다른 생성자를 정의하였다면 컴파일러는 디폴트 생성자를 만들지 않는다. 즉, 내가 정의한 생성자만 동작하게 된다. 그래서 필요한 경우 디폴트 생성자를 직접 클래스 정의 부분에 명시해주어야 한다.

~~~C++
// MyClass.h
class MyClass {
    public :
        MyClass();
        MyClass(int i);
};

// MyClass.cpp
MyClass::MyClass() {}
MyClass::MyClass(int i) {
    mValue = i;
}

// MyClass::MyClass() {} 대신 정의부분에 직접 defalut를 명시해줄 수 있다.
class MyClass {
    public :
        MyClass() = default;
        MyClass(int i);
};

// static method만 사용하여서 생성자가 필요없는 경우에는 아래와 같이 작성한다. 
class MyClass {
    public :
        MyClass() = delete;
};
~~~

### Constructor Initializers
초기값을 설정하는 방법에 Constructor Initialize라는 것이 있다. 이를 이용해서 디폴트 생성자를 다르게 작성할 수 있다. 
~~~c++
SpreadSheetCell::SpreadSheetCell() {
    mValue = 0;
}

SpreadSheetCell::SpreadSheetCell : mValue(0) {
}
~~~

두가지 방식은 다르게 동작한다. 1번의 경우에는 객체를 생성하고 생성자에서 멤버 변수의 값을 수정하는 것이라면, 2번의 경우는 생성과 동시에 값을 할당하는 것이다.  
C++에서 객체를 생성할 때는 생성자가 불리기 전에 안에 속해 있는 객체들이 먼저 생성되어야 한다. 멤버 변수에 객체들이 있다면 당연히 그들의 생성자들이 불릴 것이다. 이 때 만약 멤버 객체가 디폴트 생성자가 아닌, 초기값이 필요한 경우라면 1번의 경우에는 아직 SpreadSheetCell의 생성자가 호출되지 않았기 때문에 안에 있는 객체들이 어떤 값으로 초기화되어야 하는지 알 수 없다. 이런 경우에는 컴파일이 될 수 없기 때문에 2번의 경우를 반드시 사용해야 한다. 

그 외에도 const 멤버가 있는 경우 const는 값이 변경될 수 없기 때문에 1번의 경우를 사용할 수 없고, Reference 값도 마찬가지이다. 앞서 설명했던 것처럼 디폴트 생성자가 없는 Object가 멤버변수인 경우에도 1번의 경우를 사용할 수 없다.

**Constructor Initializer를 사용할 때 주의해야 할 점은, 헤더 파일에 정의되어 있는 변수들의 순서대로 초기값을 나열해야 한다는 것이다.**

### Copy Constructors
Copy Constructor라는 것이 있는데 이것은 객체와 같은 값을 가진 또다른 객체를 생성한다. 디폴트 생성자와 마찬가지로 정의되어 있지 않으면 컴파일러가 자동으로 생성하는데 보통 이것을 그대로 사용하는 것이 좋다. Copy Constructor가 사용되는 경우는 Call By Value인 함수에서 파라미터로 값을 넘기거나, 함수의 리턴값을 복사해야 하는 경우이다.  

### In-Class Member Initializers
C++11부터 멤버 변수 초기화를 클래스 정의에서 할 수 있다. 

~~~C++
class MyClass {
    private:
        int mInt = 1;
        std::string mStr = "Test";
};
~~~

### Delegating Constructors
생성자가 다른 생성자를 부를 수도 있는데, 이런 형태는 반드시 Constructor Initializer에서 사용되어야 한다.

~~~C++
SpreadSheetCell::SpreadSheetCell(const string& initialValue) : SpreadSheetCell(stringToDouble(initialValue)) {
}
~~~

## Object Destruction
스택에서 만들어진 객체는 스택이 소멸됨과 동시에 해제되지만, Heap에 만들어진 객체라면 반드시 delete를 해주어야 한다. 이런 번거로움을 피하려면 스마트 포인터를 사용해야 한다.  

## Assigning to Objects
C++에서는 한 객체의 값을 그대로 다른 객체 할당할 수 있다. 

~~~C++
SpreadSheetCell myCell(5), anotherCell;
anotherCell = myCell;
~~~

앞서 설명한 복사와 비슷하다고 생각할 수 있겠지만, 복사는 생성될 때에만 되는 것이고 생성 이후에는 값의 할당이라고 부르는 것이 올바르다. 객체에서 값을 할당할 때는 할당 연산자를 부르는데 = 연산자를 클래스를 위해서 override하는 모양새다. 할당 연산자는 자동으로 정의되기 때문에 필요한 경우가 아니라면 따로 정의할 필요는 없다. 