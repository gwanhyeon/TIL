> SQL 테이블 복사

```sql
CREATE TABLE 새로만들테이블명 AS
SELECT * FROM 복사할테이블명 [WHERE 절]
```

> SQL 테이블 구조만 복사
 
```sql
CREATE TABLE 새로만들테이블명 AS
SELECT * FROM 복사할테이블명 WHERE 1=2 [where에다가 참이 아닌 조건을 넣어줌]
```
 
> SQL 테이블은 이미 생성되어 있고 데이터만 복사

```sql
INSERT INTO 복사할테이블명 SELECT * FROM 복사할테이블명 [WHERE 절]
```

> SQL 테이블 이름 변경

```sql
ALTER TABLE 구테이블명 RENAME TO 신테이블명
```