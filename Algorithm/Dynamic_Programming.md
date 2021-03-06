# 다이나믹 프로그래밍?

- 다이나믹 프로그래밍은 **하나의 문제는 단 한번만 풀도록 하는 알고리즘**
- 피보나치 수열은 D[i] = D[i - 1] + D[i - 2] 라는 점화식으로 나타낼 수 있음
    - 이때 반복적으로 같은 값을 구해야 하기 때문에 비효율이 나타남
    - 큰 문제를 작은 문제로 분할하여 분할 정복과 비슷하지만 분할 정복은 위의 예시 처럼 반복의 비효율이 나타날 수 있음

## 메모이제이션

- 다이나믹 프로그래밍은 메모이제이션을 사용하여 이미 계산한 결과는 저장하여 필요할 때 단순히 반환하도록 한다

```python
dp = [0] * 100

def fibonacci(n):
    if n == 1: return 1
    if n == 2: return 1
    if dp[n] != 0: return dp[n]
    dp[n] = fibonacci(n-1) + fibonacci(n-2)
    return dp[n]

print(fibonacci(25))
```

단순 재귀함수로 구현하면 100번째 수까지 못구할지도 모름