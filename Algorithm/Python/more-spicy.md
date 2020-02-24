# 더 맵게

## Question
- 모든 음식의 스코빌 지수가 K 이상이 될 때까지 반복하여 섞음
- `섞은 음식의 스코빌 지수 = 가장 맵지 않은 음식의 스코빌 지수 + (두 번째로 맵지 않은 음식의 스코빌 지수 * 2)`
- 스코빌 지수를 담은 배열 scoville과 원하는 스코빌 지수 K가 주어질 때, 모든 음식의 스코빌 지수를 K 이상으로 만들기 위해 섞어야 하는 최소 횟수를 return
- 모든 음식의 스코빌 지수를 K 이상으로 만들 수 없는 경우에는 `-1`을 return

## I/O Example
| scoville             | K   | return |
| -------------------- | --- | ------ |
| [1, 2, 3, 9, 10, 12] | 7   | 2      |

## Answer
```py3
import heapq


def solution(scoville, k):
    heapq.heapify(scoville)
    answer = 0
    while len(scoville) > 1:
        first = heapq.heappop(scoville)
        second = heapq.heappop(scoville)
        if first < k or second < k:
            heapq.heappush(scoville, first + (second * 2))
            answer += 1
        else:
            return answer

    if scoville[0] <= k:
        return -1
    else:
        return answer
```

## Best Answer
```py3
import heapq as hq


def solution(scoville, K):
    hq.heapify(scoville)
    answer = 0
    while True:
        first = hq.heappop(scoville)
        if first >= K:
            break
        if len(scoville) == 0:
            return -1
        second = hq.heappop(scoville)
        hq.heappush(scoville, first + second*2)
        answer += 1

    return answer
```
