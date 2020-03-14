# Hoisting
- `var` 키워드로 선언되거나 초기화된 변수는 현재 스코프의 최상위까지 옮겨지는데 이것을 호이스팅이라고 부름
- 그러나 선언문만 호이스팅되며 할당(있는 경우)은 그대로 있게 됨
- 사실 선언은 실제로 이동되지 않음
- JavaScript 엔진은 컴파일 중에 선언을 파싱하고 선언과 해당 스코프를 인식하는데 선언을 해당 스코프의 맨 위로 옮겨지는 것으로 생각하여 동작을 이해하는 것이 더 쉬울 뿐

```js
// var 선언이 호이스팅
console.log(foo); // undefined
var foo = 1;
console.log(foo); // 1

// let/const 선언은 호이스팅되지 않음
console.log(bar); // ReferenceError: bar is not defined
let bar = 2;
console.log(bar); // 2
```

- 함수 선언은 함수몸체가 호이스팅되는 반면, 변수 선언 형태로 작성된 함수 표현식은 변수 선언만 호이스팅됨
```js
// 함수 선언
console.log(foo); // [Function: foo]
foo(); // 'FOOOOO'
function foo() {
  console.log("FOOOOO");
}
console.log(foo); // [Function: foo]

// 함수 표현식
console.log(bar); // undefined
bar(); // Uncaught TypeError: bar is not a function
var bar = function() {
  console.log("BARRRR");
};
console.log(bar); // [Function: bar]

```

