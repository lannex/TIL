# `this`
- JavaScript에서 함수의 `this` 키워드는 다른 언어와 다르게 동작
- 대부분의 경우 this의 값은 함수를 호출한 방법이 결정
- ECMAScript 5는 함수를 어떻게 호출했는지 상관하지 않고 `this` 값을 설정할 수 있는 `bind` 메서드를 도입
- ECMAScript 2015는 스스로의 `this` 바인딩을 제공하지 않는 화살표 함수를 추가

## Global
- 아무 함수에도 속하지 않은 범위에서 `this`는 엄격 모드 여부에 관계 없이 전역 객체를 참조
```js
// 웹 브라우저에서는 window 객체가 전역 객체
console.log(this === window); // true

a = 37;
console.log(window.a); // 37

this.b = "MDN";
console.log(window.b)  // "MDN"
console.log(b)         // "MDN"
```

## Function
- 일반 함수
```js
function f1() {
  return this;
}

// 브라우저
f1() === window; // true

// Node.js
f1() === global; // true
```

- 엄격 모드
```js
function f2(){
  "use strict"; // 엄격 모드 참고
  return this;
}

f2() === undefined; // true
```

## `apply`, `call`, `bind`
```js
var obj = { c: "d" };
function f(text) {
  console.log(this, text);
  return "f";
}
f('window'); // Window
const binded = f.bind(obj, "bind"); // obj
f.call(obj, "call"); // obj
f.apply(obj, ["apply"]); // obj
```

## Arrow Function
- 화살표 함수에서 `this`는 자신을 감싼 정적 범위(lexical context)
- 전역 코드에서는 전역 객체를 가리킴

## Method of Object
- 화살표 함수는 상위 스코프를 상속하니 객체의 메서드로 적합하지 않음
- 일반 function 키워드로 선언하면 `this`는 객체 그 자신
```js
var o = {
  prop: 37,
  f: function() {
    return this.prop;
  }
};

console.log(o.f()); // 37
```

## `new`
- `new`생성자의 `this`는 instance 자기 자신
```js
function Person () {
  this.age = 30;
  console.log(this); // Person { age: 30 }
}

new Person();
```

## DOM Events
```js
// 처리기로 호출하면 관련 객체를 파랗게 만듦
function bluify(e) {
  // 언제나 true
  console.log(this === e.currentTarget);
  // currentTarget과 target이 같은 객체면 true
  console.log(this === e.target);
  this.style.backgroundColor = '#A5D9F3';
}

// 문서 내 모든 요소의 목록
var elements = document.getElementsByTagName('*');

// 어떤 요소를 클릭하면 파랗게 변하도록
// bluify를 클릭 처리기로 등록
for (var i = 0; i < elements.length; i++) {
  elements[i].addEventListener('click', bluify, false);
}
```
