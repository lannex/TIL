# Async Loops
비동기 반복처리를 정리하자면...

- 순차적 호출은 `for of`.
- 동시적 호출은 `Promise.all`.

## `for of`
```js
async function serial(array) {
  for (const item of array) {
    await delay(item);
  }
}
```

## `Promise.all`
```js
async function parallel(array) {
  const promises = array.map(item => delay(item));
  await Promise.all(promises);
}
```
