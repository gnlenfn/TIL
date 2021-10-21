# DFS

State: Complete
유형: Algorithm
작성일시: 2021년 10월 16일 오후 6:17

# DFS

- 깊이 우선 탐색
- 주로 스택이나 재귀로 구현

### 그래프 표현법

1. 인접 행렬

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

1. 인접 리스트
    
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
    

### DFS 문제 풀이

문제

[Subsets - LeetCode](https://leetcode.com/problems/subsets/)

풀이

```python
from typing import List

class Solution:
    def subsets(self, nums: List[int]) -> List[List[int]]:
        result = []
        
        def dfs(index, path):
            result.append(path)
            
            for i in range(index, len(nums)):
                dfs(i + 1, path + [nums[i]])
                
        dfs(0, [])
        return result
```

- 재귀로 구현한 DFS
- 재귀로 구현하면 간결한 코드가 되지만 한눈에 코드가 이해되지 않을 수 있다. (설명도 힘든듯..)
- 재귀 함수가 호출될 때 마다 현재 인덱스에서 마지막 인덱스까지 차례대로 포함하는 리스트를 추가하는 것
- 그리고 해당 인덱스에서 모두 추가되면 차례대로 dfs 밖으로 나오면서 다음 인덱스로 이동 (`for`의 `i` 값 이동)

### 가지치기로 최적화(백트래킹)

문제

[Course Schedule - LeetCode](https://leetcode.com/problems/course-schedule/)

풀이

```python
from typing import List
import collections

class Solution:
    def canFinish(self, numCourses: int, prerequisites: List[List[int]]) -> bool:
        course = collections.defaultdict(list)
        for a, b in prerequisites:
            course[a].append(b)
        
        check = set()
        visited = set()
        def dfs(c):
            if c in check:
                return False
            if c in visited:
                return True
            
            check.add(c)
            for y in course[c]:
                if not dfs(y):
                    return False
            
            check.remove(c)
            visited.add(c)
            return True
        
        for x in list(course):
            if not dfs(x):
                return False
        
        return True
```

1. 먼저 인접리스트 형태로 그래프를 구성
2. 순환구조를 판별하기 위해 이미 방문했던 노드는 `check`에 추가하여 이 경우는 `False` 리턴
3. 그리고 중복 체크를 피하기 위해 이미 방문한 노드는 `visited`에 추가하여 가지치기를 할 수 있도록 한다.
    1. 이때, `visited`에 노드를 추가하는 것은 모든 탐색이 끝난 후 추가하여 만약 중간에 `check`에 걸려 `False`가 반환되면 그대로 종료되어 추가되지 않도록 한다.
    2. 한 번 방문한 노드는 다시 가지 않도록 하는 것
4. `list(course)`를 쓰는 이유
    1. defaultdict를 사용했을 때, key에 없는 값은 기본값을 가지게 된다. 이때 딕셔너리의 요소가 추가되면서 반복문 내에서 `course`의 값이 변경되는 오류가 생긴다.
    2. 따라서 새로운 복사본을 만들어 값을 고정시키는 것이다.