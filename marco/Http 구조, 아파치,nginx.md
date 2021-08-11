# 1일차

## 웹 서버

### Http Request 구조

![Untitled](https://user-images.githubusercontent.com/73640185/128987028-ba7d2f38-511f-49b8-807e-cde77b936c02.png)

Request Line : 메소드 + URL + HTTP 버전(GET/app/test/list HTTP/1.1)

Header : 일반정보(요청과 응답에 모두 사용되는 정보),요청정보(요청할때만 전달되는 정보),엔티티 정보(POST 요청일때만 사용되는 정보)가 들어 있다.  (Host:localhost:8080 등 헤더명 : 값\n으로 이루어져있다.)

**Host** : 요청하려는 서버 호스트 이름과 포트번호

**User-agent** : 클라이언트 프로그램 정보. 이 정보를 통해 서버는 클라이언트 프로그램(브라우저)에 맞는 최적의 데이터를 보내줄 수 있다.

**Referer** : 바로 직전에 머물렀던 웹 링크 주소

**Accept** : 클라이언트가 처리 가능한 미디어 타입 종류 나열

**If-Modified-Since** : 여기에 쓰여진 시간 이후로 변경된 리소스 취득. 페이지가 수정되었으면 최신 페이지로 교체한다.

**Authorization** : 인증 토큰을 서버로 보낼 때 쓰이는 Header

**Origin** : 서버로 Post 요청을 보낼 때 요청이 어느 주소에 시작되었는지 나타내는 값. 이 값으로 요청을 보낸 주소와 받는 주소가 다르면 CORS(Cross-Origin Resource Sharing) 에러가 발생한다.

**Cookie** : 쿠키 값이 key-value로 표현된다.

body : POST일때 사용

### Http Response 구조

![Untitled 1](https://user-images.githubusercontent.com/73640185/128986999-044c8240-b6e8-421c-bb4d-b98ccd980131.png)

Status Line : HTTP 버전 + Status Code + Status text

Header : HTTP 요청 헤더와 동일 단 User -Agent 대신 Server헤더 사용

body : body

### Thread.start() 와 run()의 차이

start는 쓰레드를 생성하고 그 스택 안에 run()을 담는다.

run은 그냥 우리가 쓰는 메소드 호출

### byte[]로 직렬화를 수행하는 이유

직렬화 : 객체의 상태 및 데이터 구조를 기록할 수 있는 포맷(파일,버퍼 등)으로 변환

프로그램 마다 문자열이나 파일을 인코딩 하는 방식이 다르다. 따라서 byte[]로 직렬화를 해서 보내야 정확한 정보를 받고 보낼 수 있다.

### 파비콘

웹 페이지에 접속 했을 때 상단 탭에 보여지는 아이콘

### 아파치

![Untitled 2](https://user-images.githubusercontent.com/73640185/128987014-14929742-d534-449d-8081-87de6481a9a4.png)

왼쪽 : prefork 오른쪽 : worker

웹 서버(정적 페이지를 반환) 의 하나의 종류이다.

- prefork 방식 : 각 요청을 프로세스로 받아 처리한다.  각 요청이 독립 프로세스로 진행 되기 때문에 다른 요청에 오류가 생겨도 서로 영향을 받지 않는다. 하지만 시스템 메모리, CPUI 리소스 에 부하를 준다.
- worker 방식 : 각 요청을 쓰레드로 받아 처리 한다. 쓰레드를 사용하기 때문에 프로세스 별 쓰레드 개수 제한을 넘기면 프로세스를 생성하여 처리한다. 쓰레드를 사용하기 때문에 서로 영향을 받기가 쉽다. 하지만 리소스 부하가 적다.
- event 방식 : nginx를 따라 한 방식 , 연결을 계속 물고 있다가 요청이 들어오면 처리한다.

### nginx

![Untitled 3](https://user-images.githubusercontent.com/73640185/128987025-5b6d421f-7652-42d9-8e65-d90f03371c3f.png)

Event Driven 방식으로 처리하는 웹 서버

싱글 프로세스/쓰레드 방식으로 오버헤드가 발생하지 않아 빠른 처리가 가능하다.

하지만 I/O 처리가 큰 작업의 경우가 많을 경우 성능 저하가 발생한다.

복잡한 처리나 대용량 데이터 처리가 피룡한 서비스 에서는 적합하지 않을 수 있다.
