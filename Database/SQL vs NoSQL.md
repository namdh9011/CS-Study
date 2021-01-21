# SQL vs NoSQL

### 알아둘 것
- SQL은 Structured Query Language의 약자로, 그 자체가 DB가 아니다.
- SQL은 관계형 데이터베이스 관리 시스템(RDBMS)의 데이터를 관리하기 위해 설계된 특수 목적의 프로그래밍 언어라고 위키백과는 설명한다.
(RDBMS : relational database management system)
- 예전부터 DB는 SQL로 만들어졌기 때문에 SQL이 관계형 DB라는 의미로 사용되는 것이라 추측된다.
- SQL DB, NoSQL DB라고 표현해야 정확하지만 아래 정리되는 내용에는 SQL, NoSQL로 언급한다.
### 개요
웹 애플리케이션 개발을 위한 첫 걸음을 내딛은 이후에 한가지 선택사항을 마주하게 됩니다. MySQL와 같은 SQL을 사용할 것인가? 아니면 MongoDB같은 NoSQL을 사용할 것인가?
Node.js에 익숙하신 분들이라면 NoSQL (MongoDB)이 더 좋다는 인상을 가지고 계실지도 모르겠지만 잘못된 생각입니다.
이 글에서는 SQL과 NoSQL 데이터베이스의 핵심적인 개념을 소개하고 각 솔루션의 차이점 그리고 장단점을 설명하도록 하겠습니다. 


### SQL (관계형 데이터베이스)
SQL은 '구조화 된 쿼리 언어 (Structured Query Language)'의 약자입니다. 그러므로 데이터베이스 자체를 나타내는 것이 아니라, 특정 유형의 데이터베이스와 상호 작용하는 데 사용 하는 쿼리 언어입니다. (그러나 이 글에서는 SQL을 '관계형 데이터베이스' 라는 의미로도 사용합니다.)
SQL을 사용하면 관계형 데이터베이스 관리 시스템(RDBMS)에서 데이터를 저장, 수정, 삭제 및 검색 할 수 있습니다.
이러한 관계형 데이터베이스에는 두 가지 주요 특징이 있습니다.  

- 데이터는 **정해진(엄격한) 데이터 스키마 (= structure)**를 따라 데이터베이스 테이블에 저장됩니다.
- 데이터는 **관계**를 통해서 연결된 **여러개의 테이블에 분산**됩니다.

**1. 엄격한 스키마**

데이터는 테이블(table)에 레코드(record)로 저장되며, 각 테이블에는 명확하게 정의된 구조(structure)가 있습니다. (구조란 어떤 데이터가 테이블에 들어가고 어떤 데이터가 그렇지 않을지를 정의하는 필드(field) 집합을 가르킵니다.)

- 구조(structure)는 필드의 이름과 데이터 유형으로 정의됩니다.

![SQLvsNoSQL-1](https://raw.githubusercontent.com/Songwonseok/CS-Study/main/Database/images/SQLvsNoSQL-1.jpg)

(관계형 데이터베이스에서) 스키마를 준수하지 않는 레코드는 추가할 수 없습니다. 더 많은 필드를 얻고 싶다구요? 죄송합니다만 다른 테이블을 선택하셔야 합니다. 일부 필드가 누락 되었다구요? 아무튼 이 테이블은 안돼요! (예를 들어, 위 테이블에서 '유통 기한'이라는 필드를 넣고 싶다면, 스키마를 뜯어고치지 않는한 필드를 추가 할 수 없다는 겁니다.)

**2. 관계**

SQL 기반의 데이터 베이스의 또 다른 중요한 부분은 관계입니다.
데이터들을 여러개의 테이블에 나누어서, 데이터들의 중복을 피할 수 있습니다. 만약 사용자가 구입한 상품들을 나타내기 위해서는, Users(사용자), Products(상품), Orders(주문한 상품) 여러 테이블을 만들어야 하지만, 각각의 테이블들은 다른 테이블에 저장되지 않은 데이터 만을 가지고 있습니다. (중복된 데이터가 없습니다.) 

![SQLvsNoSQL-2](https://raw.githubusercontent.com/Songwonseok/CS-Study/main/Database/images/SQLvsNoSQL-2.jpg)

이런 명확한 구조는 장점이 있습니다. 하나의 테이블에서 중복없이 하나의 데이터만을 관리하기 때문에, 다른 테이블에서 부정확한 데이터를 다룰 위험이 없습니다.


### NoSQL (비관계형 데이터베이스)
NoSQL은 기본적으로 SQL(관계형 데이터베이스)와 반대되는 접근방식을 따르기 때문에 지어진 이름입니다.
- **스키마 없음**
- **관계 없음**

NoSQL세상에서는 레코드를 문서(documents)라고 부릅니다.
이것은 단순히 이름만 다른 것이 아니라, 핵심적인 차이점 이있습니다. **SQL 세상에서는 정해진 스키마를 따르지 않는다면 데이터를 추가 할 수 없지만, NoSQL에서는 다른 구조의 데이터를 같은 컬렉션(= SQL에서의 테이블)에 추가할 수 있습니다.**

![SQLvsNoSQL-3](https://raw.githubusercontent.com/Songwonseok/CS-Study/main/Database/images/SQLvsNoSQL-3.jpg)

문서는 JSON 데이터와 비슷한 형태를 가지고 있습니다. 그리고 앞서 말씀드린대로, 스키마에 대해서는 신경 쓸 필요가 없습니다.
또한 일반적으로 관련 데이터를 동일한 컬렉션에 넣습니다. (관계형 데이터베이스처럼 여러 테이블에 나누어 담지 않습니다.) 따라서 많은 Order(주문한 상품)이 있는 경우, 일반적인 정보를 모두 포함한 데이터를 Orders 컬렉션에 저장합니다. (즉, 관계형데이터 베이스에서 사용했던 Users나 Products 정보 또한 Orders에 포함해서 한꺼번에 저장됩니다.)
따라서 여러 테이블 / 콜렉션에 조인(join) 할 필요없이 이미 필요한 모든 것을 갖춘 문서를 작성하게 됩니다.
실제로 NoSQL 데이터베이스는 조인이라는 개념이 존재하지 않습니다.
(만약 조인을 하고 싶다면 직접 해당 외래키를 검색하여 사용할 수 있겠지만 일반적인 방법은 아닙니다.)
대신 컬렉션을 통해 **데이터를 복제**하여 각 컬렉션 일부분에 속하는 데이터를 정확하게 산출하도록 합니다.

![SQLvsNoSQL-4](https://raw.githubusercontent.com/Songwonseok/CS-Study/main/Database/images/SQLvsNoSQL-4.jpg)

이런 방식은 데이터가 중복되기 때문에 불안정한 측면이 있습니다. 실수로 컬렉션 B에서는 데이터를 수정하지 않았는데, 컬렉션 A에서만 데이터를 업데이트 할 위험이 있습니다.
특정 데이터를 같이 사용하는 모든 컬렉션에서, 똑같은 데이터 업데이트를 수행되도록 해야 합니다.
**그럼에도 불구하고, 이러한 방식의 커다란 장점은 복잡하고 (어떤 순간에는 느린) 조인을 사용할 필요가 없다는 것입니다.** 필요한 모든 데이터가 이미 하나의 컬렉션안에 저장되어 있기 때문입니다.
특히 자주 변경되지 않는 데이터 일때 더 큰 장점이 있습니다.


### 수직적(Vertical) & 수평적(Horizontal) 확장(Scaling)

두 종류의 데이터베이스를 비교 할 때 살펴 봐야할 또 하나의 중요한 개념은 확장(Scaling)입니다.
데이터베이스를 어떤 방식으로 확장 시킬 수 있을까요? (데이터베이스의 서버의 확장성 말입니다.)
확장은 **수직적(vertical) 확장**과 **수평적(horizontal) 확장**으로 구별 할 수 있습니다.
- **수직적 확장**이란 단순히 데이터베이스 서버의 성능을 향상시키는 것입니다. (예를 들어, CPU를 업그레이드 하는 방식으로 말이죠.)
- 반면에 **수평적 확장**은 더 많은 서버가 추가되고 데이터베이스가 전체적으로 분산됨을 의미합니다. 따라서 하나의 데이터베이스에서 작동하지만 여러 호스트에서 작동합니다.

![SQLvsNoSQL-5](https://raw.githubusercontent.com/Songwonseok/CS-Study/main/Database/images/SQLvsNoSQL-5.jpg)

**데이터가 저장되는 방식 때문에 SQL 데이터베이스는 일반적으로 수직적 확장만을 지원합니다. 수평적 확장은 NoSQL 데이터베이스에서만 가능합니다.**
SQL 데이터베이스는 '샤딩(Sharding)'의 개념을 알고 있지만 특정 제한이 있으며 구현하기가 대체로 어렵습니다. NoSQL 데이터베이스는 이를 기본적으로 지원하므로 여러 서버에서 데이터베이스를 쉽게 분리 할 수 있습니다.


### SQL vs NoSQL

앞서서 설명한 것들과 함께 생각해봅시다. 어떤 데이터베이스 솔루션을 사용해야 할까요?
이 질문에 확실한 **정답은 없습니다.**
SQL과 NoSQL은 모두 훌륭한 솔루션입니다. 두 가지 중 하나의 솔류션을 선택해야 되는 문제에서는 **어떤 데이터를 다루는지, 어떤 애플리케이션에서 사용되는지 고려**해야합니다. 

#### SQL의 장점
- 명확하게 정의 된 스키마, **데이터 무결성 보장**
- 관계는 각 데이터를 중복없이 한번만 저장됩니다.

#### NoSQL의 장점
- 스키마가 없기때문에, 훨씬 더 **유연**합니다. 즉, 언제든지 저장된 데이터를 조정하고 새로운 "필드"를 추가 할 수 있습니다.
- 데이터는 애플리케이션이 필요로 하는 형식으로 저장됩니다. 이렇게 하면 데이터를 읽어오는 **속도가 빨라**집니다.
- 수직 및 **수평 확장**이 가능하므로 데이터베이스가 애플리케이션에서 발생시키는 모든 읽기 / 쓰기 요청을 처리 할 수 있습니다.

#### SQL의 단점
- 상대적으로 덜 유연합니다. **데이터 스키마는 사전에 계획**되고 알려져야 합니다. (나중에 수정하기가 번거롭거나 불가능 할 수 도 있습니다.)
- 관계를 맺고 있기 때문에, **JOIN문이 많은 매우 복잡한 쿼리**가 만들어 질 수 있습니다.
- **수평적 확장이 어렵고**, 대체로 수직적 확장만 가능합니다. 즉 어떤 시점에서 (처리 할 수 있는 처리량과 관련하여) 성장 한계에 직면하게 됩니다.

#### NoSQL의 단점
- 유연성 때문에, 데이터 구조 결정을 하지 못하고 미루게 될 수 있습니다.
- 데이터 중복은 여러 컬렉션과 문서가 (SQL 세계에서 처럼 하나의 테이블에 하나의 레코드가 아니라) 여러 개의 레코드가 변경된 경우 업데이트를 해야 합니다.
- 데이터가 여러 컬렉션에 중복되어 있기 때문에, **수정(update)를 해야 하는 경우 모든 컬렉션에서 수행**해야 함을 의미합니다. (SQL 세계에서는 중복된 데이터가 없기 때문에 한번만 수행하면 됩니다.)


### 결론
#### SQL은 언제 사용하는 것이 좋을까요?
- 관계를 맺고 있는 데이터가 자주 변경(수정)되는 애플리케이션일 경우 (NoSQL에서라면 여러 컬렉션을 모두 수정해줘야만 합니다.)
- 변경될 여지가 없고, 명확한 스키마가 사용자와 데이터에게 중요한 경우

#### NoSQL은 언제 사용하는 것이 좋을까요?
- 정확한 데이터 구조를 알 수 없거나 변경 / 확장 될 수 있는 경우
- 읽기(read)처리를 자주하지만, 데이터를 자주 변경(update)하지 않는 경우 (즉, 한번의 변경으로 수십 개의 문서를 업데이트 할 필요가 없는 경우)
- 데이터베이스를 수평으로 확장해야 하는 경우 ( 즉, 막대한 양의 데이터를 다뤄야 하는 경우)

분명한 것은 데이터베이스는 다른 방식으로 설계 될 수 있다는 겁니다. NoSQL 데이터베이스를 쓰더라도 설계적으로 언급된 단점들을 완화시킬 수 있습니다. (예를들면 중복된 데이터를 줄이는 방법). SQL 데이터베이스도 마찬가지입니다. 요구사항을 만족시키고, 복잡한 JOIN문을 만들지 않도록 설계할 수 있습니다.\



### 추가
#### Property
**1. SQL - ACID properties**
- SQL은 ACID 특성을 따른다.
- ACID는 DB의 Transaction(트랜잭션)이 안전하게 수행된다는 것을 보장하기 위한 특징이다.
- 트랜잭션이란 여러 작업들을 하나로 묶은 단위이다.
- 하나로 묶인 작업들은 모두 실행되거나, 실행되지 않는다. (all-or-nothing)
(트랜잭션의 예시로 많이 나오는게 송금이다.
A은행에서 B은행으로 돈을 보낸다고 할때, A은행에서 출금을 한 순간 시스템이 중지했다.
그럼 B은행으로 송금을 안했기 때문에 A은행에서 출금된 돈은 사라진다...)

	- Atomicity(원자성)
: 트랜잭션의 작업이 부분적으로 실행되거나 중단되지 않는 것을 보장하는 것이다.
(불가능한 최소의 단위인 하나의 원자처럼 동작한다는 의미이다.)
	- Consistency(일관성)
: 미리 정의된 규칙에서만 수정이 가능한 특성을 의미한다.
(숫자 컬럼에 문자열값이 저장이 안되도록 보장한다.)
	- Isolation(고립성)
: 트랜잭션 수행시 다른 트랜잭션의 작업이 끼어들지 못하도록 보장하는 것이다.
	- Durability(영구성)
: 성공적으로 수행된 트랜잭션은 영원히 반영이 되는 것을 의미한다.
(한번 반영(commit)된 트랜젝션의 내용은 영원히 적용된다.)

**2. NoSQL - CAP theorem**

- NoSQL은 CAP이론을 따른다.
- CAP이론은 분산 시스템에서는 CAP 세 가지 속성 모두를 만족하는 것은 불가능하며,
오직 2가지만 만족할 수 있다는 것으로 정의할 수 있다.
- Consistency (일관성)
	: 모든 요청은 최신 데이터 또는 에러를 응답받는다.
(DB가 3개로 분산되었다고 가정할 때, 하나의 특정 DB의 데이터가 수정되면 나머지 2개의 DB에서도 수정된 데이터를 응답받아야 한다.)
- Availability (가용성)
	: 모든 요청은 정상 응답을 받는다. (특정 DB가 장애가 나도 서비스가 가능해야 한다.)
- Partitions Tolerance (분리 내구성)
	: DB간 통신이 실패하는 경우라도 시스템은 정상 동작 한다.

![SQLvsNoSQL-6](https://raw.githubusercontent.com/Songwonseok/CS-Study/main/Database/images/SQLvsNoSQL-6.png)
<br>
![SQLvsNoSQL-7](https://raw.githubusercontent.com/Songwonseok/CS-Study/main/Database/images/SQLvsNoSQL-7.png)

### 참고
- https://academind.com/tutorials/sql-vs-nosql/ - 원문 사이트
- https://siyoon210.tistory.com/130 - 번역한 포스팅
- https://velog.io/@thms200/SQL-vs-NoSQL - Property 참고