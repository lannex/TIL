# 탑 문제

## Question
- 왼쪽으로 값이 넘어가는 탑
- 현재 탑 높이보다 왼쪽 탑(이전 탑) 높이가 더 높을때 값을 받을 수 있음
- 현재 탑 높이보다 높지 않으면 계속해서 이전 탑들을 확인
- 맨 왼쪽부터 순서대로 탑의 높이를 담은 배열 heights가 매개변수로 주어질 때 각 탑이 쏜 신호를 어느 탑에서 받았는지 기록한 배열을 return

## I/O Example
| heights         | return          |
| --------------- | --------------- |
| [6,9,5,7,4]     | [0,0,2,2,4]     |
| [3,9,9,3,5,7,2] | [0,0,0,3,3,3,6] |
| [1,5,3,6,7,6,5] | [0,0,2,0,0,5,6] |

## Answer
```js
function solution(heights) {
  const answer = [];
  for (let i = heights.length - 1; i > 0; i -= 1) {
    for (let j = i - 1; j >= 0; j -= 1) {
      if (heights[j] > heights[i]) {
        answer.unshift(j + 1);
        break;
      } else if (j === 0) {
        answer.unshift(0);
      }
    }
  }
  answer.unshift(0);
  return answer;
}
```

## Best Answer
```js
function solution(heights) {
  return heights.map((v, i) => {
    while (i) {
      i -= 1;
      if (heights[i] > v) {
        return i + 1;
      }
    }
    return 0;
  });
}
```
