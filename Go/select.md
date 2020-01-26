# Select
**switch**와 별차이 없지만 **select**는 channel로만 사용됨.

- case에 channel 값이 들어올 때 까지 블록
- 단, default를 지정하면 default를 처리하고 다시 동작
- switch와 다르게 select 키워드 뒤에 변수를 따로 지정하지 않음
- 여러 채널을 모니터링하다가 먼저 데이터가 도착한 채널의 데이터를 우선 읽어 처리
- 채널의 데이터를 무한정 대기
- select는 루프가 아님
- case만큼 모두 동작하게 하려면 루프를 사용

```go
package main

import (
    "fmt"
    "time"
)

func main() {
	test1 := make(chan int32)
	test2 := make(chan string)

	go func() {
		time.Sleep(200 * time.Millisecond)
		test1 <- int32(7)
	}()

	go func() {
		time.Sleep(100 * time.Millisecond)
		test2 <- "일곱개"
	}()

	select {
	case x := <-test1:
		fmt.Printf("test1: %v\n", x)
	case y := <-test2:
		fmt.Printf("test2: %v\n", y)
	}
}
```
