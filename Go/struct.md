# Struct
Go에는 클래스가 없다.
대신 필드를 하나로 묶어서 클래스처럼 사용할 수 있는 것이 Struct(구조체).
사실상의 클래스(에 가까움).

- 클래스가 없기 때문에 상속도 없음 -> Embedded type(포함타입)으로 처리
- 구조체 내부에 메서드를 포함 할 수 없으므로 외부에 메서드를 선언한 뒤 Receiver(수신자)로 연결해서 사용
- 메서드 선언 시 Go에서 함수 인자는 복사되니 포인터를 사용해야함
- 구조체는 mutable
- 먼저 `type`을 `struct`로 선언하고 초기화해서 사용
- 객체 접근하듯이 `.`로 필드 접근

```go
package main

import "fmt"

type Data struct {
    a int
    b int
}

func (d Data) Immutate() {
    d.a = 10
    d.b = 20
}

func (d *Data) Mutate() {
    d.a = 10
    d.b = 20
}

func main() {
    d := &Data{0, 0}
    fmt.Println(d) // &{0 0}

    d.Immutate()
    fmt.Println(d) // &{0 0}

    d.Mutate()
    fmt.Println(d) // &{10 20}
}
```

## Methods
- 메서드 구현은 수신자로 받으면 됨

```go
type Rect struct {
    width int
    height int
}

// 수신자
func (rect *Rect) area() int {
    return rect.width * rect.height
}

func main() {
    r := Rect{100, 200}
    fmt.Println(r.area()) // 20000
}
```

### Embedded type
```go
type Ball struct {
    Radius int
    Material string
}

type Football struct {
    // 변수로 선언해서 호출할 경우
    B Ball
    // 익명으로 호출할 경우
    Ball
    ...
    Player string
}
```