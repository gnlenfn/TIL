# [프로그래머스] 네트워크

State: Complete
작성일시: 2021년 10월 17일 오후 6:46

[코딩테스트 연습 - 네트워크](https://programmers.co.kr/learn/courses/30/lessons/43162)

- DFS 문제풀이
- Floodfill 문제와 매우 유사하다
    - 하지만 보통 Floodfill 문제에서 주어지는 array와 다르게 인접행렬이 주어졌다
    - 따라서 일반 Floodfill에서는 `i`에서 `i+3`으로 가는게 불가능하지만 이 문제에서는 가능할 수 있다. 그에따라 `visited`는 보통 똑같이 2차원 행렬로 만들었지만 이 문제에서는 노드의 수 만큼 길이를 가진 1차원 array로 만든다
    - 현재 노드에서 갈 수 있는 노드를 모두 순회하면서 방문하지 않았고, `computers[현재노드][다음노드]`가 1인 경우에 `visited`에 방문을 체크하고 재귀함수를 호출한다

```python
def solution(n, computers):
    visited = [False] * n

    def dfs(i, graph, visited):
        for next_v in range(n):
            if not visited[next_v] and graph[i][next_v]:
                visited[next_v] = True
                dfs(next_v, graph, visited)        
        
    count = 0
    for i in range(n):
        if not visited[i]:
            dfs(i, computers, visited)
            count += 1
    
    return count
```

## 인접행렬과 인접리스트

그래프 관련 문제에서 그래프를 표현하는 두 가지 방법이다

### 인접 행렬

1. 인접 행렬은 그래프의 연결 관계를 이차원 행렬로 표현하는 것이다. 

```python
graph = [
	[0, 1, 1, 1, 0, 0, 0],
	[0, 0, 0, 0, 1, 0, 0],
	[0, 0, 0, 0, 1, 0, 0],
	[0, 0, 0, 0, 0, 0, 0],
	[0, 0, 0, 0, 0, 1, 0],
	[0, 0, 0, 0, 0, 0, 0],
	[0, 0, 1, 0, 0, 0, 0]
]
```

1. 무방향 그래프의 경우 대각성분을 기준으로 대칭을 이룬다.
2. 장단점
    1. 장점
        - 구현이 쉬움
        - 두 노드가 연결된 상태인지 확인할 때 O(1)의 시간복잡도를 가짐
    2. 단점
        - 노드 `i`에 연결된 노드를 모든 노드를 방문하려 할 떄, 모든 모드를 방문해야 하기 때문에 O(V)의 시간이 걸림 (V는 전체 노드의 수)
        - 노드는 많고 간선은 적은 경우 매우 비효율적

### 인접리스트

1. 인접 리스트를 구현할 때 Python에서는 dictionary 자료형을 사용
2. 간선에 가중치가 있으면 리스트의 요소로 튜플 등을 사용하면 됨

```python
graph = {
	1: [2, 3, 4],
	2: [5],
	3: [5],
	4: [],
	5: [6, 7],
	6: [],
	7: [3]
}
```

1. 장단점
    1. 장점
        - 실제로 연결된 노드의 정보만 저장하기 때문에 간선의 개수에 비례하는 메모리만 사용
        - 전체 노드를 탐색할 때 인접행렬은 O(V^2)만큼 시간이 걸리지만 인접리스트는 O(E)만큼만 걸린다. (E는 간선의 수)
    2. 단점
        - 노드 `i`와 노드 `j`가 연결됐는지 알고 싶다면 노드 `i`의 리스트를 모두 순회하면서 `j`가 있는지 확인해야 한다. O(V)의 시간이 걸린다

인접 행렬과 인접 리스트는 서로의 단점을 보완하는 방식이다. 따라서 문제의 상황에 따라 적절한 표현법을 사용할 수 있어야 한다.