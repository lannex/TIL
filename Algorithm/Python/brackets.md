# 괄호 문제

## Question
- 올바른 괄호는 `()` 짝지어짐
- `(` `)`만으로 끝나는 것은 올바르지 않은 괄호임
- 예를들어 `()()` 또는 `(())()` 는 올바른 괄호
- 예를들어 `)()(` 또는 `(()(` 는 올바르지 않은 괄호
- 문자열 s는 `(` 또는 `)` 로만 이루어져 있음
- 문자열 s가 올바른 괄호이면 `true`를 return, 올바르지 않은 괄호이면 `false`를 return하는 함수 만들기

## Answer
```py3
def solution(brackets):
    stack = []
    for bracket in brackets:
        if bracket == '(':
            stack.append(bracket)
        elif stack:
            stack.pop()
        else:
            return False
    return len(stack) == 0
```
