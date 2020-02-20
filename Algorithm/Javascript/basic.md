# 기본적인 문제

## 숫자의 자릿수를 각각 떼어내서 모두 더하기

```js
function solution(n) {
  const splitedNum = String(n).split("");
  const answer = splitedNum.reduce((prevValue, currentValue) => {
    return prevValue += Number(currentValue);
  }, 0);

  return answer;
}
console.log(solution(123)) // 6
```

## 문장에서 띄어쓰기한 단어들을 기준으로 각 단어들의 0과 짝수 인덱스는 대문자, 홀수 인덱스는 소문자로 변환하기

```js
function solution(s) {
  const splited = s.split(" ");
  const answer = splited.map(item => {
    const character = item.split("");
    const newCharacter = character.map((c, i) => {
      if (i % 2 === 1) {
        return c.toLowerCase();
      }
      return c.toUpperCase();
    });
    return newCharacter.join("");
  });
  return answer.join(' ');
}
console.log(solution("try hello world")) // TrY HeLlO WoRlD
```