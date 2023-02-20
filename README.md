# AI를 활용한 안면인식 출결 시스템
## 프로젝트 내용

---

### 문제점

- 대리 출석
    
    코로나로 인해 학생들의 직접 강의를 듣는지 확인할 방법이 부족해 지면서 대리출석의 위험이 커지고 있다
    
- 강의 시간 문제
    
    학생들의 출석을 부르는데 수업 시간의 5~6분 정도가 소요된다
    

### 내용

- 비대면 및 대면 수업의 강의 시간 확보 및 대리 출석 근절을 목표
- 기능
    - 얼굴을 통한 안면인식 로그인
    - 학생들의 출석 기록을 교수님 이메일로 보내는 기능
    - Zoom코드 변경 버튼을 통한 Zoom 코드 공지 간편화기능

## 프로젝트 설계

---

### UI

- 메인 페이지

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/ec1bad71-9655-4da9-a59e-04e0ab9e249f/Untitled.png)

- 회원 등록

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/cfbf9796-6ba5-4486-9c69-0c95e5980681/Untitled.png)

- 교수님 페이지
    - 출석기록 이메일 전송
    - 실시간 강의 목록

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/df38a15c-d188-4bb3-8b26-09b297085517/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/f1dfc2e6-951c-4117-bfa2-795a328a0cd8/Untitled.png)

- 학생 페이지
    - 대면 강의 출석
    - 실시간 강의 목록

### Opencv

- 회원 등록
    - 회원가입시 이미지를 웹캠에서 받아서 저장
    - 학생 세부사항을 데이터베이스에 저장

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/081eefff-0c37-41bf-a352-2b037c51199a/Untitled.png)

- 출석 확인
    - 웹캠의 상하좌우를 학습시킨 모델이 비교를 통해 신뢰도가 0.55가 넘으면 확인

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/6a821a71-21ad-42bd-bca3-ed9054720c78/Untitled.png)

- 이메일 전송
    - Yamail을 통해 구글 이메일로 데이터베이스에 저장된 출결정보를 csv로 전송
    
    ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/4845beda-fd63-4c19-b228-d8367d0612b1/Untitled.png)
    

### 서버

- 서버 플로우차트
    - Opencv와 같은 라이브러리는 용량의 제한 때문에 Lambda로 구현을 못함
    - Nginx
        - 아파치 보다 가벼우면서 강력한 프로그램
        - 파이썬 웹 개발에 대한 정보가 많다
        - event-driven의 비동기 구조
        
        동영상을 이용해 정보를 얻는 기능 때문에 동시 접속자 수의 증가에 대해 대응하기에 적합한 방식의 웹서버라고 생각했다.
        
        - reverse proxy
        
        서버 확장에 용이하고, 보안적으로도 더 뛰어났다.
        
        - 무중단 배포
        
        무중단 배포가 가능하여 채팅 기능이 있는 웹사이트이기에 배포시 중단되지 않는점이 사용자들에게 사용성 및 편의성을 증대시킨다.
        
    - Gunicorn
        - 파이썬으로 되어있어 호환이 잘된다
        - 디버깅이 파이썬으로 되어있어 편하다
    

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/84cef4de-69f1-44f4-a96f-f6cd961c2d6c/Untitled.png)

### 데이터 베이스

- ORM
    - 객체 지향적인 코드로 인해 더 직관적이고 비즈니스 로직에 집중
    - 재사용 및 유지 보수의 편리성이 증가
    - DBMS 종속성이 줄어든다

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/32a0e875-496e-4b58-ba8e-7e1dc9833663/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/adb50a56-b201-4877-a602-538c9fa69300/Untitled.png)
