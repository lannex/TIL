# 채널 Channel
goroutine끼리 통신 수단으로 쓰여지며 일종의 파이프.

> Channels can be thought as pipes using which Goroutines communicate. Similar to how water flows from one end to another in a pipe, data can be sent from one end and received from the another end using channels.

## 선언
키워드 `chan` 사용하며 타입은 어떤 것이든 가능.

zero value는 `nil`.

메모리 할당하려면 `make()` 사용.

```go
// zero value
var channel1 chan int // nil

// 메모리 할당
var channel2 chan int= make(chan int)
var channel2 = make(chan int)
channel2 := make(chan int)
```

## 연산자
채널은 변수라고 볼 수는 없어서 값을 저장하려면 따로 할당해야됨.

`<-`를 사용.

```go
data := <- channel1 // channel1로부터 읽기
channel2 <- data // channel2에 쓰기
```

보내거나 받을때 모두 블로킹. (`<-` 만나면 대기)

## 단방향
기본적으로는 양방향으로 데이터를 주고받지만 단방향으로도 쓸 수 있다.
```go
// 보내기 (채널에 값을 보내기만)
func sending(channel1<- chan string) {
    channel1 <- "data"
}

// 받기 (채널에 값을 받기만)
func receiving(<-channel1 chan string) {
    fmt.Println(<-channel1)
    // 출력값 : data
}
```

## 버퍼링
멀티 버퍼는 `make`에서 선언.

```go
func main() {
    // 최대 2개의 값을 버퍼
	channel := make(chan int, 2)
	channel <- 1
	channel <- 2
	fmt.Println(<-channel)
	fmt.Println(<-channel)
}
```

## Deadlock
goroutine을 호출할 때 `go`를 사용하지 않으면 `deadlock`.

goroutine없이 값을 받을때도 `deadlock`. (멀티 버퍼는 가능)

```go
package main

func test(value int, channel1 chan int) {
    channel1 <- value + 1
}

func main() {
    // deadlock
    channel1 := make(chan int)
    test(1, channel1)
    value := <-channel1
    fmt.Println(value)

    // deadlock
    channel2 := make(chan int)
    channel2 <- 5
}
```

```go
fatal error: all goroutines are asleep - deadlock!
```






