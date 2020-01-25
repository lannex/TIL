# CORS (Cross-Origin Resource Sharing)
**교차 출처 리소스 공유**

한 출처의 리소스를 다른 출처에서 접근할 수 있는 권한을 알려주는 메커니즘.

다른 출처를 가진 리소스를 요청할 때 `cross-origin HTTP` 요청을 실행.

`same-origin policy` 때문에 외부의 요청을 브라우저에서 보안이유로 차단.

```js
// error
Access to fetch at '...' from origin '...' has been blocked by CORS policy: No 'Access-Control-Allow-Origin' header is present on the requested resource. If an opaque response serves your needs, set the request's mode to 'no-cors' to fetch the resource with CORS disabled.
```

## Same Origin
**Same Origin** 확인은 아래 3가지로 결정
1. Scheme name
2. Hostname
3. Port Number

## Preflight
브라우저는 실제로 들어온 요청을 전송하기 전에 `OPTIONS` 메서드로 **preflight** 요청을 서버로 전송.
**preflight** 요청을 받은 서버는 CORS 관련 정보를 헤더에 넣어 클라이언트로 전송.

### Request Header
- `Access-Control-Request-Method` : 실제 요청 시 사용할 메서드
- `Access-Control-Request-Headers` : 브라우저가 실제 요청을 보낼 때 헤더에 추가할 커스텀 속성

### Response Header
- `Access-Control-Allow-Origin` : 허용 Origin
- `Access-Control-Request-Methods` : 허용 요청 메서드
- `Access-Control-Allow-Headers` : 허용 헤더 속성
- `Access-Control-Max-Age` : preflight request 캐시하는 시간(초 단위)

## How to Enable CORS
허용을 하려면 크게 두가지 방법이 존재한다.
1. `Access-Control-Allow-Origin`을 response header에 추가
```js
"Access-Control-Allow-Origin": "*"
// 혹은 whitelist 리스트 추가
// ex "http://abc.com:8080"
```

2. 미들웨어에서 CORS 관련 디펜던시 사용 (세부 옵션은 해당 디펜던시 확인)
```js
// node.js - express
const express = require('express');
const cors = require('cors');

const app = express();
app.use(cors());
```
```go
// go - gin
package main

import (
    "time"

    "github.com/gin-contrib/cors"
    "github.com/gin-gonic/gin"
)

func main() {
	router := gin.Default()
	router.Use(cors.Default())
	router.Run()
}
```
