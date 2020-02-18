# Prototype
- Javascript는 Class라는 개념이 없음
- Javascript는 Prototype기반의 언어
- 객체를 생성할 때 프로토타입은 결정
- 결정된 프로토타입 객체는 다른 임의의 객체로 변경할 수 있음(참조의 개념이지만 변경도 가능)
- 인스턴스를 선언해야 접근이 가능함
- 인스턴스 선언은 함수로 객체를 생성된다는 것

```js
// 인스턴스 선언 전 접근
// prototype 속성이 없음
function Foo() {}
Foo.prototype.test = "test";
Foo.prototype.constructor.constructorTest = "constructor.constructorTest";
console.log(Foo.prototype.test); // test
console.log(Foo.constructorTest); // constructor.constructorTest (생성자constructor값)
console.log(Foo.test); // ERROR undefined

// 인스턴스 선언 후 접근
// prototype 속성이 있음
function Foo2 () {}
Foo2.prototype.test = "test";
const foo2Instance = new Foo();
console.log(foo2Instance.test); // test
```

- 인스턴스는 프로토타입의 값을 복사해서 처리
```js
// 프로토타입의 속성을 인스턴스에서 접근만 한다면 프로토타입에 값이 있는지 확인한 뒤에 참조만
// 인스턴스에서 프로토타입 속성으로 연산을 하려고 할 경우, 인스턴스에 메모리가 주어지고, 프로토타입의 속성을 호출하여 받은 값을 연산하여 할당된 메모리에 저장됨

// 값이 복사됨
function Foo() {}
Foo.prototype.test = 100;
const fooInstance = new Foo();
console.log(fooInstance.test); // 100

fooInstance.test = fooInstance.test - 1;
console.log(fooInstance.__proto__.test); // 100
console.log(fooInstance.test);  // 99
```

## Prototype Object
- 함수 객체는 일반 객체와는 달리 prototype 속성도 소유
- 프로토타입 객체도 객체이므로 일반 객체와 같이 프로퍼티를 추가/삭제할 수 있고 이렇게 추가/삭제된 프로퍼티는 즉시 프로토타입 체인에 반영됨
- 객체는 언제나 함수로 생성됨
```js
function Person() {}
const personObject = new Person(); // 함수로 객체를 생성

// 동일한 선언 하지만 prototype 속성의 유무 차이는 존재
const object = {};
const object = new Object();

const array = [];
const array = new Array();
```

- 함수가 정의될때 Constructor 자격 부여, Prototype Object도 같이 생성
- Prototype Object는 `constructor`와 `__proto__`(Prototype Link)를 가지고 있음


## Prototype Link
- `__proto__`속성은 모든 객체가 빠짐없이 가지고 있음
```js
const student = {
  name: 'Kim',
  score: 80
};

// student에는 hasOwnProperty 메서드가 없지만 아래 구문은 동작
console.log(student.hasOwnProperty('name')); // true

// student객체는 __proto__로 자신의 부모 객체(프로토타입 객체)인 Object.prototype을 가리키고 있음
console.log(student.__proto__ === Object.prototype); // true
console.log(Object.prototype.hasOwnProperty('hasOwnProperty')); // true
```

- 프로토타입은 원형의 값이라 변경할 수 없을 것 같지만 `__proto__`으로 접근해서 값을 할당하면 수정이 됨
```js
function Foo() {}
Foo.prototype.test = 100;
const fooInstance = new Foo();
console.log(fooInstance.test); // 100

fooInstance.test = fooInstance.test - 1;
fooInstance.__proto__.test = 50;
const fooInstance2 = new Foo();  // 바꾼 뒤에 Foo로 부터 생성된 객체는 다른 기본 값을 가지게 됨
console.log(fooInstance2.test);  // 50
console.log(fooInstance.test); // 99
```
