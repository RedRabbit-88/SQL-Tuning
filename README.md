# SQL-Tunning

## SQL 최적화 과정

**1. SQL 파싱 (Parsing)**

* 파싱 트리 생성 : SQL 문을 이루는 개별 구성요소를 분석해서 파싱 트리 생성
* Syntax 체크 : 문법적 오류가 없는지 확인 ex) FROM 절 구문 확인
* Semantic 체크 : 의미상 오류가 없는지 확인 ex) 테이블 존재유무 확인

**2. SQL 최적화**

* 옵티마이저(Optimizer)가 미리 수집한 시스템 및 오브젝트 통계정보를 바탕으로 다양한 실행경로를 생성해서 비교한 후 가장 효율적인 하나를 선택

**3. 로우 소스 생성**

* 옵티마이저가 선택한 실행경로를 실제 실행 가능한 코드 또는 프로시저 형태로 포맷팅하는 단계


## 힌트 목록

분류|힌트|설명
--|--|--
최적화 목표|ALL_ROWS|전체 처리속도 최적화
||FIRST_ROWS(N)|최초 N건 응답속도 최적화
액세스 방식|FULL|Table Full Scan으로 유도
||INDEX|Index Scan으로 유도
||INDEX_DESC|Index를 역순으로 스캔하도록 유도
||INDEX_FFS|Index Fast Full Scan으로 유도
||INDEX_SS|Index Skip Skan으로 유도
조인순서|ORDERED|FROM절에 나온 순서대로 조인
||LEADING|LEADING 힌트 괄호에 기술한 순서대로 조인<br>ex) LEADING(T1 T2)
||SWAP_JOIN_INPUTS|해시 조인 시, BUILD INPUT을 명시적으로 선택<br>ex) SWAP_JOING_INPUTS(T1)
조인방식|USE_NL|NL 조인으로 유도
||USE_MERGE|소트 머지 조인으로 유도
||USE_HASH|해시 조인으로 유도
||NL_SJ|NL 세미조인으로 유도
||MERGE_SJ|소트 머지 세미조인으로 유도
||HASH_SJ|해시 세미조인으로 유도
서브쿼리<br>팩토링|MATERIALIZE|WITH 문으로 정의한 집합을 물리적으로 생성하도록 유도<br>`ex) WITH /*+ MATERIALIZE */ T AS (SELECT)`
||LINE|WITH 문으로 정의한 집합을 물리적으로 생성하지 않고 INLINE 처리하도록 유도<br>`ex) WITH /*+ INLINE */ T AS (SELECT)`
쿼리 변환|MERGE|뷰 머징 유도
||NO_MERGE|뷰 머징 방지
||UNNEST|서브쿼리 Unnesting 유도
||NO_UNNEST|서브쿼리 Unnesting 방지
||PUSH_PRED|조인조건 Pushdown 유도
||NO_PUSH_PRED|조인조건 Pushdown 방지
||USE_CONCAT|OR 또는 IN-LIST 조건을 OR-Expansion으로 유도
||NO_EXPAND|OR 또는 IN-LIST 조건을 OR-Expansion으로 방지
병렬 처리|PARALLEL|테이블 스캔 또는 DML을 병렬방식으로 처리하도록 유도<br>`ex) PARALLEL(T1 2) PARALLEL(T2 2)`
||PARALLEL_INDEX|인덱스 스캔을 병렬방식으로 처리하도록 유도
||PQ_DISTRIBUTE|병렬 수행 시 데이터 분배 방식 결정<br>`ex) PQ_DISTRIBUTE(T1 HASH HASH)`
기타|APPEND|Direct-Path Insert로 유도
||DRIVING_SITE|DB Link Remove 쿼리에 대한 최적화 및 실행 주체 지정(Local 또는 Remote)
||PUSH_SUBQ|서브쿼리를 가급적 빨리 필터링하도록 유도
||NO_PUSH_SUBQ|서브쿼리를 가급적 늦게 필터링하도록 유도
