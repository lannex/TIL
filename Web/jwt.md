# JWT (JSON WEB TOKEN)
- 서버와 클라이언트 간 정보를 주고 받을 때 Http 리퀘스트 헤더에 JSON 토큰을 넣은 후 서버는 별도의 인증 과정없이 헤더에 포함되어 있는 JWT 정보를 통해 인증
- header, payload, signature로 구성

## Header (JSOE Header - JSON Object Signing and Encryption)
- JWT 토큰을 어떻게 해석해야 하는지를 명시한 부분

## Payload (JWT Claim Set)
- 토큰에 담을 정보가 들어있음

## Signature
- JSOE Header랑 JWT Claim Set만으로 encode를 한다면 누구나 쉽게 위변조를 할 수 있기에 이를 방지하기 위해 사용
- Header에서 지정했던 알고리즘으로 인코딩하여 Signature를 생성

## Pros
- URL 파라미터와 헤더로 사용
- 수평 스케일이 용이
- 디버깅 및 관리가 용이
- 트래픽 대한 부담이 낮음
- REST 서비스로 제공 가능
- 내장된 만료
- 독립적인 JWT

## Cons
- 토큰은 클라이언트에 저장되어 데이터베이스에서 사용자 정보를 조작하더라도 토큰에 직접 적용할 수 없음
- 더 많은 필드가 추가되면 토큰이 커질 수 있음
- 비상태 애플리케이션에서 토큰은 거의 모든 요청에 대해 전송되므로 데이터 트래픽 크기에 영향을 미칠 수 있음