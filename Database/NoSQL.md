# NoSQL?

Not Only SQL. 지금까지 많이 사용되던 RDBMS의 특징들 외에 다른 특성들을 가진 데이터베이스를 말한다. 기존의 관계형 데이터베이스 시스템이 가진 ACID 특성을 제공하지 않고 뛰어난 확장성, 성능 등을 가진 데이터베이스를 가리킨다.

# RDBMS와의 차이

- 스키마가 없이 자유로운 데이터 구조를 가지기 때문에 더 유연하게 확장 가능
- 데이터 분산처리가 용이하고 성능 향상을 위한 scale-up 가능
- RDBMS의 레코드를 Documnet라고 함

# NoSQL의 특징

- 관계형 스키마가 없고 테이블간의 조인 기능 없음
- 직접 프로그래밍 하는 등 SQL query대신 다른 방식의 인터페이스 사용
- 여러 대의 데이터베이스 서버를 묶어 하나의 데이터베이스로 구성 가능 → 분산형
- 관계형 데이터베이스에서 지원하는 데이터 처리의 완결성 미보장 → 단점?
- 많은 경우 오픈 소스
- 높은 확장성, 가용성, 성능

하나의 NoSQL이 위의 모든 특징을 가지는 것이 아니고 각각의 특징이 있다고 생각할 수 있다. 

# NoSQL 예시

1. Key-Value DB
    - 가장 단순한 형태로 key-value쌍이 저장되는 형태
2. Wide Columnar Store
    - Big Table DB라고도 하며 key value에서 발전된 Column Family의 형태
3. Document DB
    - JSON, XML같은 collection 데이터 모델 구조의 DB
4. Graph DB

![Wikipedia](https://image.samsungsds.com/kr/insights//08_02.JPG?queryString=20211108032649)
Wikipedia

대표적으로 많이 사용되는 DB는 Document 타입의 MongoDB, Wide Columnar Store 타입의 HBase과 Cassandra가 있다. 

# RDBMS/NoSQL의 장단점

### SQL

- 장점
    - 명확하게 정의된 스키마 → 데이터 무결성 보장
    - 각 데이터가 중복없이 저장되는 것이 보장됨
- 단점
    - 스키마 수정이 어려움, 사전에 잘 계획되어야 함
    - 테이블이 많아지면 JOIN이 많은 복잡한 쿼리 생길 수 있음
    - 수직적 확장만 가능
- 관계를 맺고있는 데이터가 자주 변경될때 혹은 변경의 여지가 없고 명확한 스키마가 있을 때 사용하는 것이 유리

### NoSQL

- 장점
    - 스키마가 없기 때문에 유연하고 언제든지 데이터를 수정하고 새로운 필드 추가 가능
    - 수직, 수평적 확장이 가능 → 대용량 데이터 처리에 훨씬 유리
- 단점
    - 중복된 데이터를 저장할 수도 있고 중복 데이터가 수정되면 전체에서 수정하는 것이 쉽지 않음 → ACID 보장 못함
- 정확한 데이터 구조를 알 수 없거나 변경될 수 있는 경우
- 읽기는 자주 하지만 변경은 자주 없는 경우
- 데이터 크기가 매우 커서 수평적 확장이 필요한 경우 NoSQL을 사용하는 것이 유리

---

수직적 확장: 서버의 스펙 상승

수평적 확장: 여러 대의 서버를 만들어 성능 향상