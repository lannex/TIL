# Arrow Function (화살표 함수)
- 화살표 함수 표현(arrow function expression)은 function 표현에 비해 구문이 짧음
- 자신의 `this`, `arguments`, `super` 또는 `new.target`을 바인딩 하지 않음
- 화살표 함수는 항상 익명
- 메소드 함수가 아닌 곳에 가장 적합하며 그래서 생성자로서 사용할 수 없음

## this
- function 키워드로 생성한 일반 함수와 화살표 함수의 가장 큰 차이점은 `this`
- 화살표 함수의 this 언제나 상위 스코프의 `this`를 가리키며 이를 `Lexical this`라고 함

```js
function Prefixer(prefix) {
  this.prefix = prefix;
}

Prefixer.prototype.prefixArray = function(arr) {
  // this는 상위 스코프인 prefixArray 메소드 내의 this를 가리킨다.
  return arr.map(x => `${this.prefix}  ${x}`);
};

const pre = new Prefixer("Hi");
console.log(pre.prefixArray(["Lee", "Kim"])); // ['Hi Lee', 'Hi Kim']
```

- 화살표 함수는 `call`, `applay`, `bind` 메소드를 사용하여 `this`를 변경할 수 없음

```js
window.x = 1;
const normal = function () { return this.x; };
const arrow = () => this.x;

console.log(normal.call({ x: 10 })); // 10
console.log(arrow.call({ x: 10 }));  // 1
```

## method
- 화살표 함수로 method를 정의하는 것은 피해야 함
```js
// Bad
const person = {
  name: 'Lee',
  sayHi: () => console.log(`Hi ${this.name}`)
};

person.sayHi(); // Hi undefined

// Good
const person = {
  name: 'Lee',
  sayHi() { // === sayHi: function() {
    console.log(`Hi ${this.name}`);
  }
};

person.sayHi(); // Hi Lee
```

## prototype
- 화살표 함수로 prototype을 정의하는 것은 피해야 함
```js
// Bad
const person = {
  name: 'Lee',
};

Object.prototype.sayHi = () => console.log(`Hi ${this.name}`);

person.sayHi(); // Hi undefined

// Good
const person = {
  name: 'Lee',
};

Object.prototype.sayHi = function() {
  console.log(`Hi ${this.name}`);
};

person.sayHi(); // Hi Lee
```

## new (생성자)
- 화살표 함수는 생성자 함수로 사용할 수 없음
- 화살표 함수는 prototype 프로퍼티를 가지고 있지 않음
```js
const Foo = () => {};

// 화살표 함수는 prototype 프로퍼티가 없다
console.log(Foo.hasOwnProperty('prototype')); // false

const foo = new Foo(); // TypeError: Foo is not a constructor
```

## addEventListener
- `addEventListener` 함수의 콜백 함수를 화살표 함수로 정의하면 `this`가 상위 컨택스트인 전역 객체 `window`를 가리킴
```js
// Bad
var button = document.getElementById('myButton');

button.addEventListener('click', () => {
  console.log(this === window); // => true
  this.innerHTML = 'Clicked button';
});

// Good
var button = document.getElementById('myButton');

button.addEventListener('click', function() {
  console.log(this === button); // => true
  this.innerHTML = 'Clicked button';
});
```

## yield
- `yield` 키워드는 화살표 함수의 본문(그 안에 더 중첩된 함수 내에서 허용한 경우를 제외하고)에 사용될 수 없음
- 그 결과, 화살표 함수는 생성기(generator)로서 사용될 수 없음
