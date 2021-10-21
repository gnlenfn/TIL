# 다익스트라

State: Complete
유형: Algorithm
작성일시: 2021년 10월 19일 오후 5:38

- 최단 경로 문제를 푸는 알고리즘 중 하나
- 항상 노드 주변의 최단 경로만을 택하는 그리디 알고리즘
- BFS를 기반으로 사용
    - 마치 교차로가 나올 때 마다 갈라져서 길을 찾는 것과 비슷
- 가중치가 음수인 경우 사용할 수 없음

### 예시 문제

[Network Delay Time - LeetCode](https://leetcode.com/problems/network-delay-time/)

이 문제는 2가지 사항을 판별해야 한다

> 1. 모든 노드가 신호를 받는데 걸리는 시간
2. 모든 노드에 도달할 수 있는지 여부
> 

1번은 다익스트라 알고리즘으로 알 수 있음

2번이 거짓이면 -1을 리턴해야 함

```python
class Solution:
    def networkDelayTime(self, times: List[List[int]], n: int, k: int) -> int:
        graph = collections.defaultdict(list)
        for source, target, weight in times:
            graph[source].append((target, weight))
            
        Q = [(0, k)]
        dist = collections.defaultdict(int)
        while Q:
            time, node = heapq.heappop(Q)
            if node not in dist:
                dist[node] = time
                for v, w in graph[node]:
                    alt = time + w
                    heapq.heappush(Q, (alt, v))
                    
        if len(dist) == n:
            return max(dist.values())
        
        return -1
```

1. input의 형식이 a에서 b까지 w의 가중치를 가진다는 의미로 `[a, b, w]`가 포함된 리스트가 들어온다
    1. 이것을 인접리스트 형태로 변환해준다
    2. value 리스트의 요소는 `(도착지, 가중치)` 형태의 튜플을 삽입
2. `Q` 변수는 BFS를 위한 큐이고 (소요시간, 정점)으로 구성한다, 최적화를 위해 `heapq` 사용
3. `dist`는 해당 노드까지의 거리를 저장 —> 위에서 말한 2번을 체크하기 위함
4. 이제 너비 우선 탐색 시작
    1. 순회를 시작하면 큐의 최소값을 추출 (`heappop`)
    2. 해당 노드가 `dist`에 없으면 ( == 방문한 적 없으면) 그 노드에서 갈 수 있는 모든 노드를 큐에 삽입한다 (`heappush`)
    3. 현재 노드까지 소요시간 + 다음 노드까지 걸리는 시간이 다음 소요시간으로 들어감
5. 만약 `dist`의 요소 개수가 전체 노드 수와 같지 않으면, 모든 노드에 도달하지 못한 경우
6. 전체 노드 수와 같을 때만 최대 소요 시간을 반환