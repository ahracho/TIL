# Profession C++ (by Marc Gregoire)

#### 블록체인 코어 개발 스터디 2주차 (4/13)


# Chapter 2 : Working with Strings

## WHAT’S IN THIS CHAPTER?
- C 스타일 문자열과 C++ 스타일 문자열의 차이를 알아본다.
- std::string 클래스를 자세히 들여다본다.
- Raw String Literals에 대해 알아본다.

---

# Dynamic Strings
## C-Style Strings
C에서 string은 단순히 character 배열이다. 마지막 문자는 반드시 \0(NUL)으로 해야 문자열의 끝을 나타낼 수 있다. C++ 프로그램에서도 외부 라이브러리에서 C 스타일 문자열을 사용하는 경우가 있기 때문에 알아두는 것이 좋다. <cstring> 헤더에 C 스타일 문자열 연산이 정의되어 있다. 

**메모리 할당할 때 반드시 (strlen + 1) 만큼 해야 한다는 것!**  

## String Literals
변수가 아니라 그냥 문자열 자체로 사용된 것을 String Literal이라고 한다 (written as a value, not a variable). String Literal은 RO 메모리 영역에 할당된다. C++ 표준에서는 string literal을 'array of n const char *'라고 정의하고 있지만 backward compatibility 때문에 const 없이 char *로 취급하기도 한다. 보통은 문제가 없지만 String Literal 값을 바꾸려 하는 동작은 정의가 되어 있지 않기 때문에 컴파일러에 따라서 다르게 동작할 수가 있으니(crash/side effect이 나거나 warning을 띄우거나, 아니면 정상 동작할 수도 있다) 주의해야 한다. String Literal을 변수에 할당할 때는 const를 쓰는 게 가장 좋다.  

## The C++ String Class
std::string class는 <cstring> 헤더에 있는 기능을 거의 지원하지만 메모리 할당에 대한 관리를 더 잘해준다. 

### Using the string Class
string이 클래스이긴 하지만 int 같은 built-in type이라고 생각해도 된다. 연산자 오버로딩 덕분에 C 스타일 string보다 훨씬 쉽게 사용할 수 있다.  +, +=, ==, !=, < 등의 연산자를 모두 사용할 수 있다.  

~~~c++
string myString = "hello";
myString += ", there";
string myOtherString = myString;
if (myString == myOtherString) {
    myOtherString[0] = 'H';
}
cout << myString << endl;
cout << myOtherString << endl;
~~~
위의 코드에서 보듯이, 문장이 길어질 때마다 메모리 관리는 string class에서 알아서 다 해주기 때문에 memory overrun에 대해서 걱정할 필요가 없다.  

# Raw String Literals
일반 string에서는 escape sequence를 사용하거나 따옴표를 사용할 때 항상 \를 붙여줬어야 했는데, Raw String Literal에서는 그냥 사용할 수 있다. R"( )" 괄호 사이에 문장을 작성하면 된다. Raw string literal은 여러 줄에 걸쳐 사용할 수 있다. 대신 \t \n과 같은 escape sequence는 문자 그대로 사용된다는 점을 주의하자. 

~~~c++
string str = "Hello \"World\"!";
string str = R"(Hello "World"!)";
~~~

여기서 )"는 Raw String Literals를 나타내기 위해서 사용되었기 때문에 작성할 문장 사이에 이게 들어가면 안된다. )"를 사용해야 한다면 extended raw string literal syntax를 사용해야 하는데, 방법은 아래와 같다.

~~~c++
// R"d-char-sequence(r-char-sequence)d-char-sequence"
// 작성하고자 하는 문장을 () 안에 적고 괄호 앞 뒤로 같은 문자열(최대 16 char)을 적어준다.
string str = R"-(The characters )" are embedded in this string)-";
~~~

# Nonstandard Strings
개발 프레임워크나 운영 체제에 따라서 다른 방식으로 string을 취급하기 때문에(CString 클래스나 MS의 MFC 등) 보통의 C++ 개발자들은 C++ 스타일 string을 사용하지 않는다. 개발을 시작하기 전에 팀 내에서 어떻게 사용할지 합의를 보고 시작하는 것이 중요하다.   