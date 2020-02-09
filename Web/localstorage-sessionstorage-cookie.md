# LocalStorage, SessionStorage and Cookie
- HTML5에서 Web Storage인 LocalStorage, SessionStorage는 웹데이터를 클라이언트에 저장할 수 있는 자료구조
- 별차이 없을 정도로 Cookie와 비슷

# LocalStorage, SessionStorage
- 서버로 전송 불가
- 객체 저장 가능 (브라우저마다 조금씩 다름)
- 용량 제한 없음
- 만료기간 지정안함
- window global 객체를 통해 저장과 조회
- SessionStorage는 브라우저가 닫히면 데이터가 지속되지 않으나 LocalStorage는 브라우저가 닫혀도 데이터 저장됨
- SessionStorage는 다른 탭이나 브라우저라면 서로 다른 영역으로 인식되나 LocalStorage은 도메인만 같으면 데이터 공유 가능

# Cookie
- 서버로 전송 가능
- 최대 쿠키 수는 20개, 최대 쿠키 사이즈는 4kb로 제한
- 만료기간 지정해야됨
