# Pointer
- Go에서는 인자를 받는 함수를 호출할 때 해당 인자는 함수로 복사됨
- 포인터는 값 자체보다는 값이 저장된 메모리상의 위치를 가리킴 (&)

```go
package main

import "fmt"

func zeroval(ival int) {
  ival = 0
}

func zeroptr(iptr *int) {
  *iptr = 0
}

func main() {
  i := 1
  fmt.Println("initial:", i)
  // initial: 1

  zeroval(i)
  fmt.Println("zeroval:", i)
  // zeroval: 1

  zeroptr(&i)
  fmt.Println("zeroptr:", i)
  // zeroptr: 0

  fmt.Println("pointer:", &i)
  // pointer: 0x42131100
}
```
