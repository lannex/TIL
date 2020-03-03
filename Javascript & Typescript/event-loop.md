# Event Loop
![event-loop-1](./event-loop.png)

- Javascript runtime 구조는 크게 `Memory heap`과 `Call stack`
- `Event loop`와 `Task queue (Callback Queue)`등은 Web APIs처럼 따로 존재
- `Event loop`가 하는 일은 간단한데 queue의 첫번째 있는 작업을 stack이 비워져있는지 확인한 뒤 작업을 stack으로 보내는 역할
- 즉, **Call Stack**과 **Task Queue**의 상태를 체크하여, **Call Stack**이 빈 상태가 되면, **Task Queue**의 첫번째 콜백을 **Call Stack**으로 밀어넣음 (이러한 반복적인 행동을 틱(tick) 이라 부름)


![event-loop-2](./event-loop.jpg)

## Call Stack
- 코드가 실행될 때 쌓이는 곳
- Javascript의 큰 특징 중 하나는 `Single thread` 기반의 언어이며 스레드가 하나라는 말은 동시에 하나의 작업만을 처리할 수 있다라는 소리와 같고, 또 구조에서 볼수 있듯이 하나의 `Call stack`을 가지고 있다는 소리
- Javascript 엔진은 하나의 호출 스택을 사용하며, 현재 스택에 쌓여있는 모든 함수들이 실행을 마치고 스택에서 제거되기 전까지는 다른 어떠한 함수도 실행될 수 없음
- Stack: 선입후출(LIFO, Last In First Out)의 룰

## Task Queue
- 비동기적으로 실행된 콜백함수가 보관 되는 영역
- `setTimeout`, `XMLHttpRequest`, `addEventListener` 등등
- Queue: 선입선출(FIFO, Frist In Frist OUT)의 룰

## Microtask Queue
```js
setTimeout(function() { // (A)
  console.log('A');
}, 0);
Promise.resolve().then(function() { // (B)
  console.log('B');
}).then(function() { // (C)
  console.log('C');
});
```
- 콘솔로그는 `B -> C -> A`인데 Promise가 마이크로 태스크를 사용하기 때문
- 마이크로 태스크는 쉽게 말해 일반 태스크보다 더 높은 우선순위를 갖는 태스크
- 태스크 큐에 대기중인 태스크가 있더라도 마이크로 태스크가 먼저 실행

## Order of action
1. V8 엔진에서 코드가 실행되면, Call Stack에 쌓임
2. Stack의 선입후출의 룰에 따라 제일 마지막에 들어온 함수가 먼저 실행되며, Stack에 쌓여진 함수가 모두 실행
3. 비동기함수가 실행된다면, Web API가 호출
4. Web API는 비동기함수의 콜백함수를 Task Queue에 밀어넣음(Promise는 Microtask Queue로, Timeout은 Task Queue로, RequestAnimationFrame은 Animation Frame으로)
5. Event Loop는 Call Stack이 빈 상태가 되면 Task Queue에 있는 첫번째 콜백을 Call Stack으로 이동
