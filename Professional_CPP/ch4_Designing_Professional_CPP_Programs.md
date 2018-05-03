# Profession C++ (by Marc Gregoire)

#### 블록체인 코어 개발 스터디 4주차 (4/27)


# Chapter 4 : Designing Professional C++ Programs

## WHAT’S IN THIS CHAPTER?
- 프로그래밍 디자인이 무엇이고 왜 중요한지 알아본다.
- C++ 만의 독특한 디자인 요소가 있는지 살펴본다.
- C++ 디자인에서 중요한 요소인 추상화와 재사용에 대해 살펴본다.
- 코드 재사용를 위한 다양한 기법과 코드 재사용이 장단점을 알아본다.

---

# What is Programming Design?
프로그램 디자인/소프트웨어 디자인이라는 것은 구현하고자 하는 프로그램이 여러 요구사항들을 만족하기 위해서 세부사항을 어떻게 설계할 것인지에 대한 것이다.  

보통 디자인 문서에는 다음과 같은 두가지 내용이 포함되어야 한다.
1. 여러 하위 시스템들의 전체적인 그림 : 인터페이스, 각 하위 시스템들의 dependency, 데이터 흐름, 입출력, thread 모델 등이 어떻게 되는지
2. 각 하위 시스템의 세부사항 : 하위 시스템 별로 클래스 구조, 데이터 구조, 알고리즘, 에러 처리 등

# The Importance of Programming Design?

# Designing for C++
# Two Rules for C++ Design
## Abstraction
TV가 어떻게 신호를 수신하고 화면에 출력하는지 원리를 알지 못해도 어렵지 않게 사용할 수 있듯이, 추상화란 내부의 구현과 외부와의 인터페이스를 구분하여 프로그램을 작성하는 것을 뜻한다. 

### Benefiting From Abstraction
추상화를 잘 하면 구현과 인터페이스가 명확히 구분되어 있기 때문에, 기저의 구현이 바뀌어도 사용하는 입장에서는 예전과 똑같이 사용할 수 있게 된다.

### Incorporating Abstration in Your Design
함수와 클래스를 구현할 때 사용하는 사람이 해당 기능이 어떻게 구현되어 있는지 파악하지 않아도 사용할 수 있도록 구현해야 한다. 

## Reuse
### Writing Reusable Code
특정 상황에서만 사용할 수 있는 자세한 코드를 작성하는 것은 지양해야 한다. C++에서 재사용 가능한 코드를 작성하는 방법 중 하나는 템플릿을 사용하는 것이다. 

~~~C++
class ChessBoard
{
    public:
        // This example omits constructors, destructors, and assignment operator.
        void setPieceAt(ChessPiece* piece, int x, int y);
        ChessPiece& getPieceAt(int x, int y);
        bool isEmpty(int x, int y) const;
    private:
    // This example omits data members.
};

// specific한 ChessPiece를 정의하여 사용하는 대신 PieceType이라는 템플릿을 정의하여 타입을 바꿀 수 있도록 유연하게 정의한다.
template <typename PieceType>
class GameBoard
{
    public:
        // This example omits constructors, destructors, and assignment operator.
        void setPieceAt(PieceType* piece, int x, int y);
        PieceType& getPieceAt(int x, int y);
        bool isEmpty(int x, int y) const;
    private:
    // This example omits data members.
};
~~~

# Reusing Code
## Deciding Whether or Not to Reuse Code
### Advantages to Reusing Code
- 개발 시간 단축
- 디자인이 간결해진다.
- 디버깅 할 필요가 줄어든다.
- 라이브러리가 에러 처리를 더 잘 해놓았다.
- 내가 짠 코드보다 훨씬 안정적이다.
- 라이브러리 코드는 계속 개선된다.

### Disadvantages to Reusing Code
- 사용법을 알기 위해서 어느 정도 시간을 투자해야 한다.
- 내가 원하는 기능에 정확하게 맞지 않을 수 있다.
- 원하는 성능이 안 나올 수 있다.
- 버그 수정이 쉽지 않다.
- 지원이 중단될 수도 있다.
- Cross Platform에 문제가 될 수 있다. 
- 호환성 문제가 있을 수 있다.


## Strategies for Reusing Code
### Understand the Capabilities and Limitations
라이브러리/프레임워크 사용하기 전에 검토해야 할 사항
- Multithread 지원 여부
- Dependency 체크
- Initialization / Cleanup 관련해서 해 주어야 할 게 있는지
- Class인 경우 생성자/소멸자 처리, Override
- Error 처리 방법 등

## Bundling Third-Party Applications
- Platform / Version 종속성
- **라이센스, 적법성 체크!!**


