#### 해당 포스트는 HTTP 완벽 가이드 책을 보고 정리한 내용 입니다.

### 01. HTTP 개관

### 1.1 HTTP: 인터넷의 멀티미디어 배달부

- JPEG 이미지, HTML 페이지, 텍스트 파일, MPEG 동영상, WAV 음성 파일, 자바 애플릿 등 **다양한 리소스들이 인터넷을 통해 전달**된다.
- HTTP는 신뢰성 있는 데이터 전송 프로토콜을 사용하기 때문에, **데이터가 지구 반대편**에서 오더라도 **전송 중 손상되거나 꼬이지 않음을 보장** 한다.

### 1.2 웹 클라이언트와 서버

- HTTP 클라이언트: 서버에 **HTTP 요청을 보내는 곳**
- HTTP 서버: 요청된 데이터를 **HTTP 응답으로 돌려주는 곳**
- <img src="https://velog.velcdn.com/images/mocha/post/4078658a-18ab-4409-9183-4d5eb9f396a7/image.jpg" alt="웹 클라이언트와 웹 서버" width="600" height="300">


### 1.3 리소스

- 웹 서버는 웹 리소스를 관리하고 제공
- 웹 리소스의 종류
- 가장 간단한 웹 리소스는 웹 서버 파일 시스템의 **정적 파일**이다.
- **동적 컨텐츠 리소스**는 사용자가 누구인지, 어떤 정보를 요청했는지, 몇 시인지에 따라 다른 콘텐츠를 생성한다.
- <img src="https://velog.velcdn.com/images/mocha/post/78e43752-dd1f-4f0f-b62f-611886c65524/image.jpg" alt="웹 리소스" width="600" height="800">

- **미디어 타입**
- 인터넷은 수천 가지 데이터 타입을 다루기 때문에, **HTTP는 웹에서 전송되는 객체** 각각에 신중하게 **MIME(Multipurpose Internet Mail Extensions, 다목적 인터넷 메일 확장) 타입**이라는 데이터 포맷 라벨을 붙여서 사용한다.
- **MIME**이란 원래 각기 다른 전자메일 시스템 사이에서 메세지가 오갈 때 겪는 문제점을 해결하기 위해 설계되었는데 워낙 잘 동작했어기 때문에, **HTTP에서도 멀티미디어 콘텐츠를 기술하고 라벨을 붙이기 위해 채택** 되었음.

  - MIME 타입
    - 주 타입(primary object type), 사선(/)으로 구분
      - 부 타입(specific subtype)으로 이루어진 문자열 라벨
      - **HTML 텍스트 문서** -> **text/html 라벨**이 붙음
      - **plain ASCII 텍스트 문서** -> **text/plain 라벨**이 붙음
      - **JPEG 이미지** -> **image/jpeg 라벨**이 붙음
  - **URI(uniform resource identifier)**
    - 웹 서버 리소스는 각자 이름을 갖고 있기 때문에, 클라이언트는 관심 있는 리소스를 지목할 수 있다. 이때 서버 리소스 이름을 **통합 자원 식별자** 혹은 **URI**로 불린다.
  - **URL(uniform resource locator)**
    - 리소스 식별자의 가장 흔한 형태
      - 특정 서버의 한 리소스에 대한 구체적인 위치를 서술한다.
      - URL은 세 부분으로 이루어진 표준 포맷을 따른다.
        - **스킴(scheme)** 리소스에 접근하기 위해 사용되는 **프로토콜을 서술**한다. 보통 HTTP 프로토콜 (예: http://)
          - **서버의 인터넷 주소** (예: www.google.com)
          - **웹 서버의 리소스를 가리킴** (예: /blade.jpeg)
  - **URN(uniform resource name)**
    - 콘텐츠를 이루는 한 리소스에 대해, 그 리소스의 위치에 영향 받지 않는 유일무이한 이름 역할을 한다.

### 1.4 트랜잭션

- HTTP 트랜잭션은 요청 명령(클라이언트가 서버로 보내는)과 응답 결과(서버가 클라이언트에게 돌려주는)로 구성
- <img src="https://velog.velcdn.com/images/mocha/post/88e6ffb2-2bf1-4fb4-b8ed-a6e55dffa3bb/image.jpg" alt="HTTP 트랜잭션" width="600" height="800">

- **메서드**
- HTTP는 HTTP 메서드라고 불리는 여러 가지 종류의 요청 명령을 지원 함.
- **모든 HTTP 요청 메세지는 한 개의 HTTP 메서드를 가진다.**
- | HTTP 메서드 | 설명                                                                 |
  | ----------- | -------------------------------------------------------------------- |
  | GET         | 서버에서 클라이언트로 지정한 리소스를 보내라.                        |
  | PUT         | 클라이언트에서 서버로 보낸 데이터를 지정한 이름의 리소스로 저장하라. |
  | DELETE      | 지정한 리소스를 서버에서 삭제하라.                                   |
  | POST        | 클라이언트 데이터를 서버 게이트웨이 애플리케이션으로 보내라.         |
  | HEAD        | 지정한 리소스에 대한 응답에서, HTTP 헤더 부분만 보내라.              |

- **상태 코드**

  - 모든 HTTP 응답 메세지는 상태 코드와 함께 반환된다.
  - 상태 코드는 **클라이언트에게 요청이 성공했는지 아니면 추가 조치가 필요한지 알려주는 세 자리 숫자**
    - | HTTP 상태코드 | 설명                                           |
      | ------------- | ---------------------------------------------- |
      | 200           | 좋다. 문서가 바르게 반환되었다.                |
      | 302           | 다시 보내라. 다른 곳에 가서 리소스를 가져가라. |
      | 404           | 없음. 리소스를 찾을 수 없다.                   |

- **웹 페이지는 여러 객체로 이루어질 수 있다**
- 애플리케이션은 보통 하나의 작업을 수행하기 위해 여러 HTTP 트랜잭션을 수행한다.
- 예를 들어, https://www.naver.com 으로 HTTP 요청을 보내면 HTML '뼈대'를 한 번의 트랜잭션으로 가져온 뒤, 첨부된 이미지, 그래픽 조각, 자바 애플릿 등을 가져오기 위해 추가로 여러 HTTP 트랜잭션들을 수행한다.

### 1.5 메세지

- HTTP 메시지는 단순한 줄 단위의 문자열이다.
- 요청 메시지: 클라이언트 -> 서버로 보낸 HTTP 메시지
- 응답 메시지: 서버 -> 클라이언트로 보낸 HTTP 메시지
- HTTP 메시지는 크게 3부분으로 이루어져 있다.

  - 시작줄: 메시지의 첫 줄은 시작줄로, 요청이라면 무엇을 해야 하는지 응답이라면 무슨 일이 일어났는지 나타낸다.
  - 헤더: 시작줄 다음에는 0개 이상의 헤더 필드가 이어진다. 구문자로는 쌍점(:)으로 구분되고 헤더 필드를 추가하려면 그저 한 줄을 더하기만 하면된다. 마지막으로 헤더는 빈 줄로 끝난다.
  - 본문: 헤더의 마지막 빈 줄 다음에는 어떤 종류의 데이터든 들어갈 수 있는 메시지 본문이 필요에 따라 올 수 있다. 요청의 본문은 웹 서버로 데이터를 실어 보내며, 응답의 본문은 클라이언트로 데이터를 반환한다.

### 1.6 TCP 커넥션

- TCP 특징

  - 오류 없는 데이터 전송
  - 순서에 맞는 전달 (데이터는 언제나 보낸 순서대로 도착한다)
  - 조각나지 않는 데이터 스트림 (언제든 어떤 크기로든 보낼 수 있다)
  - HTTP 클라이언트가 서버에 메시지를 전송할 수 있게 되기 전에, 인터넷 프로토콜 주소와 포트번호를 사용해 클라이언트와 서버 사이에 TCP/IP 커넥션을 맺어야 한다.
  - <img src="https://velog.velcdn.com/images/mocha/post/7cf26540-7baf-4d10-96a2-8df3161e2bec/image.jpg" alt="웹 브라우저 연결의 기본적인 절차" width="600" height="800">
  - (a) 웹 브라우저는 서버의 URL에서 호스트 명을 추출
  - (b) 웹 브라우저는 서버의 호스트 명을 IP로 변환
  - (c) 웹 브라우저는 URL에서 포트번호(있다면)를 추출
  - (d) 웹 브라우저는 웹 서버와 TCP 커넥션을 맺음
  - (e) 웹 브라우저는 서버에 HTTP 요청을 보냄
  - (f) 서버는 웹 브라우저에 HTTP 응답을 돌려줌
  - (g) 커넥션이 닫히면, 웹 브라우저는 문서를 보여줌

### 1.7 프로토콜 버전

- HTTP/0.9
  - 1991년에 사용되던 버전 금방 HTTP/1.0으로 대체 되었다.
- HTTP/1.0

  - 처음 널리 쓰이기 시작한 버전
  - 버전 번호, HTTP 헤더, 추가 메서드, 멀티미디어 객체 처리를 추가
  - 하지만 여전히 잘 정의된 명세가 아니였음

- HTTP/1.0+

  - keep-alive 커넥션, 가상 호스팅 지원, 프락시 연결 지원을 포함한 많은 기능이 추가됨
  - 공식적이진 않지만 사실상의 표준으로 추가되었다.

- HTTP/1.1
  - 설계의 구조적 결함 교정, 성능 최적화, 잘못된 기능 제거에 집중
  - 현재의 버전
- HTTP/2.0
  - HTTP/1.1 성능 문제를 개선하기 위해 구글의 SPDY 프로토콜 기반으로 설계가 진행 중인 프로토콜이다.

### 1.8 웹의 구성요소

- **프락시**
  - 클라이언트와 서버 사이에 위치한 HTTP 중개자
  - 웹 보안, 애플리케이션 통합, 성능 최적화를 위한 중요한 구성요소
  - 주로 **보안**을 위해 사용
  - **요청과 응답을 필터링**
  - 예를들어, 바이러스 검출 또는 성인 콘텐츠를 차단하는 등의 역할 가능
- **캐시**
  - 많이 찾는 웹 페이지를 클라이언트 가까이 보관하는 HTTP 창고
  - 웹 캐시와 캐시 프락시는 자신을 거쳐 가는 문서들 중 **자주 찾는 것의 사본을 저장**해두는 특별한 종류의 HTTP 프락시 서버
- **게이트웨이**
  - 다른 애플리케이션과 연결된 특별한 웹 서버
  - 다른 서버들의 중개자로 동작하는 특별한 서버
  - 주로 **HTTP 트래픽을 다른 프로토콜로 변환하기 위해 사용**
- **터널**
  - 단순히 HTTP 통신을 전달하기만 하는 특별한 프락시
  - 두 커넥션 사이에서 raw 데이터를 열어보지 않고 그대로 전달해주는 HTTP 애플리케이션
  - 주로 **비 HTTP 데이터를 하나 이상의 HTTP 연결을 통해 그대로 전송해주기 위해 사용**
  - 예를들어, 암호화된 SSL 트래픽을 HTTP 커넥션으로 전송함으로써 웹 트래픽만 허용하는 사내 방화벽을 통과시키는 것이 가능
  - <img src="https://velog.velcdn.com/images/mocha/post/40a79ece-f95f-40b1-93d0-1579413d1394/image.jpg" alt="HTTP/SSL 터널" width="600" height="400">
- **에이전트**
  - 사용자를 위해 **HTTP 요청을 만들어주는 클라이언트 프로그램**

### 1.9 시작의 끝

### 1.10 추가 정보
