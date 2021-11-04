# 트라이 (Trie)

트라이는 **문자열을 빠르게 탐색하는 자료구조**이다. 문자열을 빠르게 탐색한다는 장점 외에도 문자열 관리에 이점이 있는 자료구조이기 때문에 형태소 분석기 등에서 활용한다.

# 작동원리

트라이는 주어진 문자열을 이루고 있는 문자를 앞에서부터 하나씩 노드를 생성해가며 만들어진다. 

> 1. 주어진 문자열에서 현재 문자를 가져온다.
> 2. 현재 문자로 이루어진 노드가 존재하면, 그 노드로 그 다음 문자열을 탐색하고, 노드가 없다면 그 노드를 새로 할당 받은 후 해당 노드를 통해 다음 문자열을 탐색한다.
> 3. 문자열의 마지막이 될 때까지 위 과정을 반복
 

트라이는 많이 봤던 이진 트리가 아닌 다진 트리가 된다. 

# 트라이 구현

먼저 트라이의 노드를 정의한다

```python
from collections import defaultdict

class TrieNode:
    def __init__(self):
        self.word = False
        self.children = defaultdict(TrieNode)
```

다음은 트라이 클래스와 단어를 삽입하는 메소드이다

```python
class Trie:
    def __init__(self):
        self.root = TrieNode()

    def insert(self, word):
        node = self.root
        for char in word:
            node = node.children[char]
        node.word = True # 주어진 문자열 끝까지 삽입하고나면 한 단어임을 표시
```

트라이노드가 딕셔너리로 정의되어있기 때문에 이미 존재하는 경로라면 노드가 이동하고 새로운 경로라면 딕셔너리에 새 값을 추가한다.

다음은 문자열이 존재하는지 찾는 `serach`메소드이다.

```python
    def search(self, word):
        node = self.root
        for char in word:
            if char not in node.children: # 자식노드가 없다? 없는 단어
                return False
            node = node.children[char]
        return node.word
```

마지막으로 prefix 등을 찾는 `startwith` 메소드이다.

```python
    def startwith(self, prefix):
        node = self.root
        for char in prefix:
            if char not in node.children:
                return False
            node = node.children[char]

        return True
```

`search`와 마찬가지로 주어진 prefix를 가진 자식 노드가 없다면 존재하지 않는 단어이므로 False 리턴하고 prefix를 무사히 찾는다면 (for 문을 무사히 빠져나오면) prefix가 존재하는 것이므로 True 리턴

### 전체 코드

```python
from collections import defaultdict

class TrieNode:
    def __init__(self):
        self.word = False
        self.children = defaultdict(TrieNode)

class Trie:
    def __init__(self):
        self.root = TrieNode()

    def insert(self, word: str) -> None:
        node = self.root
        for char in word:
            node = node.children[char]
        node.word = True

    def search(self, word: str) -> bool: # 찾는단어가 있는지 없는지 찾기
        node = self.root
        for char in word:
            if char not in node.children:
                return False
            node = node.children[char]
        return node.word

    def startsWith(self, prefix: str) -> bool: # 해당 문자열로 시작하는 단어 있는지 찾기
        node = self.root
        for char in prefix:
            if char not in node.children:
                return False
            node = node.children[char]
        
        return True
```

### 관련 문제

[Palindrome Pairs - LeetCode](https://leetcode.com/problems/palindrome-pairs/)