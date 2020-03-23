# 1. 리스트 삭제
- 다음 리스트에서 400, 500를 삭제하는 code를 입력하세요.
```py3
nums = [100, 200, 300, 400, 500]
```
## 답
```py3
nums.pop()
nums.pop()
print(nums)
```

# 2. 리스트의 내장함수
```py3
l = [200, 100, 300]
<pass>
print(l)
```
- `<pass>`부분에 리스트 내장함수를 insert를 이용하여 코드를 입력하고 다음과 같이 출력되게 하세요.
```py3
[200, 100, 10000, 300]
```

## 답
```py3
l.insert(2, 10000)
print(l)
```

# 3. 변수의 타입
- 다음 출력 값으로 올바른 것은?
```py3
l = [100, 200, 300]
print(type(l))
```

## 답
```py3
class 'list'
```

# 4. 변수의 타입 2
- 다음 변수 a를 print(type(a))로 넣었을 때 출력될 값과의 연결이 알맞지 않은 것은?

1. 입력 : a =1, 출력 : class 'int'
2. 입력 : a = 2.22, 출력 : class 'float'
3. 입력 : a = 'p', 출력 : class 'char'
4. 입력 : a = [1, 2, 3], 출력 : class 'list'

## 답
```
3. 입력 : a = 'p', 출력 : class 'char'
class 'str' 이 맞는 출력값입니다.
```

# 5. for문 계산
- 다음 코드의 출력 값으로 알맞은 것은?
```py3
a = 10
b = 2
for i in range(1, 5, 2):
    a += i
print(a+b)
```

## 답
```py3
16
```

# 6. False
- True를 찾아주세요.

1. None
2. 1
3. ""
4. 0
5. bool(0)

## 답
```
2. 1
```

# 7. 변수명
- 다음 중 변수명으로 사용할 수 없는 것 2개를 고르시오.

1. age
2. a
3. as
4. _age
5. 1age

## 답
```
3. as
5. 1age
```

# 8. 딕셔너리 키 이름 중복
- 출력값을 입력하시오. (출력값은 공백을 넣지 않습니다.)
```py3
d = {'height':180,'weight':78,'weight':84,'temparture':36,'eyesight':1}
print(d['weight'])
```

## 답
```py3
84
```

# 9. sep과 end를 활용한 출력방법
- 다음 소스 코드를 완성하여 날짜와 시간을 출력하시오.
```py3
year = '2019'
month = '04'
day = '26'
hour = '11'
minute = '34'
second = '27'
print(year, month, day, )
print(hour, minute, second, )
```
```py3
2019/04/26 11:34:27
```

## 답
```py3
print(year, month, day, sep='/', end=' ')
print(hour, minute, second, sep=':')
```

# 10. 별 찍기
```py3
# input
5

# output
    *
   ***
  *****
 *******
*********
```

## 답
```py3
n = int(input())
for i in range(1, n+1):
    print(" "*(n-i)+("*"*(2*i-1)))
```
