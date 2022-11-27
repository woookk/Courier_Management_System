# Courier Management System

## Data Class

### Product Class
- 택배 상품 정보를 담는 클래스
- 상품 번호, 등록한 관리자 번호, 상품명, 배송 상태, 생성 시간으로 구성
- API 형식에 맞게 생성자 구성 요구

### User Class
- 로그인 시 유저 정보 담는 클래스
- 고유 번호로만 구성

## Client Side

### ProductSystemUI Class
- 화면 구성요소 정의, 레이아웃 이용하여 컴포넌트 배치
- 주요 메서드
  - ProductSystemUI() (생성자)
    - 화면을 구성하는 컴포넌트 초기화 및 레이아웃 배치 등
  - void addButtonActionListener
- 이벤트 핸들러 등록 메서드, 모든 버튼의 이벤트 핸들러 등록

### ClientController Class
- Client의 메인
  - UI와 연결 및 서버 API 호출
- 주요 메서드 (API 요청 관련)
  - void login()
    - 로그인 요청
  - void getProducts()
    - 택배 상품 조회 요청
  - void addProduct()
    - 새로운 택배 추가 요청
  - void updateProduct()
    - 기존 택배의 정보(이름, 상태) 변경 요청
  - void deleteProduct()
    - 택배 삭제 요청
    
### HTTPRequestController Class
- Request를 세팅하고 보내는 과정을 모듈화한 클래스
- 주요 메서드
  - void setLoginRequest()
    - 로그인 API request 세팅 및 보내는 역할
  - void setGetRequest()
    - 상품 조회 API request 세팅 및 보내는 역할
  - void setPostRequest()
    - 상품 추가 API request 세팅 및 보내는 역할
  - void setPutRequest() or void setPatchRequest()
    - 상품 수정 API request 세팅 및 보내는 역할
  - void setDeleteRequest()
    - 상품 삭제 API request 세팅 및 보내는 역할

## Server Side

### ProductSystemServer Class
- 여러 클라이언트의 요청 핸들링 할 수 있는 HTTP 서버 구현
- 주요 메서드
  - void start()
    - 서버의 메인 실행 메소드, serversocket 실행하고 클라이언트 연결 및 스레드 생성/처리
  - Class HTTPHandler
    - 각 클라이언트에서 요청한 API 핸들링하고 적합한 Service 메서드 호출

### ProductService Class
- DB와 직접적으로 통신하는 class
- 서버의 비즈니스 로직을 담당
- 주요 메서드
  - void connnectDB()
    - DB와 연결하는 작업 수행
  - void getProducts()
    - DB에 접근하여 택배 상품 조회 작업 수행 및 결과 생성
  - void addProduct()
    - DB에 접근하여 기존 택배의 정보(이름, 상태) 변경 작업 및 결과 생성
  - void deleteProduct()
    - DB에 접근하여 기존 택배 삭제 작업 수행 및 작업 결과 및 작업 결과 생성
  - void setDefaultResponse()
    - 등록되지 않은 형식의 API 호출 시 응답 결과 생성

### HTTPResponseController Class
- Response를 세팅하고 보내는 과정을 모듈화한 클래스
- Service에서 결과를 리턴하는 역할을 하는 클래스
- 주요 메서드
  - void setSuccessLoginResponse()
    - 로그인 성공시 response 세팅하고 보내는 역할
  - void setSuccessGetResponse()
    - 택배 상품 조회 성공시 response 세팅하고 보내는 역할
  - void setSuccessPostResponse ()
    - 택배 추가 작업 성공시 response 세팅하고 보내는 역할
  - void setSuccessPutResponse () 또는 void setSuccessPatchResponse() 
    - 택배 수정 작업 성공시 response 세팅하고 보내는 역할
  - void setSuccessDeleteResponse ()
    - 택배 삭제 작업 성공시 response 세팅하고 보내는 역할
  - void setFailedResponse()
    - 잘못된 API 호출 시 response 세팅하고 보내는 역할