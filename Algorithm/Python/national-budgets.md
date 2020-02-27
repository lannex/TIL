# 국가 예산 최대 평균값

## Question
- 정해진 총액(M) 이하에서 가능한 한 최대의 총 예산(return)을 다음과 같은 방법으로 배정함
  - 모든 요청이 배정될 수 있는 경우에는 요청한 금액을 그대로 배정
  - 모든 요청이 배정될 수 없는 경우에는 특정한 정수 상한액을 계산하여 그 이상인 예산요청에는 모두 상한액을 배정
  - 상한액 이하의 예산요청에 대해서는 요청한 금액을 그대로 배정
- 국가 예산이 `485`이고 지방 예산 요청이 각각 `[120, 110, 140, 150]` 이라고 한다면 상한액을 `127`로 잡을 경우 `[120, 110, 127, 127]`을 배정하고 그 합이 `484`로 가능한 최대가 됨

## I/O Example
| budgets              | M   | return |
| -------------------- | --- | ------ |
| [120, 110, 140, 150] | 485 | 127    |

## Answer
```py3
def solution(budgets, M):
    budgets.sort()
    answer = 0
    maxBudget = budgets[-1]
    totalBudgets = sum(budgets)

    if totalBudgets > M:
        start = 0
        end = maxBudget
        compareMid = 0

        while True:
            mid = (start + end) // 2
            total = 0

            for budget in budgets:
                if budget > mid:
                    total += mid
                else:
                    total += budget

            if mid == compareMid:
                answer = mid
                break

            if total > M:
                end = mid - 1
            else:
                start = mid + 1

            compareMid = mid
        return answer

    else:
        return maxBudget

```