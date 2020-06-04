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
