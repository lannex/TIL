# Closure
- 내부 함수가 외부 함수의 컨텍스트(변수 등)에 접근할 수 있는 것을 가르킴
- 외부 함수가 실행 뒤 소멸되어도 내부 함수는 외부 함수의 변수 등에 참고 가능
- 함수가 선언된 환경의 (렉시컬) 스코프를 기억하여 함수가 스코프 밖에서 실행될 때에도 이 스코프에 접근할 수 있게 하는 기술

```js
function makeFunc() {
  var name = "Mozilla";
  function displayName() {
    return name;
  }
  return displayName;
}

var myFunc = makeFunc();
// myFunc변수에 displayName을 리턴함
// 유효범위의 어휘적 환경을 유지
myFunc(); // Mozilla
// 리턴된 displayName 함수를 실행(name 변수에 접근)
```

```js
const outer = function() {
  let count = 0;
  function inner(number) {
    count += number;
  }
  return {
    increase: function() {
      inner(1);
    },
    decrease: function() {
      inner(-1);
    },
    show: function() {
      alert(count);
    }
  }
};
// outer를 실행하면 outer함수 스코프를 기억하고 있는 클로저들이 담긴 객체를 반환
// closure는 outer함수 내부에 정의된 count나 inner에 접근 가능
const closure = outer();
closure.increase(); //
closure.show(); // 1
closure.decrease();
closure.show(); // 0
```