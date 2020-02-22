# 수포자 문제

## Question
- 1번 수포자가 찍는 방식: 1, 2, 3, 4, 5, 1, 2, 3, 4, 5, ...
- 2번 수포자가 찍는 방식: 2, 1, 2, 3, 2, 4, 2, 5, 2, 1, 2, 3, 2, 4, 2, 5, ...
- 3번 수포자가 찍는 방식: 3, 3, 1, 1, 2, 2, 4, 4, 5, 5, 3, 3, 1, 1, 2, 2, 4, 4, 5, 5, ...
- 1번 문제부터 마지막 문제까지의 정답이 순서대로 들은 배열 answers가 주어졌을 때, 가장 많은 문제를 맞힌 사람이 누구인지 배열에 담아 return
- 가장 높은 점수를 받은 사람이 여럿일 경우, return하는 값을 오름차순 정렬

## Answer
```js
function solution(answers) {
  const result = [];
  const givenUpMath = [
    [1, 2, 3, 4, 5],
    [2, 1, 2, 3, 2, 4, 2, 5],
    [3, 3, 1, 1, 2, 2, 4, 4, 5, 5]
  ];
  const points = [0, 0, 0];
  answers.forEach((answer, i) => {
    givenUpMath.forEach((person, j) => {
      if (answer === person[i % person.length]) {
        points[j] += 1;
      }
    });
  });
  const max = Math.max(...points);
  console.log(max);
  points.forEach((point, i) => {
    if (point === max) {
      result.push(i + 1);
    }
  });
  return result;
}
```
