# 코딩야학 2일차 : 인터넷/웹의 개념, 서버-클라이언트

## 인터넷과 웹의 역사
### 인터넷과 웹은 다르다!
인터넷이 웹보다 훨씬 큰 범위. 인터넷이 OS라면, 웹은 어플리케이션. 인터넷이 도시면, 웹은 집 한 채. 파일을 주고 받는 FTP, 이메일 등이 웹과 동급으로 이해할 수 있음. 웹은 인터넷에서 사용할 수 있는 수많은 기술 중 가장 유명한 기술 중 하나임.

- 1960년대 : 인터넷의 등장 - 전세계의 컴퓨터가 연결되어 데이터를 주고받을 수 있도록 한 가장 큰 네트워크  
- 1990년대 : 웹의 등장 - 이 네트워크, 즉 인터넷을 활용해서 HTML 형태로 작성된 문서(혹은 프로그램)를 주고받아 웹페이지를 표현할 수 있도록 한 기술 (팀버너스리)  

웹브라우저와 그 반대편에 웹서버라는 SW를 개발. 웹브라우저와 웹서버가 통신을 하면서 정보를 주고받게 되는데, 이 통신 규약이 HTTP이고 그 위로 돌아다니는 데이터의 형태가 HTML인 것!  
__웹을 제대로 배우려면 웹브라우저와 웹서버의 관계, HTML 언어에 대한 이해가 필수적__

## 서버와 클라이언트
### 서버와 클라이언트의 의미
서버용으로 사용되는 컴퓨터도 일반적인 컴퓨터와 동작하는 매커니즘의 거의 유사함. 즉, 어떤 컴퓨터라도 서버나 클라이언트가 될 수 있다는 얘기. 그렇다면 웹을 생각할 때, 2대의 컴퓨터 중에 누가 서버이고 누가 클라이언트인지 구분할 것인가. __웹브라우저가 설치되어 있는 컴퓨터가 클라이언트, 웹서버가 설치되어 있는 컴퓨터가 서버 역할을 하는 것__  

1. 웹브라우저에 주소를 치면, 웹브라우저는 주소에 해당하는 웹서버에 웹페이지를 요청  
2. 웹서버는 요청을 받아 서버에 저장되어 있는 해당 웹페이지 문서(HTML)을 읽어서 클라이언트에 돌려줌(응답)  

즉, __요청하는 쪽이 클라이언트, 요청을 받아 응답하는 쪽이 클라이언트__  

### 웹서버 준비하기
웹 공부를 하려면 웹클라이언트와 웹서버를 모두 준비해야 하는데, 그럼 PC 2개를 준비해야 하나? 한 대의 컴퓨터에 웹브라우저와 웹서버를 모두 설치하면 됨. 즉, 웹브라우저가 요청할 때 해당 컴퓨터에 요청을 전달하도록 하면 동작하겠지!

웹서버의 종류: __아파치(1등)__, NginX(오픈소스), IIS (MS)

아파치를 설치하여 사용할 테지만, 서버용 프로그램은 일반인들이 설치하기 굉장히 복잡해서 이를 쉽게 설치해줄 수 있는 보조 프로그램을 사용할 것!  

### 웹서버 동작 방식
웹브라우저에 localhost/index.html라고 치면, localhost는 웹브라우저가 설치되어 있는 컴퓨터를 가리키고, 해당 컴퓨터에 웹서버도 설치되어 있기 때문에 결국 웹서버를 가리키는 것. 브라우저는 웹서버에게 index.html 파일을 요청한 것. 웹서버는 약속된 폴더(htdocs - document root 폴더)에 있는 해당 파일을 브라우저에게 돌려줌.

브라우저에서 폴더에 없는 파일 이름을 요청하면 Page Not Found 에러가 보이겠지?

## Bitnami 사용하여 서버제어
MySQL DB, Apache Web Server  둘 다 실행 중이어야 함. 