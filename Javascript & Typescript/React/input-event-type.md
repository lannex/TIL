# Input in Typescript
- 보통 input에서 이벤트 타입 설정할때 `React.FormEvent<HTMLInputElement>`로 받고 `e.currentTarget.value`를 사용해야 된다.
```js
onChange = (e: React.FormEvent<HTMLInputElement>) => {
  const newValue = e.currentTarget.value;
}
```

- `e.target.value`을 사용하고자 하는 경우는 `React.ChangeEvent<HTMLInputElement>`로 받아야 된다.
```js
onChange = (e: React.ChangeEvent<HTMLInputElement>)=> {
  const newValue = e.target.value;
}
```
