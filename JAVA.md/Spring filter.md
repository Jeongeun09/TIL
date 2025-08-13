Spring filter
====

Spring Filter
 

spring은 요청을 받았을 때 Dispatcher Servlet을 통해 Controller에 도달하게 된다.

Dispatcher Servlet에 요청이 가기 전 필요한 요청인 지 아닌 지 구분하는 역할을 하는 것이 Spring filter이다.

Spring filter는 요청이 불필요한 것인 지 필요한 것인 지 구별하기 때문에 요청을 확인하고 분석한다.

또한 Spring filter는 Dispatcher Servlet로 Controller에 도달하기 전에 사용되기 때문에 불필요한 로직 처리를 하지 않게 할 수 있다는 장점이 있다.

Spring filter에는 대표적으로 세 가지의 메서드들이 있다.

- init
- doFilter
- destroy


--- 

1. init
  필터를 초기화하는 역할을 맡고 있고 그렇기 때문에 spring이 실행될 때 처음으로 한 번만 실행한다.

 
2. doFilter
init은 필터에 요청이 가기 전 단계였다면 doFilter는 실제로 필터를 실행하는 단계라고 할 수 있다.

spring filter가 하는 역할 중 많은 부분이 doFilter에서 실행되고 요청과 응답을 중간에 가져와 로직을 실행할 수 있게 한다.

또한 다중 필터 방식일 때에는 필터를 여러 개 걸쳐 Dispatcher Servlet에 도달하게 된다.

이때 요청을 Dispatcher Servlet에 넘길 때 chain을 사용한다.

 
→ chain이란?

말 그대로 체인처럼 서로 이어져 있다는 의미인데 Dispatcher Servlet에 요청을 넘길 때 사용되고

chain.doFilter(request, response)를 호출해주면 다중 필터일 시에는 다음 필터로 이동하게 되고 다중 필터 형식이 아닐 시에는 Dispatcher Servlet으로 이동하고 제어하는 역할을 한다.

3. destroy
요청이 종료될 때 불러오는 메서드이다. 그러기 때문에 종료될 때 한 번만 실행하는 특징이 있다.

spring의 서버가 종료되거나 필터가 종료될 때 주로 사용한다. 항상 필수로 구현하는 것은 아니다.

하지만 자원을 명시적으로 닫아야할 때에는 구현해야한다. 또한 서버가 종료될 때 실행되다 보니 리소스를 정리하는 역할을 한다.

여기서 자원을 명시적으로 닫아야한다는 것은 자원의 의미부터 알아야 한다.

여기서 말하는 자원이란 DB 연결 또는 캐시 같은 것들을 말하는데 이것들을 destroy를 호출하지 않는다면 리소스들이 종료되지 않고 메모리에 그대로 남게 된다. 그러면 메모리가 의미없이 소요되게 되고 리소스 누수가 발생하게 되는 것이다.


한 마디로 destroy를 호출하는 이유는 리소스의 누수를 막기 위함이다.
-
 

Interceptor란?
Dispatcher Servlet이 Controller에 요청을 위임하기 전과 후에 끼어들어 요청과 응답을 변경, 수정하는 기능을 한다.

 

필터와 하는 일은 비슷하지만 필터는 웹 컨테이너, 인터셉터는 스프링 컨테이너에서 실행되는 차이점이 있다. 

 

인터셉터의 메서드 또한 3가지가 있다. 

 
1. preHandle

→ Controller가 실행되기 전 호출된다. 주로 컨트롤러 이전에 실행되야 하는 동작들을 수행한다.

2. postHandle

→ Controller 이후에 처리될 작업들이 있으면 실행된다. 하지만 요즘엔 REST API의 @RestController가 생겨났기 때문에 잘 쓰이지 않는다.

잘 사용하지 않는 이유?

→ postHandle은 ModelAndView를 나타내는데 이것은 예전 고전 방식이다. 왜냐하면 옛날에는 HTML 코드를 직접 렌더링해서 표현했기 때문에 데이터와 그것을 렌더링할 템플릿이 필요했는데 요즘엔 프론트가 화면을 제작하고 백엔드가 JSON 형태로 데이터를 보내는 형식이기 때문이다.


3. afterCompletion

→ 모든 작업이 완료된 이후 실행된다. 요청을 처리하는 과정에서 사용했던 리소스들을 반환하는 역할을 한다.

