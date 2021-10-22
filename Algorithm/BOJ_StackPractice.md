# 스택

State: Complete
유형: DataStructure
작성일시: 2021년 10월 22일 오전 10:55

[2504번: 괄호의 값](https://www.acmicpc.net/problem/2504)

- 백준의 괄호 문제
- 괄호는 보통 스택으로 쉽게 풀 수 있음
- 이 문제는 온전한 괄호쌍인지 판별하는 것과 동시에 각 괄호값을 더해야함

```python
def parentheses(case):
    pair = {
        "}" : "{",
        ")" : "("
    }
    stack = []
    answer = 0
    tmp = 1
    
    for idx, p in enumerate(case):
        if p in pair and (not stack or p != pair[p]):
            return 0 # 괄호쌍이 이루어지지 않음
        
        elif p == "(":
            stack.append(p)
            tmp *= 2  # 일반괄호 2점

        elif p == "[":
            stack.append(p)
            tmp *= 3  # 대괄호 3점

        elif p == ")":
            if case[idx - 1] == pair[p]: # 같은 종류의 괄호가 연속으로 나올때만 점수 추가
                answer += tmp
            stack.pop()
            tmp //= 2

        elif p == "]":
            if case[idx - 1] == pair[p]:
                answer += tmp
            stack.pop()
            tmp //= 3

    if stack:
        return 0

    return answer

if __name__ == "__main__":
    print(parentheses(input()))
```

- 아이디어 생각이 어려웠다
- 여는 괄호일때 2 or 3을 곱하고 괄호를 닫을때 지금까지의 `tmp`를 더한다
    - 이때 연속으로 같은 괄호가 나왔을 때만 더해야함
    - 괄호를 열었을때 괄호값만큼 더하는 것으로 보면 됨
- 직접 종이에 써보면 위의 아이디어 쉽게 이해됨