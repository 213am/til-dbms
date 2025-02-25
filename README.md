# 데이터베이스 모델링 및 ERD 및 MySql 활용

- MySql(DBMS) 8.x 버전
  : RDBMS(관계형 데이터베이스 관리 시스템)

## 1. 요구사항 분석

- 회의 참석(회의록)
- 회의록 검토 후 각 사항을 요구사항 분석(요구사항정의서, 업무지시서)
  <br />

## 2. 요구사항 분석을 하는 이유

- 각 내용의 속성을 찾고 분류
- 분류 된 내용을 모아서 Entity 정의
- 각 Entity 간의 관계를 찾기
- 요구사항 정의서 작성

### 2.1. 요구사항 분석 예시

- 고객은 고객코드, 고객명, 전화번호, 이메일, 주소(기본주소, 상세주소), 지역, 가입일로 되어 있다.
- 고객은 지역별로 관리되도록 한다.
- 지역은 지역코드와 지역명으로 되어 있고, 지역명은 대한민국의 지역코드(02: 서울특별시)를 이용한다.
- 한 지역에는 여러 고객이 있을 수 있다.
- 제품은 제품코드, 제품명, 제품색상, 가격으로 되어 있다.
- 하나의 제품은 여러 색상을 가질 수 있다.
- 고객은 등록된 제품을 구매할 수 있다.
- 한 명의 고객은 여러 제품을 구매할 수 있고, 하나의 제품은 여러 고객이 구매할 수 있다.
- 고객이 제품을 구매 시 구매수량과 구매일자를 기록한다.

### 2.2. 요구사항 정의서 또는 업무 기술서(회사마다 포맷이 다름)

![업무기술서](https://github.com/user-attachments/assets/00e261ba-580a-4624-a5d1-006b0ecf52f8)

### 2.3. 속성(Attribute) 찾기 후 Entity 정의

- 설계 전문가는 Entity 정의 후 속성을 선별해나간다
- 신입 데이터 설계자는 Attribute 선별 후 Entity 정의

#### 2.3.1. 먼저 Entity 항목정리

- 명사소문자 추천

![속성 찾기](https://github.com/user-attachments/assets/751a552e-4866-4127-9f8a-97ca7036ea7f)

#### 2.3.2. 각 Entity 간의 관계정리

- 동사소문자 추천

![관계도](https://github.com/user-attachments/assets/62183626-77a2-4149-bc61-9f8f808abdd2)

<br/>

## 3. ERD 그리기

### 3.1.개념적 모델링

- Entity-Relationship-Diagram

![기본형태](https://github.com/user-attachments/assets/ea0410f8-ed1d-4424-b739-1a5fceceec37)

- 고객

![고객](https://github.com/user-attachments/assets/5dd6478c-843c-48a6-b4b4-a1a392b73ff4)

- 고객 PK 후보

![고객 PK 후보](https://github.com/user-attachments/assets/57f848fc-90a1-427b-8172-8fdf3d81a670)

- 지역

![지역](https://github.com/user-attachments/assets/9bb54756-d144-4cd3-b852-b0d95b000e2c)

- 제품

![제품](https://github.com/user-attachments/assets/e2a35f2e-3fb5-4001-86e3-6f20c7cecba3)

### 3.2. Realation 표현하기

- 개체와 개체가 맺고 있는 연관성을 표현

![Relation](https://github.com/user-attachments/assets/3b488f64-e688-458f-82b6-c2cc57a5568a)

#### 고객은 제품을 구매한다.

![고객-제품 관계](https://github.com/user-attachments/assets/7b231023-55ad-4538-8ad3-1051f3cbccef)

![최종](https://github.com/user-attachments/assets/e498ab6c-2d2f-4b29-b2a8-78cead7493bd)

<br/>

## 4. Logical Data Modeling(논리적 데이터 모델링)

- 개념적 schema 를 표 또는 테이블 형식으로 표현함
- Entity 의 속성 데이터 타입, 길이, null 허용여부, 기본값, 제약 조건 등을 세부적으로 작성 후 문서화
- 즉, `테이블 정의서`를 생성(이를 위한 도구는 다양함)

![테이블 정의서](https://github.com/user-attachments/assets/3af62455-5ae8-4673-b2c2-734a8240c400)
