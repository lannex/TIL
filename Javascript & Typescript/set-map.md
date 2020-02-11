# Set, Map
set, map은 ES6에서 새로 도입한 데이터 구조이다.

## Set()
- value 컬렉션
- 중복을 허용하지 않는 점만 제외하면 배열과 비슷
- index로 값을 조회할 수는 없음

```js
const set = new Set();
set.size; // 데이터 개수
set.has(value); // value 확인 boolean 리턴 indexOf() 보다 빠름. 단, index가 없음
set.add(value); // value 추가
set.delete(value); // value 삭제
set.clear(); // 데이터 모두 삭제
set[Symbol.iterator](); // 새로운 iterator로 리턴

// 기존 js 순회
set.forEach(() => {});
set.keys();
set.values();
set.entries();
```

## Map()
- key-value pair 컬렉션
- key와 value을 연결한다는 점에서 객체와 비슷
- key는 함수, 객체 등을 포함한 모든 값이 가능

```js
const map = new Map();
set.size; // 데이터 개수
map.has(key); // key로 엔트리 확인 boolean 리턴
mag.get(key); // key로 엔드리 가져오기
map.set(key, value); // 엔트리 추가 및 변경
map.delete(key); // 엔트리 삭제
map.clear(); // 데이터 모두 삭제
map[Symbol.iterator]() === map.entries() // 동일

// 기존 js 순회
map.forEach(() => {});
map.keys();
map.values();
```

## to Array
```js
// spread operator
const letters = new Set([ 'abc', 'def' ]);
const array = [...letters];
console.log(array); // [ 'abc', 'def' ];

// array.from()
const foo = new Set(['foo', 'bar']);
const array2 = Array.from(foo);
console.log(array2); // [ 'foo', 'bar' ];
```

## WeakSet, WeakMap
- 참조하는 객체에 다른 참조가 없으면 가비지 컬렉션 됨 (메모리 유리)
- `WeakMap`은 `new`, `.has()`, `.get()`, `.set()`, `.delete()` 만 지원
- `WeakSet`은 `new`, `.has()`, `.add()`, `.delete()` 만 지원
- `WeakSe`t과 `WeakMap`의 key는 반드시 객체(object)여야 됨
