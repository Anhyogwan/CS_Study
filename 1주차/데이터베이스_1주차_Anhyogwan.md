Q. RDBMS와 NoSQL의 차이에 대해 설명해주세요.

RDBMS는 모든 데이터를 2차원 테이블 형태로 표현합니다.
장점 : 스키마에 맞춰 데이터를 관리하기 때문에 데이터의 정합성을 보장할 수 있다.
단점 : 시스템이 커질 수록 쿼리가 복잡해지고 성능이 저하되며 Scale-out이 어렵다(Scale-up만 가능)

NoSQL(Not Only SQL)은 RDBMS와 반대로 데이터간의 관계를 정의하지 않고, 스키마가 없어 좀 더 자유롭게 데이터를 관리할 수 있으며, 컬렉션이라는 형태로 데이터를 관리합니다.

장점 : 스키마 없이 Key-Value 형태로 데이터를 관리해 자유롭게 데이터를 관리할 수 있다
데이터 분산이 용이하여 성능 향상을 위한 scale-up 뿐만아닌 scale-out 또한 가능하다.
단점 : 데이터 중복이 발생할 수 있고, 중복된 데이터가 변경될 경우 수정을 모든 컬렉션에서 수행해야 한다.
스키마가 존재하지 않기에 명확한 데이터 구조를 보장하지 않아 데이터 구조 결정이 어려울 수 있다.



Q. RDBMS와 NoSQL은 어느 경우에 적합한가요?

RDBMS는 데이터 구조가 명확하고, 변경 될 여지가 없으며 스키마가 중요한 경우 사용하는 것이 좋습니다. 또한 중복된 데이터가 없어(데이터 무결성) 변경이 용이하기 때문에 관계를 맺고 있는 데이터가 자주 변경이 이루어지는 시스템에 적합합니다.

NoSQL은 정확한 데이터 구조를 알 수 없고 데이터가 변경/확장 될 수 있는 경우 사용하는 것이 좋습니다. 또한 단점에서도 명확하듯 데이터 중복이 발생할 수 있으며 중복된 데이터가 변경될 시 모든 컬렉션에서 수정해야 하기 때문에 Update가 많이 이루어지지 않는 시스템에 좋으며, Scale-out이 가능하다는 장점을 활용해 막대한 데이터를 저장해야 해서 DB를 Scale-out 해야 되는 시스템에 적합합니다.




Q. Index에 대해 설명해주시고, 장/단점에 대해 아는대로 말해주세요.
Index란 테이블을 처음부터 끝까지 검색하는 방법인 FTS(Full Table Scan)과는 달리 인덱스를 검색하여 해당 자료의 테이블을 엑세스 하는 방법입니다.
예를들어, DB를 책으로 비유하면 데이터는 책의 내용일 것이고, 데이터가 저장된 레코드의 주소는 index 목록에 있는 페이지 번호일 것이다.
인덱스는 항상 정렬된 상태를 유지하기 때문에 원하는 값을 검색하는데 빠르지만, 새로운 값을 추가하거나 삭제, 수정하는 경우에는 쿼리문 실행 속도가 느려집니다.
즉, 인덱스는 데이터의 저장 성능을 희생하고 그대신 데이터의 검색 속도를 높이는 기능이라 할 수 있습니다.

Q. 그렇다면 DBMS는 Index를 어떻게 관리하고 있나요? (Index 자료구조)
1. B+Tree 인덱스 자료구조
자식 노드가 2개 이상인 B-Tree를 개선시킨 자료구조이며,
BTree 리프노드들을 LinkedList로 연결하여 순차 검색을 용이하게 합니다. 해시 테이블보다 나쁜 O(log2N)의 시간복잡도를 갖지만 일반적으로 사용되는 자료구조입니다.

2. 해시 테이블
컬럼의 값으로 생성된 해시를 기반으로 인덱스를 구현합니다.
시간복잡도가 O(1)이라 검색이 매우 빠릅니다.
부등호(<,>)와 같은 연속적인 데이터를 위한 순차 검색이 불가능하기 때문에 사용에 적합하지 않습니다.



Q. 정규화(Normalization)에 대해 설명해주세요.

하나의 릴레이션에 하나의 의미만 존재하도록 릴레이션을 분해하는 과정이며, 데이터의 일관성, 최소한의 데이터 중복, 최대한의 데이터 유연성을 위한 방법입니다.

제1 정규형 : 테이블의 컬럼이 원자 값(Atomic Value; 하나의 값)을 갖도록 분해합니다.

제2 정규형: 제1 정규형을 만족하고, 기본키가 아닌 속성이 기본키에 완전 함수 종속이도록 분해합니다.
※ 여기서 완전 함수 종속이란 기본키의 부분집합이 다른 값을 결정하지 않는 것을 의미


제3 정규형 : 제2 정규형을 만족하고, 이행적 함수 종속을 없애도록 분해합니다.
※ 여기서 이행적 종속이란 A → B, B → C가 성립할 때 A → C가 성립되는 것을 의미


BCNF 정규형 : 제3 정규형을 만족하고, 함수 종속성 X → Y가 성립할 때 모든 결정자 X가 후보키가 되도록 분해합니다.



Q. 정규화에는 어떤 장점이 있고 어떤 단점이 있는지 아는대로 설명해주세요.

장점
1. 데이터베이스 변경 시 이상현상이 발생하는 문제점을 해결할 수 있다.
2. 데이터베이스 구조 확장 시 정규화된 데이터베이스는 그 구조를 변경하지 않아도 되거나 일부만 변경해도 된다.

단점
릴레이션의 분해로 인해 릴레이션 간의 연산(JOIN 연산)이 많아진다. 이로인해 질의에 대한 응답 시간이 느려질 수 있다.

+ 정규화를 수행한다는 것은 이상현상을 제거하는 것이다. 데이터의 중복 속성을 제거하고 결정자에 의해 동일한 의미의 일반 속성이 하나의 테이블로 집약되므로 한 테이블의 데이터 용량이 최소화되는 효과가 있다. 따라서 정규화된 테이블은 데이터를 처리할 때 속도가 빨라질 수도 있고 느려질 수도 있는 특성이 있다.

 

Q. 역정규화를 하는 이유에 대해 아는대로 설명해주세요.
정규화를 거치면 릴레이션 간의 연산(JOIN 연산)이 많아지는데, 이로인해 성능이 저하될 우려가 있습니다.

역정규화를 하는 가장 큰 이유는 성능 문제가 있는(읽기작업이 많이 필요한) DB의 전반적인 성능을 향상시키기 위함입니다.



Q. 트랜잭션이란 무엇인지 설명해주세요.
트랜잭션은 작업의 완전성을 보장해줍니다.
즉, 작업들을 모두 처리하거나 처리하지 못할 경우 이전 상태로 복구하여 작업의 일부만 적용되는 현상이 발생하지 않게 만들어주는 기능입니다.
하나의 트랜잭션은 Commit(작업완료)되거나 Rollback(취소)됩니다.

Q. 트랜잭션의 특성(ACID)에 대해 설명해주세요.
1. 원자성(Atomicity) 작업이 모두 반영되던지 아니면 전혀 반영되지 않아야 한다.

2. 일관성(Consistency) 실행이 완료되면 언제나 일관성 있는 상태를 유지해야 한다.

3. 독립성(Isolation) 둘 이상 트랜잭션이 동시에 실행될 경우 서로의 연산에 끼어들 수 없다.

4. 영속성(Durability) 완료된 결과는 영구적으로 반영되어야 한다.


Q. Elasticsearch란?

Elasticsearch는 Apache Lucene( 아파치 루씬 ) 기반의 Java 오픈소스 분산 검색 엔진입니다.
Elasticsearch를 통해 루씬 라이브러리를 단독으로 사용할 수 있게 되었으며, 방대한 양의 데이터를 신속하게, 거의 실시간( NRT, Near Real Time )으로 저장, 검색, 분석할 수 있습니다.

Q. Elastic Search의 키워드 검색과 RDBMS의 LIKE 검색의 차이에 대해 설명해주세요.
RDBMS는 단순 텍스트매칭에 대한 검색만을 제공해 동의어나 유의어 같은 검색은 불가능합니다.
(MySQL 최신 버전에서 n-gram 기반의 Full-Text 검색을 지원하긴 하지만, 한글 검색의 경우 아직 많이 빈약한 감이 있습니다.)
하지만 엘라스틱 서치는 동의어나 유의어를 활용한 검색이 가능하며, 비정형 데이터의 색인과 검색이 가능하고, 역색인 지원으로 매우 빠른 검색이 가능합니다.
※ Full-Text : 이미지, CSS, 글 등의 복합적으로 이뤄진 컨텐츠에서 순수하게 텍스트만 추출한 데이터를 의미. 이 과정을 보통 크롤링으로 구현함 ( 엘라스틱 서치의 검색엔진엔 크롤러가 빠져있어 별도로 구축해야함)
