## 1. HTTP

HTTP는 Hypertext Transfer Protocol로, 서로 다른 시스템 사이에서 데이터를 주고받을 때 사용하는 '규칙'이다.

> Protocol? 두 사람이 대화를 할 때는 말이 필요하고, 말은 여러 문법이 있다. 네트워크에서는 말을 '네트워크 아키텍쳐'라 하고, 문법은 '프로토콜'이라 한다.

보통 HTTP를 통해 전송하는 데이터는 HTML, 이미지, 파일 등등이 있다.

클라이언트가 무언가를 달라고 *요청*할 때는 Request, 서버가 무언가를 줌으로 *응답*하는 것을 Response라 한다.

### 1-1. HTTP의 구조

HTTP는 크게 *HTTP Header*와 *Entity Body*로 이루어져 있다.

#### HTTP Header

HTTP Header는 3부분으로 이루어져 있다.<br>
1. Request Line / Response Line
```
HTTP Method/Request target/HTTP version
```
Header가 시작되는 부분으로 위와 같은 형태로 담겨있다.<br>
HTTP Method의 경우 해당 요청이 어떤 요청인지 알려준다.<br>
GET, POST, OPTIONS, PUT, DELETE 가 있는데, GET은 데이터를 서버로부터 받아올 때 사용하고 POST는 데이터를 생성, 수정할 때 많이 사용한다.

2. Message Header

Message Header는 웹브라우저의 종류나 버전, body의 길이 등이 Key:Value 형태로 적혀있다.

3. Blank Line

이부분은 말 그대로 공백인 줄로, Header와 Body를 구분하는데 사용된다.

#### Entity Body

몸통부분에는 응답으로 돌아올 때 데이터가 담겨서 돌아오거나, POST 메소드를 이용하여 요청 시 파라미터를 담아서 요청한다.
