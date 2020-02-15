# enum
- JavaScript에는 없는 개념
- 이름이 부여된 상수 집합
- 하나의 객체

## Difference with Object
- 객체는 특별한 경우를 제외하고 속성을 바꿀 수 있지만 enum은 바꿀 수 없음
- 객체의 속성값은 JavaScript의 모든 값이 가능하지만, enum의 속성값은 문자열 또는 숫자만 허용

## Usage
- 컴파일 과정
```ts
enum Directions {
  Up,
  Down,
  Left,
  Right
}

// compiled
"use strict";
var Directions;
(function (Directions) {
    Directions[Directions["Up"] = 0] = "Up";
    Directions[Directions["Down"] = 1] = "Down";
    Directions[Directions["Left"] = 2] = "Left";
    Directions[Directions["Right"] = 3] = "Right";
})(Directions || (Directions = {}));

// easy to read code
var Directions = {
  Up: 0,
  Down: 1,
  Left: 2,
  Right: 3,
  0: 'Up',
  1: 'Down',
  2: 'Left',
  3: 'Right',
};
```
- 선언가능 방법
```ts
// 명시적으로 값을 할당하지 않으면 0 부터 순차적으로 자동 할당
enum Order {
  A,
  B,
  C,
}
console.log(Order.A, Order.B, Order.C); // 0 1 2

// 숫자 및 표현식
enum Colors {
  RED = 10,
  GREEN = 20,
  BLUE = RED + GREEN
}

// 숫자가 아닌 값을 할당하면 그 이후값은 자동으로 할당되지 않음
enum justEnum {
  A,
  B = "string",
  C,
};

console.log(justEnum.A); // 0
console.log(justEnum.B); // string
console.log(justEnum.C); // ERROR

// const로 선언 시 Enum은 컴파일 결과물을 가지지 않음
const enum Alphabet {
    A = 1,
    B = A * 2
}
console.log(Alphabet.A, Alphabet.B);

// compiled
console.log(1 /* A */, 2 /* B */);
```
