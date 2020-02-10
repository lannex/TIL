# Generics
Javascript 동적타이핑인데다 런타임 시 에러가 발생하기 때문에 Generic(제네릭)이 원래 없다.

Typescript는 정적타이핑이라서 재사용성과 확장성을 높여 중복된 코드를 방지하기 위해 Generic이 존재한다.

한마디로 정의하자면 클래스 내부나 함수 내부에서 사용하는 데이터의 타입을 외부에서 지정하는 것이다.

- **Class**와 **Function**에서 사용 (type, interface도 가능)
- 관례상 `T`, `U`...대문자로 선언
- 컴파일러가 리턴하는 타입을 알 수 있게 되어 에러 확인이 가능
- 아무래도 실제 개발보다는 라이브러리를 개발할때 많이 사용

```ts
// class
class Children<T> {
  private children: T[] = [];

  constructor() {}

  add(child: T): void {
    this.children.push(child);
  }

  pop(): T {
    return this.children.pop();
  }
}

const teddyChildren = new Children<number>();
const emmaChildren = new Children<string>();
const avaChildren = new Children<boolean>();

// function
function identity<T>(arg: T): T {
  return arg;
}

const output = identity<string>("myString");

// 타입 인수 추론(type argument inference)
const output = identity("myString");
```

## Function

### Multiple generics
```ts
function test<T, U>(a1: T, a2: U): [T, U] {
  return [a1, a2];
}
test<string, boolean>("true", true);
```

### Rest generics
```ts
interface ABC {
  a: any;
  b: any;
  c: any;
}

function test<T extends ABC>(obj: T) {
  let { a, b, c, ...rest } = obj;
  return rest;
}
```

### Arrow function
```ts
const asyncData = async <T, U>(param: T): Promise<U> => {
  const res = await fetch(`${param}`);
  return res.json();
}
const data: DataType = await asyncData<string, DataType>(baseUrl);

// or
// extends {}가 extends any보다 나으며 T가 객체가 되게 강제함
const foo = <T extends {}>(x: T) => x;

// 만약 ERROR : unclosed `T` tag
const foo = <T>(x: T) => x;
// 제네릭 매개 변수에 extends를 사용해서 제네릭임을 컴파일러에 알림
const foo = <T extends unknown>(x: T) => x;
```

## Constraints
```ts
// 이렇게 선언하면 T가 무슨 타입인지 모르니 에러
function test<T>(arg: T): T {
  console.log(arg.length);
  return arg;
}

// 수정
// length 프로퍼티 확장하면 에러가 없어짐
interface Lengthwise {
  length: number;
}

function test<T extends Lengthwise>(arg: T): T {
  console.log(arg.length);
  return arg;
}
// number 는 length 프로퍼티 없으니 에러
test(3);
// 대신 모든 필수 프로퍼티가 있는 타입의 값을 전달해야 함
test({ length: 10, value: 3 });
```

`keyof T`은 **인덱스 타입 쿼리 연산자** 즉, key 값을 체크하고 없는 key 값은 에러

```ts
function getProperty<T, K extends keyof T>(obj: T, key: K) {
  return obj[key];
}

let x = { a: 1, b: 2, c: 3, d: 4 };

getProperty(x, "a"); // pass
getProperty(x, "m"); // error : 타입 'm'의 인수를 'a' | 'b' | 'c' | 'd' 에 할당 할 수 없음
```

