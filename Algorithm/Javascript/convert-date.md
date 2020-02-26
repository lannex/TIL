# 12시간 단위의 Date를 초를 추가하고 24시간 단위로 변경

## Question
- t는 12시간 형태의 시간
- n은 t에 추가될 초단위 시간
- `PM 01:10:20`을 10초 뒤 24시 단위인 `13:10:30`로 리턴
- 단, `AM 12:10:00`은 24시간 단위 표시로 `00:10:00` 이고 `PM 12:10:00`은 24시간 단위 표시로 `12:10:00`이여야 함

## Answer
```js
function solution(t, n) {
  const splittedP = t.split(" ");
  const ampm = splittedP[0];
  const splittedTime = splittedP[1].split(":");
  let hours = Number(splittedTime[0]);
  if (ampm === "PM") {
    hours += 12;
  }
  let minutes = Number(splittedTime[1]);
  let seconds = Number(splittedTime[2]) + n;
  const time = new Date();
  time.setHours(hours);
  time.setMinutes(minutes);
  time.setSeconds(seconds);
  let h = time.getHours();
  const m = time.getMinutes();
  const s = time.getSeconds();
  function pad(number) {
    return (number < 10 ? "0" : "") + number;
  }
  if (ampm === "AM" && hours === 12) {
    h -= 12;
  } else if (ampm === "PM" && hours === 24) {
    h += 12;
  }
  return `${pad(h)}:${pad(m)}:${pad(s)}`;
}
```