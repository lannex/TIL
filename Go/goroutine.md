# 동시성을 위한 goroutine
javascript는 싱글 스레드지만 이벤트 루프로 동시성(Concurrency)을 지원하는데 반해 Go는 동시성을 지원하기 위해 goroutine이라는 것을 사용

## goroutine 특징
- OS 스레드보다 훨씬 가볍고 한 스레드에 여러개의 goroutine이 동작
- 생성하는데 메모리가 적음(2kb)
- 마찬가지로 철거하는데도 비용이 적게 듦
- OS에서 스케줄링하지 않고 자체적으로 Go runtime에서 처리
- 문법이 간단

```go
package main

import (
    "fmt"
    "time"
)

func goroutine() {
    fmt.Println("goroutine")
}
func main() {
    go goroutine()
    time.Sleep(1 * time.Second)
    fmt.Println("main terminated")
}
```

`go` 키워드 선언만으로 간단하다.

```go
package main

import (
    "fmt"
    "time"
)

func numbers() {
    for i := 1; i <= 5; i++ {
        time.Sleep(250 * time.Millisecond)
        fmt.Printf("%d ", i)
    }
}
func alphabets() {
    for i := 'a'; i <= 'e'; i++ {
        time.Sleep(400 * time.Millisecond)
        fmt.Printf("%c ", i)
    }
}
func main() {
    go numbers()
    go alphabets()
    time.Sleep(3000 * time.Millisecond)
    fmt.Println("main terminated")
}
```
출력 결과는 `1 a 2 3 b 4 c 5 d e main terminated`.

동시에 두 함수 동작이 포인트.


