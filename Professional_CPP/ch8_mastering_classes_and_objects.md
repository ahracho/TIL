# Profession C++ (by Marc Gregoire)

#### 블록체인 코어 개발 스터디 8주차 (5/25)

# Chapter 8 : Mastering Classes and Objects

## WHAT’S IN THIS CHAPTER?
- 객체의 동적 할당
- static, const, reference 멤버 변수와 메소드
- 메소드 오버로딩
- 연산자 오버로딩

---

# Dynamic Memory Allocation in Objects
## Freeing Memory with Destructors
동적으로 생성한 객체를 해제할 때는 소멸자에서 모두 delete 해주어야 한다. 

## Handling Copying and Assignment
동적으로 생성한 객체에는 포인터가 들어있기 때문에 이 값을 다른 변수에 할당하거나 복사를 하면 두 변수가 같은 메모리를 참조하게 되고 하나가 free 하면 나머지는 이미 해제된 메모리를 가리키게 되는 문제가 발생하게 된다. 따라서, **동적으로 생성된 객체에는 반드시 독자적인 소멸자, 복사 생성자, 할당 연산자를 정의해야 한다.** 복사 생성자에서는 단순히 포인터 값을 복사하는 것이 아니라 deep copy를 해야하고, 할당 연산자에서는 왼편에 있는 메모리를 먼저 해제하고 오른편에 있는 메모리 값을 deep copy하는 과정이 필요하다.    

# Different Kinds of Data Members
## static Data Members
클래스 전체가 바라보아야 하는 값은 static 변수로 선언해야 한다. C에서 글로벌 변수의 역할과 비슷하다고 보면 된다. static 멤버 변수의 경우에는 클래스 정의에도 포함되어야 하지만 소스 파일에도 선언해야 한다.  
static 멤버 변수는 생성자에서도 접근 가능하다. 객체와 상관없이 클래스 단위로 관리되는 값이기 때문에!

## const Data Members
const 변수는 초기화 이후에 값을 변경할 수 없다. 상수가 클래스 단위로 적용되는 값이라면 static const로 선언하면 된다. 

## Reference Data Members
여러 클래스가 상호 참조해야 하는 경우가 있는데 이 때는 #include으로 해결할 수 없다. 이 때 forward declaration을 사용하면 되는데 헤더파일 하나에 다른 클래스를 선언해주면 된다. 

~~~C++
class SpreadSheetApplication;
class SpreadSheet {
    public:
        SpreadSheet(int inWidth, int inHeight, SpreadSheetApplication& theApp);
    private:
        SpreadSheetApplication& mTheApp;
}
~~~

## const Reference Data Members
const Reference 변수를 사용하면 const 메소드에서만 사용할 수 있다. const 메소드는 멤버 변수 값을 안 바꾸는 메소드라는 의미이기 
때문에 const Reference 변수도 const 메소드에서만 호출할 수 있다. 

# More about Methods
## static Methods
static 변수와 같이 static 메소드도 정의할 수 있는데, static 메소드는 개별 객체와 상관없이, 즉 static이 아닌 멤버 변수 값을 참조하거나 수정하지 않는 메소드이다. 그렇기 때문에 static 메소드 안에서는 this 포인터도 사용할 수 없으며 non-static 멤버 변수도 참조하지 않는다.  

정리하자면, static 메소드에서는 1) static 멤버 변수 또는 2) non-static 멤버 변수의 reference나 포인터만 사용할 수 있다.  

## const Methods
const 메소드는 멤버 변수의 값을 바꾸지 않는 메소드이다. 객체에도 const를 붙일 수 있는데, const 객체는 const 메소드만 호출할 수 있다. 

## Method Overloading
메소드의 이름은 같지만 파라미터가 다른 여러 메소드를 정의하는 것을 메소드 Overloading이라고 한다. 이 때 주의할 점은 return 타입은 반드시 같아야 한다는 것이다. 

## Default Parameters
오버로딩과 비슷하게 쓰일 수 있는 것이 디폴트 파라미터이다. 파이썬에서처럼 파라미터에 디폴트 값을 설정해놓으면 호출 시에 해당 파라미터 값을 주지 않아도 에러가 나지 않는다. 주의할 점은 디폴트 값이 설정된 파라미터는 정의할 때 오른쪽 끝부터 정의해야 한다는 것이다.

## inline Methods
define 매크로를 사용하는 것처럼 inline 메소드를 정의하면 컴파일 때에 코드가 대체된다. 

~~~c++
inline double SpreadSheetCell::getValue() const {
    return mValue;
}
~~~

inline 메소드와 같은 동작을 하도록 헤더파일의 클래스 정의에 바로 메소드 내용을 정의할 수도 있다. inline 키워드를 사용하면 컴파일러가 상황에 따라서 짧은 코드를 사용하기 때문에 inline이 사용되지 않을 수도 있다. 

# Friends


# Operator Overloading
