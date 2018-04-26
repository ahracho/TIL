# Profession C++ (by Marc Gregoire)

#### 블록체인 코어 개발 스터디 3주차 (4/20)


# Chapter 2 : Coding with Style

## WHAT’S IN THIS CHAPTER?
- 코드 문서화의 중요성과 주석 스타일에 대해 알아본다.
- Decomposition에 대해 알아본다.
- Naming Convention과 Formatting Rule에 대해 살펴본다.

---

# The Importance of Looking Good
## Elements of Good Style
- Documentation
- Decomposition
- Naming
- Use of the Language
- Formatting

# Documenting Your Code
프로그래밍에서 문서화라고 하는 것은 꼭 워드 파일로 문서화하는 것 뿐만 아니라, 코드 사이에 코멘트를 넣는 것을 가리킨다. 코멘트로 구현하고자 했던 기능과 어떤 식으로 접근했는지, 혹은 작성할 때 명확하지 않았던 부분, 수정해야 하는 부분 등을 적어둘 수 있다.  

## Reasons to Write Comments
### Commenting to Explain Usage
헤더 파일에 선언되어 있는 함수나 메소드는 누구나 접근하여 사용할 수 있기 때문에, 어떻게 호출해야 하는지에 대한 설명이 필요하다.  

코드 자체에서는 설명할 수 없는 것들, 예를 들어, 해당 함수는 반드시 A 함수를 호출하고 난 다음에 호출해야 한다든지, 어떤 형태의 데이터는 사용할 수 없다든지 등의 내용이 들어갈 수 있다. 또한, 코드에 대한 부가적인 설명이 추가될 수 있는데, 예를 들어, 파라미터/리턴 타입 자체는 함수를 보면 바로 알 수 있지만, 파라미터로 어떤 값을 주어야 하는지, 리턴된 값이 어떤 의미인지 등 추가적으로 사용자가 알아야 하는 내용을 적어둘 수 있다. 

~~~C++
/*
* func()
*
* Description of the function.
*
* Parameters:
* int param1: parameter 1.
* Returns: int
* An integer representing...
* Throws:
* Exception1 if...
* Notes:
* Additional notes...
*/
~~~

### Commenting to Explain Complicated Code
한 눈에 봐서 모르는 복잡한 알고리즘을 사용한 코드의 경우, 작성한 사람은 이해하지만(그마저도 시간이 좀 지나면 잊으니까) 다른 사람이 이해하려면 시간과 노력이 많이 들기 때문에 적절한 코멘트는 필수다.  

보통 코드 상단에 high-level의 개요를 적고, 코드 중간에는 해당 라인이 어떤 의미인지 설명을 적는다.  

다만 조직마다 코멘트 적는 방식도 다르기 때문에 상황에 맞게 적절하게 적도록 한다.  

### Commenting to Convey Meta-information
코드 자체에 대한 코멘트가 아니라 메타정보를 적기 위해서도 코멘트를 사용한다. 작성자, 작성일, 기능, 변경로그 등의 정보를 담는다. 버그 번호나 TODO 등도 여기에 속한다.  

코드 관리 프로그램을 사용하면 너무 상세한 정보는 프로그램에서 제공해주기 때문에 안 적어도 된다. 이 역시 상황에 맞게 적절하게 사용하도록 한다. 

## Commenting Styles
### Commenting Every Line
작성한 코드 한줄한줄마다 설명을 적으면 각 라인이 꼭 필요한 코드인지 다시 한번 확인할 수 있어서 좋지만 덩치가 큰 프로그램의 경우엔 이렇게 적는 게 오버헤드가 되거나 더 지저분해질 수가 있다.  

간단한 코드에 이렇게 설명을 적어놓는 것은 한 눈에 봐도 이해가 되는 코드에 추가적인 정보 없이 불필요한 설명을 덧붙이는 꼴이기 때문에 좋지 않지만, 복잡한 코드에는 유용할 수 있다.  

### Prefix Comments
소스 파일의 최상단에 필요한 정보를 적어둘 수 있다. 보통 적어놓는 내용으로는 
- 최종 수정일
- 작성자
- 수정 로그
- Feature ID
- 저작권 / 라이센스 관련 정보
- 간단한 설명
- 미구현 사항
- Known Bugs

### Fixed-Format Comments 
정해진 포맷으로 적힌 코멘트를 파일빌더로 빌드하는 방법도 있는데, Java에서는 JavaDoc이라는 툴을 사용하고, C/C++에서는 Doxygen을 사용해서 HTML 파일로 만든다.


**읽기 편하고 이해하기 쉬운 코드가 가장 좋은 코드이다. 만약 코드에 설명을 많이 적고 있다면 코드에 개선할 점은 없는지 확인해보는 게 좋다.**  

# Decomposition
Decomposition은 코드를 작은 단위로 쪼개는 걸 가리킨다. 이상적으로 하나의 함수나 메소드는 단일 작업을 수행해야 한다.  

## Decomposition through Refactoring
사용할 수 있는 리팩토링 기법의 예 (리팩토링만 다시 한번 정리할 예정)
1. Abstraction
- Encapsulate Field : 변수를 private으로 만들고 getter/setter로 접근
- Generalize Type : general type을 만들어서 공통으로 많이 사용할 수 있도록 한다.
2. Breaking code apart into more logical pieces
- Extract Method : 큰 method에서 작은 부분을 뽑아내서 작게 만든다.
- Extract Class : 클래스의 부분을 쪼개서 작은 클래스로 만든다.
3. Improving names and the location of code
- Move Method / Field
- Rename Method / Field
- Pull up : 코드를 base class로 이동
- Push down : 코드를 하위 클래스로 이동

## Decomposition by Design
코드를 짤 때부터 큰 그림을 그리고 시작하면 덜 엉망이 될 것(코드가 망가지는 건 피할 수 없다)


# Naming
컴파일러 자체에서 거르는 Naming Rule
- 함수/변수는 숫자로 시작할 수 없다. 
- double underscore(__)가 포함되면 안된다.

## Choosing a Good Name
가장 좋은 이름은 변수/함수/클래스의 목적을 잘 드러내는 이름이다. 이 것도 이렇게 해야한다 딱 정해진 룰이 있는 건 아니지만, 보통 많이 쓰는 룰이 있다. 

안 좋은 사례
- Too general
- Too long
- Too onscure/concise
- Unacceptable inside joke
- Non-descriptive Name
- Abbreviations

반대로 말하면 간결하면서도 필요한 정보를 담고 있는 이름이 좋은 이름이라는 것.

## Naming Conventions
### Counters
for loop 돌 때 i나 j를 많이 쓰는데, 헛갈려서 잘못 쓴 경험들 많이 있을 것이다. 이럴 때는 대신 outerLoopIndex, innerLoopIndex 이렇게 쓰는 게 귀찮지만 더 좋을 수 있다.

### Prefixes
변수 이름을 데이터 타입을 나타내는 글자로 시작하는 경우도 있고, prefix를 쓰면 코드 수정이 용이하지 않아서 선호하지 않는 경우도 있다 (변수 타입이 바뀌게 되면 변수 이름도 다 바꿔줘야 하는 경우도 있을 수 있고 등등).

# Using Language Features with Style
## Use Constants
상수를 써야할 때 무작정 하드코딩 해놓으면 나중에 봤을 때 어떤 값을 표현한 건지 기억이 안 나거나 다른 사람이 봤을 때 명확하지 않기 때문에 하드코딩 대신 constant 변수로 만들어서 이름을 붙이자.  
~~~C++
const double kApproximationForE = 2.71828182845904523536;
~~~

## Use References Instead of Pointers
기존 C에서 포인터로 해야했던 작업의 대부분을 레퍼런스로 대체할 수 있다. 레퍼런스를 사용할 때의 장점은
- 더 안전하다 : 메모리 주소를 직접 건드리지 않고, nullptr을 넣을 수 없다.  
- 포인터보다 보기 편하다 : 변수처럼 사용하지만 포인터의 기능을 가진 레퍼런스!
- 쓰기 편하다
- 메모리 관리를 누가 해야하는지 명확히 할 수 있다 : 레퍼런스를 넘기면 읽기/쓰기를 할 수 있지만 메모리를 해제하는 것은 불가능하다. 포인터를 생성한 곳에서 해제도 해야한다는 것

## Use Custom Exceptions
Exception을 쓰면 훨씬 더 풍부한 Error Handling 메커니즘을 사용할 수 있다.


# Formatting
포맷과 관련한 난제 --> 팀에서 규칙을 정해야
1. The Curly Brace Alignment Debate : {} 어떻게 쓸래
> **NOTE When selecting a style for denoting blocks of code, the important consideration is how well you can see which block falls under which condition simply by looking at the code.**
2. Coming to Blows over Spaces and Parentheses : (), {} 띄어쓰기
3. Spaces and Tabs 

- 구글 C++ 컨벤션 찾아보기
- AStyle Formatter
- Doxygen 만드는 법 실습해보기