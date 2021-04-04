## API? Application Programming Interface

***운영체제나 시스템, 애플리케이션, 라이브러리 등을 활용해 응용 프로그램을 작성할 수 있게 하는 다양한 인터페이스를 의미합니다. Window API, Java API, HTML5 API, Android API 등이 있습니다.*** - [API의 기본 by Naver Developers](https://developers.naver.com/docs/common/openapiguide/apiterms.md#api%EC%9D%98-%EA%B8%B0%EB%B3%B8)

Interface의 뜻을 검색하면 두 물체, 공간 등의 접점면 또는 상호작용이나 통신이 일어날 때 사용하는 수단 등이라고 나온다.<br>
API는 위의 말처럼 어떤 응용 프로그램을 작성하는데 사용하는 수단으로, 우리가 프로그램을 작성할 때 제공되는 함수들도 API이다.<br>
API를 어떻게 사용하는지는 API문서를 보고 서식을 따라 작성하면 되는데 평소 사용하는 [Java docs](https://docs.oracle.com/en/java/javase/16/docs/api/index.html) 또한 API 문서이다. 그리고 우리는 해당 문서를 보고 어떻게 작성해야 하는지 확인하고 API를 사용하는 것이다.

API를 사용하면 내부적으로 어떻게 작동하는지 알 필요 없이 API에서 설명하는대로 사용하면 된다.


## REST API? REpresentation State Transfer Application Programming Interface

REST API는 HTTP 통신에서 자원에 접근하여 CRUD를 할 때 URI와 메소드를 이용하여 주고받는 것을 말한다.<br>
그래서 응답하는 쪽이 REST API를 제공해주면, 요청하는 쪽에서는 사용법을 확인하고 응답하는 쪽이 하라고 했던대로 HTTP 요청을 하면 된다. 그러면 응답하는 쪽에서는 내부에서 일을 처리하여 다시 응답을 해준다.

이렇게 하면 요청하는 쪽은 응답하는 쪽이 정확히 어떻게 작동하는지 알지 못해도 요청을 할 수 있고, HTTP 통신으로 하기 때문에 통신만 가능하다면 REST API를 통해 내가 원하는 작업을 할 수 있다.

[네이버](https://developers.naver.com/main/), [카카오](https://developers.kakao.com/), [구글](https://developers.google.com/) 등에서 개발자를 위해 제공하는 기능들을 보면 대부분 REST API를 통해 사용한다.

### REEST의 구조

REST는
- 자원 : URI
- 행위 : HTTP Method
- 표현
으로 이루어져 있다.

URI로 자원을 표시하고 HTTP Method로 작엽을 요청, 그 응답을 받는 것이다.



-------

참고
- [RedHat](https://www.redhat.com/ko/topics/api/what-are-application-programming-interfaces)
- [API의 기본 by Naver Developers](https://developers.naver.com/docs/common/openapiguide/apiterms.md#api%EC%9D%98-%EA%B8%B0%EB%B3%B8)
