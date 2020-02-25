# 드래그 범위에 선택되는 아이템들 개수

## Question
- x, y의 평면위에 마우스 드래그 시작점(start)과 끝점(end)이 주어짐
- 위치를 담고 있는 배열 points가 주어짐
- 같은 위치에 두 개 이상의 point는 없음
- 범위안에 들어가는 포인트 총개수를 return

## I/O Example
| points                           | start  | end    | return |
| -------------------------------- | ------ | ------ | ------ |
| [[2, 3], [1, 1], [3, 4], [0, 3]] | [1, 1] | [4, 3] | 2      |
| [[2, 3], [1, 1], [3, 4], [0, 3]] | [2, 3] | [0, 1] | 3      |

## Answer
```js
function solution(points, start, end) {
  const width = Math.abs(start[0] - end[0]);
  const height = Math.abs(start[1] - end[1]);
  const minX = Math.min(start[0], end[0]);
  const minY = Math.min(start[1], end[1]);
  let answer = 0;
  points.forEach(item => {
    if (
      item[0] <= minX + width &&
      item[0] >= minX &&
      item[1] <= minY + height &&
      item[1] >= minY
    ) {
      answer += 1;
    }
  });
  return answer;
}
```