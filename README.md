# MariaDB

- MySQL 은 유료
- MySQL 이 유료로 바뀌기 전에 git 을 Folk 해서 만들어진 것이 MariaDB
- 문법이 99.9% 동일

[공식사이트](https://mariadb.org/download/?os=windows&cpu=x86_64&pkg=msi&mirror=blendbyte&t=mariadb&p=mariadb&r=11.7.2)

## 설치 시 주의 사항

- port 충돌 : `3308` 번으로 변경(3306 - MySql 용 포트 충돌)
- pw : 1234
- 설치 중 한글 사용 체크
  - Use UTF8 as default character set and collation
    - 문자를 입력할때 한글 및 다양한 언어들이 정상적으로 입력되도록 하는 옵션

## Path 설정

- 하단의 윈도우 검색창에서 `환경 변수 편집` 검색 후 실행
- `환경 변수` > `시스템 변수` > `Path 변수` 수정
- 새로만들기로 `C:\Program Files\MariaDB 11.X\bin` 추가

## SQL 구문으로 schema 즉, database 생성하기

```sql
-- 데이터베이스 목록 보기
show databases;

-- 데이터베이스 즉, schema 만들기
create database board;

-- 데이터베이스 목록 보기
show databases;
```

## SQL 구문으로 schema(database) 안에 Table 생성 및 컬럼명, 컬럼 속성 세팅

```sql
-- schema 에 표 생성하기
-- 어느 schema 를 쓸지 결정을 해주어야 한다
use board;
```

- author 테이블 생성하기

```sql
-- create table 테이블명
create table author(
id int primary key,   -- pk 로 항목의 제약조건을 지정
name varchar(100),
email varchar(30),
password varchar(20)
);
```

- 실행된 sql 구문 보기

```sql
-- 실행이 된 쿼리 다시 보기
show create table author
```

- 실행이 이루어진 구문

```sql
CREATE TABLE `author` (
   `id` int(11) NOT NULL,
   `name` varchar(100) DEFAULT NULL,
   `email` varchar(30) DEFAULT NULL,
   `password` varchar(20) DEFAULT NULL,
   PRIMARY KEY (`id`)
 ) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_uca1400_ai_ci
```

- posts 테이블 만들기

```sql
-- board schema(database) 에 posts 테이블 생성하기
CREATE TABLE `author` (
  `id` int(11) NOT NULL,
  `name` varchar(100) DEFAULT NULL,
  `email` varchar(30) DEFAULT NULL,
  `password` varchar(20) DEFAULT NULL,
  PRIMARY KEY (`id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_uca1400_ai_ci
```

- 실행이 이루어진 구문

```sql
CREATE TABLE `posts` (
  `id` int(11) NOT NULL,
  `title` varchar(255) DEFAULT NULL,
  `content` varchar(3000) DEFAULT NULL,
  `author_id` int(11) NOT NULL,
  PRIMARY KEY (`id`),
  KEY `author_id` (`author_id`),
  CONSTRAINT `posts_ibfk_1` FOREIGN KEY (`author_id`) REFERENCES `author` (`id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_uca1400_ai_ci
```

- Table 구조 살펴보기

```sql
-- 만들어진 table 구조 살펴보기
describe author;
describe posts;
```

## 테이블 및 속성 변경 문법 ( ALTER )

- 테이블명 변경하기

```sql
-- 테이블명 변경하기
use 스키마명;

use board; -- board schema 사용하겠다는 쿼리

alter table 테이블명 rename 새테이블명;
```

- 테이블에 컬럼 추가하기

```sql
alter table 테이블명 add column 컬럼명 테이터타입;
```

- 테이블에 컬럼 삭제하기

```sql
alter 테이블명 drop column 컬럼명;
```

- 상세정보 보기

```sql
describe author;
```

- 컬럼명 변경하기

```sql
alter table 테이블명 change colum 칼럼명 새칼럼명 데이터타입;
```

- 특정 컬럼에 속성을 변경하기

```sql
alter table 테이블명 modify column 컬럼명 데이터타입;

-- author 테이블에 email 컬럼 속성 변경하기
alter table author modify column email varchar(30) not null;

-- 상세정보 보기
describe author;

-- posts 테이블에 title 컬럼의 속성 변경하기
alter table posts modify column title varchar(255) not null;

-- 상세정보 보기
describe posts;
```

## 데이터 추가 ( INSERT )

- 테이블에 새로운 데이터 (레코드) 추가

```sql
insert into 테이블명 (컬럼명, 컬럼명, ...) values (값, 값, ...);


describe author;


-- 레코드 추가하기
insert into author (id, name, email, password) values (1, "홍길동", "hong@naver.com", "1234");

-- 레코드 내용 전체 출력
select * from author;

describe posts;

-- author 테이블에 id 가 존재하는 레코드를 posts 에 추가하기
insert into posts (id, title, contents, author_id) values (1, "react","react...",1);

-- 전체 레코드 출력
select * from posts;

-- author 테이블에 id 가 존재하지 않는 경우 레코드를 posts 에 추가하기
insert into posts (id,title,contents,author_id) values (2,"java", "jaja...",2);	-- 거부됨

-- 전체 레코드 출력 ( 변화 없음 )
select * from posts;
```

## 데이터 수정 ( UPDATE )

```sql
-- 추가 레코드 입력
insert into author (id, name, email, password ) values (2, '박길동', 'park@naver.com', '1234' );
insert into author (id, name, email, password ) values (3, '최길동', 'choi@naver.com', '1234' );

-- 전체 레코드 출력
select * from author;

update 테이블명 set 컬럼명=값;
update 테이블명 set 컬럼명=값 where 조건;

-- Editor 에서 Safe Update Mode 가 Where 절을 요구하도록 셋팅됨. (SET SQL_SAFE_UPDATES = 0)
update author set email="a@a.net"; -- 실행 안됨
update author set email="a@a.net" where id=1; -- 실행 가능

-- 전체 레코드 출력
select * from author;
```

## 데이터 삭제 ( DELETE )

- where 조건은 필수입니다
- where 가 없으면 전체가 대상이 됩니다

```sql
delete from 테이블명 where 조건;
delete from 테이블명 where 필드이름=값;

-- 전체 레코드 출력
select * from author;

-- author 테이블에서 id 가 2인 레코드 삭제
delete from author where id=2;

-- 전체 레코드 출력
select * from author;
```

## 삭제에 관해서

# 🔹 DELETE vs TRUNCATE vs DROP 비교

## ✅ `DELETE FROM 테이블명`

- **특정 데이터만 삭제 가능** (`WHERE` 절 사용 가능).
- 삭제된 데이터는 **롤백 가능** (트랜잭션을 사용하면 `ROLLBACK` 가능).
- **로그 기록이 남아 속도가 느릴 수 있음**.
- **AUTO_INCREMENT 값이 유지됨** (새 데이터 삽입 시 기존 값 이후로 증가).
- **Foreign Key 제약을 준수하며 삭제 가능**.

## ✅ `TRUNCATE TABLE 테이블명`

- **테이블의 모든 데이터를 삭제하지만, 테이블 구조는 유지됨**.
- **WHERE 절 사용 불가능** (테이블 전체 데이터만 삭제 가능).
- **롤백 불가능한 경우가 많음** (DBMS에 따라 다름).
- **로그 최소화로 DELETE보다 빠름**.
- **AUTO_INCREMENT 값이 초기화됨**.
- **Foreign Key 제약이 있으면 실행이 제한될 수 있음**.

## ✅ `DROP TABLE 테이블명`

- **테이블과 모든 데이터를 완전히 삭제**.
- **테이블 자체가 삭제되므로 다시 사용하려면 새로 생성해야 함**.
- **롤백 불가능**.
- **Foreign Key 제약이 걸려 있다면 먼저 제거해야 실행 가능**.

---

## 🚀 DELETE vs TRUNCATE vs DROP 차이점

| 구분                  | `DELETE FROM`              | `TRUNCATE TABLE`             | `DROP TABLE`        |
| --------------------- | -------------------------- | ---------------------------- | ------------------- |
| 데이터 삭제           | ✅ (선택적 삭제 가능)      | ✅ (전체 삭제)               | ✅ (전체 삭제)      |
| 테이블 구조 유지      | ✅                         | ✅                           | ❌ (완전히 삭제)    |
| `WHERE` 절 사용 가능  | ✅                         | ❌                           | ❌                  |
| 속도                  | 느림 (로그 기록)           | 빠름                         | 가장 빠름           |
| 롤백 가능 여부        | ✅ (트랜잭션 사용 시 가능) | ❌ (DBMS에 따라 다름)        | ❌                  |
| AUTO_INCREMENT 초기화 | ❌ (유지됨)                | ✅ (초기화됨)                | N/A (테이블 삭제됨) |
| Foreign Key 제약      | ✅ (제약 준수)             | ⚠️ (제약이 있으면 실행 불가) | ❌ (먼저 삭제 필요) |

👉 **정리**

- `DELETE` → **특정 데이터 삭제**(로그 기록됨, 트랜잭션 가능).
- `TRUNCATE` → **전체 데이터 삭제**(빠름, 테이블 구조 유지, AUTO_INCREMENT 초기화).
- `DROP` → **테이블 자체 삭제**(완전히 제거됨, 다시 생성해야 함).

## 데이터 조회 ( SELECT ) 구문

- 개발자가 가장 많이 사용하는 구문
- 복잡한 옵션으로 값 추출

```sql
select * from 테이블명;

-- 전체 레코드 출력
select * from author;
```

```sql
select 컬럼, 컬럼
from 테이블명
where 조건;

-- 전체 레코드 출력
select * from author;

-- 컬럼별로 뽑기
select id, name from author;

-- where 조건으로 뽑기
select * from author where id=1;
select email, name from author where id = 1;

-- 비교문 쓰기
select * from author where id > 1;
select * from author where id >= 1;

-- 그리고 조건 더 쓰기
select * from author where id >= 1 and name = "박길동";
select * from author where id >= 1 or name = "박길동";

-- 중복되는 값 제거
select distinct password from author;

-- 오름차순 정렬 (기본값)
select * from author order by id asc;
select * from author order by email asc;
-- 내림차순 정렬
select * from author order by id desc;
select * from author order by email desc;

-- 갯수 제한 (2개만)
select * from author order by name limit 2;
```

## 컬럼 및 테이블에 별도의 이름 붙이기

- 컬럼명에 별칭 붙이기

```sql
select name as "이름", email as "메일주소" from author;
```

- 테이블명에 별칭 붙이기

```sql
select name as "이름", email as "메일주소" from author 작성자;
-- ✅ 테이블 별칭에는 AS 생략 & 따옴표 사용 안 함
```

- null 을 조회 조건으로 사용
  - null 은 `값이 없다`는 의미
  - `is null` 은 값이 없는 경우를 검색
  - `is not null` 은 값이 있는 경우를 검색

## 데이터 종류

### 1. 숫자

- tinyint : -128 ~ 127 까지, 나이 등
- `int` : -20억 ~ 20억까지, 일반적 정수에 사용
- bigint : 가장 큰 범위, 글로벌 서비스 시 활용
- unsigned : 무조건 양수로( tinyint unsigned : 0 ~ 254 )

### 2. 실수 (소수점)

- decimal(진수, 소수점) : 증권, 금융거래 정보 등 정확한 정보
- float, double : 일반적 실수

### 3. 문자

- char(길이)

  - 0 ~ 255 글자, `내용과 상관없이 길이 만큼 차지`
  - 연산 속도가 빠름
  - 성별, 전화번호, 주민등록번호 등

- `varchar(길이)`

  - 가장 많이 사용
  - 0 ~ 65535 글자
  - 가변 길이 : `내용만큼 메모리를 사용`
  - 이름, 주소, 상품명 등

- `text`

  - 가변 길이
  - 별도로 길이 지정은 불가
  - varchar 보다 더 큰 범위를 지정할 때

- blob

  - 바이너리 데이터
  - 이미지 파일을 문자열로 전환 후 저장할 때
  - 픽셀의 값 모두 글자로 저장해 용량이 큼
  - 지금은 일반적으로 blob 보다는 실제 파일을 서버에 저장

- enum
  - 미리 들어갈 수 있는 특정 데이터 목록 값을 지정
  - "admin", "member" 등의 권한 설정시 사용

### 4. 날짜

- date

  - 날짜만 저장(YYYY-MM-DD)
  - 생년월일 활용

- datetime
  - 날짜와 시간을 모두 저장
  - 예를 들어, m 옵션을 주면 microsecond 단위까지 저장
  - YYYY-MM-DD HH:mm:ss
  - 가장 많이 사용 ( 주문시간, 글 작성 시간 등 )
  - 현재시간을 추력하는 함수 : current_timestamp( ), now( )
