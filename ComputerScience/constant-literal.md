# Constant and Literal

## Literal
- 리터럴은 상수와 매우 유사한 의미이지만, 엄격히 말하면 다른 의미
- 리터럴의 사전적 의미는 '문자 그대로, 직역의' 뜻
- 리터럴이란 소스 코드의 고정된 값

## Differences
- 상수는 변하지 않는 변수(메모리 위치) 메모리 값을 변경할 수 없음
- 리터럴은 변수의 값이 변하지 않는 데이터(메모리 위치안의 값)

즉, 한번 메모리에 변수를 지정과 초기화하고 난 뒤에는 에는 값을 바꿀 수 없는 변수가 상수라면 리터럴은 이러한 변수 및 상수에 저장되는 값 자체를 말함

## JS Function Literal
```js
function test(seatNum) {
  alert("function");
}

let test = function(seatNum) {
  alert("function literal");
};

```
## JS Object Literal
```js
let test = {
  name: "SSJ",
  age: 37,
};
```
